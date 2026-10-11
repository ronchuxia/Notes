# Forward
```python
class Value:
	"""A Value is a node in the computational graph."""
	
	def _init(...)
		# The operation that produced this value, may be None.
		self.op = op
		# The inputs of the operation that produced this value.
		self.inputs = inputs
		
	def realize_cached_data(self):
		# self.cached_data is NDArray
		self.cached_data = self.op.compute(
			*[x.realize_cached_data() for x in self.inputs]
		)
		return self.cached_data
```

```python
class Tensor(Value):
	grad: "Tensor"

    @staticmethod
    def make_from_op(op, inputs):
	    # Make a new node in the computational graph.
        tensor = Tensor.__new__(Tensor)
        
        # Link the new node to its parents. Determine tensor.requires_grad.
        tensor._init(op, inputs)
        
        if not LAZY_MODE:
            if not tensor.requires_grad:
	            # Make a new node but don't link it to its parents.
                return tensor.detach()
                
            # Populate Value.cached_data with NDArray data.
            tensor.realize_cached_data()
        return tensor
	
    # Override operators to call corresponding TensorOp.__call__(), which calls Tensor.make_from_op(), which calls Value.realize_cached_data(), which calls Op.compute().
	def __matmul__(self, other):
		return needle.ops.MatMul()(self, other)
	
	def transpose(self, axes=None):
		return needle.ops.Transpose(axes)(self)
		
	__radd__ = __add__ # 1 + t
	__rmul__ = __mul__ # 1 * t
```

How Tensor operation works:
- Overridden operator calls `TensorOp.__call__()`.
- `TensorOp.__call__()` calls `Tensor.make_from_op()` to make a new node in the computational graph.
- `Tensor.make_from_op()` calls `Value.realize_cached_data()`.
- `Value.realize_cached_data()` calls `TensorOp.compute()` to populate `Value.cached_data` with `NDArray` data.

Needle builds a new computational graph in each forward pass.

# Backward
```python
class Tensor(Value):
	def backward(self, out_grad=None):
		out_grad = (
			out_grad
			if out_grad
			else init.ones(*self.shape, dtype=self.dtype, device=self.device)
		)
		compute_gradient_of_variables(self, out_grad)
```

```python
def compute_gradient_of_variables(output_tensor, out_grad):
    # A map from a node to a list of gradient contributions from its child nodes.
    node_to_output_grads_list: Dict[Tensor, List[Tensor]] = {}
    node_to_output_grads_list[output_tensor] = [out_grad]
	
    # Traverse graph in reverse topological order given the output_node that we are taking gradient wrt.
    reverse_topo_order = list(reversed(find_topo_sort([output_tensor])))
	
    for node in reverse_topo_order:
        node.grad = sum_node_list(node_to_output_grads_list[node])
	
        if not node.is_leaf():
            out_grads = node.op.gradient_as_tuple(node.grad, node)
            for i, input in enumerate(node.inputs):
                if input in node_to_output_grads_list:
                    node_to_output_grads_list[input].append(out_grads[i])
                else:
                    node_to_output_grads_list[input] = [out_grads[i]]
```

# Detach
```python
class Tensor(Value):
    # Make a new tensor that shares the data but detaches from the graph.
    def detach(self):
		return Tensor.make_const(self.realize_cached_data())
```