Gradient tape is a way to implement automatic differentiation by storing the topological order of the nodes in the computational graph using a linear gradient tape. It is used by Tensorflow 2.

```
global tape = stack()

class Module:
	method init()
		out_tensor= null
		out_gradient= Tensor(1)
	
	method apply_fwd(List in_modules)
		in_tensors = [x.out_tensor for x in in_modules]
		out_tensor = forward(in_tensors)
		tape.push(self)
		return self
	
	method apply_bwd():
		in_gradients= backward(in_tensors , out_tensor , out_gradient)
		for i in , ... , len(in_modules):
			in_modules[i].out_gradient += in_gradients[i]
			return self
	
function tape_bwd():
	while len(tape) > 0
	m = tape.pop()
	m.apply_bwd()
```