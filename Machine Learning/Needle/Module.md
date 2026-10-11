# Parameter
```python
class Parameter(Tensor):
	"""A wrapper around Tensor."""
```

# Module
```python
class Module:        
    def __call__(self, *args, **kwargs):
		return self.forward(*args, **kwargs)
```

```python
class Linear(Module):
	def __init__(...):
		self.weight = Parameter(init.kaiming_uniform(...))
		self.bias = Parameter(init.kaiming_uniform(...))
		
	def forward(self, X):
		"""Forward pass.
		
		The inputs and outputs are Tensor.
		"""
		out_shape = X.shape[:-1] + (self.out_features,)
		return X @ self.weight + self.bias.broadcast_to(out_shape)
```

Note that **Needle does not support implicit broadcasting**. Although `TensorOp.compute()` calls NumPy API, which supports implicit broadcasting, `TensorOp.gradient()` does not. If a value is implicitly broadcasted in `TensorOp.compute()`, `TensorOp.gradient()` will return a gradient with the wrong shape. Therefore, we need to explicitly broadcast each value to the correct shape.

Explicit broadcasting is achieved through `ops.reshape` and `ops.broadcast_to`.

# Module Parameters
```python
class Module:
	def parameters(self):
        return _unpack_params(self.__dict__)
```

```python
def _unpack_params(value):
    if isinstance(value, Parameter):
        return [value]
    elif isinstance(value, Module):
        return value.parameters()
    elif isinstance(value, dict):
        params = []
        for k, v in value.items():
            params += _unpack_params(v)
        return params
    elif isinstance(value, (list, tuple)):
        params = []
        for v in value:
            params += _unpack_params(v)
        return params
    else:
        return []
```

# Train Mode and Eval Mode
```python
class Module:
	def __init__(self):
		self.training = True
	
	def train(self) -> None:
        self.training = True
        for m in self._children():
            m.training = True
    
	def eval(self) -> None:
		self.training = False
		for m in self._children():
			m.training = False
```

Eval mode only changes the behavior of some modules. The computational graph is still built in eval mode.