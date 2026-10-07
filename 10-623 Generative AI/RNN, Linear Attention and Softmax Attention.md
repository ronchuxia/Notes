All three models keep a "state" of the past.

|                 | RNN                     | Linear attention transformer                                     | Softmax attention transformer |
| --------------- | ----------------------- | ---------------------------------------------------------------- | ----------------------------- |
| State           | vector $h_t$            | matrix $S_t$ and vector $z_t$                                    | KV cache                      |
| State size      | fixed                   | fixed                                                            | grows with $t$                |
| Update          | $h_t = f(h_{t-1}, x_t)$ | $S_t = S_{t-1} + \phi(k_t)\, v_t^T$, $z_t = z_{t-1} + \phi(k_t)$ | append $k_t, v_t$             |
| Cost per step   | O(1)                    | O(1)                                                             | O(t)                          |
| Old information | compressed, can be lost | compressed, can be lost                                          | kept exactly                  |

# Linear Attention
Linear attention replaces the softmax attention score with:
$$
\text{sim}(q, k) = \phi(q)^T \phi(k)
$$
where $\phi$ is a fixed function that maps a length-d vector to a length-m vector with positive entries (e.g. $\phi(x) = \mathrm{elu}(x) + 1$).

The output at position t:
$$
o_t = \frac{\sum_{i=1}^t \phi(q_t)^T \phi(k_i) v_i^T}{\sum_{i=1}^t \phi(q_t)^T \phi(k_i)} = \frac{\phi(q_t)^T \left( \sum_{i=1}^{t} \phi(k_i)\, v_i^T \right)}{\phi(q_t)^T \left( \sum_{i=1}^{t} \phi(k_i) \right)}
$$

Let the two sums be:
$$
S_t = \sum_{i=1}^{t} \phi(k_i)\, v_i^T
$$
$$
z_t = \sum_{i=1}^{t} \phi(k_i)
$$

Then
$$
S_t = S_{t-1} + \phi(k_t)\, v_t^T
$$
$$
z_t = z_{t-1} + \phi(k_t)
$$
$$
o_t = \frac{\phi(q_t)^\top S_t}{\phi(q_t)^\top z_t}
$$

Softmax attention can't be expressed in this recurrent form due to the softmax.

# State Space Models
An SSM models the relation between continuous **scalar** function $x(t)$ and continuous **scalar** function $y(t)$ with the following ODE:
$$
\mathbf h'(t) = \mathbf A \mathbf h(t) + \mathbf B x(t)
$$
$$
y(t) = \mathbf C \mathbf h'(t) + \mathbf D x(t)
$$
which can be discretized as:
$$
\mathbf h_k = \bar{\mathbf A} \mathbf h_{k-1} + \bar{\mathbf B} x_k
$$
$$
y_k = \bar{\mathbf C} \mathbf h_k + \bar{\mathbf D}x_k
$$

Therefore, an SSM is a layer that keep a **fixed-size hidden state**. At each step, **it updates the hidden state with a linear recurrence**.

Thanks to the linear recurrence, SSMs are more **efficient** than transformers at inference time and at training time with long sequences. 

Deep SSMs add non linear layers between SSM layers to increase model expressivity.

# Hybrid Models
Some recent models mix linear attention layers (cheap) with softmax attention layers (exact recall) to leverage advantages of both methods.
