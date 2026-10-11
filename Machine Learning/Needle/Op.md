```python
class Op:
	def __call__(self, *args):
		raise NotImplementedError()
	
	def compute(self, *args):
		"""Forward pass.
		
		The inputs and outputs are NDArray.
		"""
		raise NotImplementedError()
	
	def gradient(self, out_grad, node):
		"""Backward pass.
		
		The inputs and outputs are Value.
		"""
		raise NotImplementedError()
```

```python
class TensorOp(Op):
	"""An Op class specialized to output Tensor."""

	def __call__(self, *args):
		"""Make a new node in the computational graph."""
		return Tensor.make_from_op(self, args)
```

```python
class Log(TensorOp):
	def compute(self, a):
		return array_api.log(a)
		
	def gradient(self, out_grad, node):
		"""
		Use TensorOp in backward pass to extend computational graph.
		"""
		a = node.inputs[0]
		return out_grad * power_scalar(a, -1)

# The convenient function calls TensorOp.__call__() to make a new node.
def log(a):
	return Log()(a)
```

# Numerical Stability
Apart from basic operations, some compositional operations (e.g. `LogSoftmax`) are defined to:
1. Improve numerical stability.
2. Fuse multiple basic operations into a single node to accelerate forward and backward pass.

Note that `LogSumExp` can be also composited using basic operations to improve numerical stability, if Needle provides a `Max(TensorOp)`, but it doesn't.