CPU device.
```python
class CPUDevice(Device):
	def randn(self, *shape):
		return numpy.random.randn(*shape)
```

Initialize a CPU device.
```python
def cpu():
	"""Return cpu device"""
	return CPUDevice()
```

Initialize a random normal Tensor on a given device.
```python
def randn(*shape, device=None, dtype="float32", requires_grad=False):
	device = ndl.cpu() if device is None else device
	array = device.randn(*shape)
	return ndl.Tensor(array, device=device, dtype=dtype, requires_grad=requires_grad)
```