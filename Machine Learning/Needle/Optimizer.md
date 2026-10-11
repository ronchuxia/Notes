```python
class Optimizer:
    def __init__(self, params):
        self.params = params
	
	def step(self):
        raise NotImplementedError()
	
    def reset_grad(self):
        for p in self.params:
            p.grad = None
```

Optimizer updates parameters using `Tensor.data`, which returns a detached `Tensor`.

```python
class Tensor(Value):
	@property
	def data(self):
		return self.detach()
	
	@data.setter
    def data(self, value):
        self.cached_data = value.realize_cached_data()
```