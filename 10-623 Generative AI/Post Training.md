# Instruction Fine-Tuning
Instruction fine-tuning teaches LLMs to behave like chat assistants.

They are often trained with specific prompt templates that segment the prompt into:
- System prompt
- User message
- Assistant response

# RLHF
Human ranks a set of K responses. Trains a reward model to reward the LLM in RL training.

Model the probability that $y_w$ is preferred over $y_l$ with **Bradley-Terry preference model**:
$$
P(y_w \succ y_l) = \sigma(r_\theta(x, y_w) - r_\theta(x, y_l))
$$

Objective function for the reward model:
$$
\text{loss}(\theta) = -\frac{1}{K \choose 2} \mathbb E_{(x, y_w, y_l) \sim D} [\log(\sigma(r_\theta(x, y_w) - r_\theta(x, y_l)))]
$$

Objective function for RLHF (InstructGPT):
$$
l(\phi) = \mathbb E_{\pi^\text{RL}_\phi(\tau)} \left[ r_\theta(\tau) - \beta \log \frac{\pi_\phi^\text{RL}(\tau)}{\pi^\text{SFT}(\tau)} \right] - \gamma \mathbb E_{x \sim D_\text{pretrain}}[\log \pi_\phi^\text{RL}(x)]
$$

This is a PPO objective function plus a term to retain the performance on pre-training dataset.

# DPO
RLHF trains a reward model, then uses the reward model to fine-tune the pre-trained model with PPO. **DPO fine-tunes the pre-trained model directly to increase the likelihood of higher-ranking responses, and decrease the likelihood of lower-ranking responses.**

The PPO objective function:
$$
l(\phi) = \mathbb E_{\pi^\text{RL}_\phi(\tau)} \left[ r_\theta(\tau) - \beta \log \frac{\pi_\phi^\text{RL}(\tau)}{\pi^\text{SFT}(\tau)} \right]
$$
has a closed form solution:
$$
\pi_{\phi^*}(y | x) = \frac{1}{Z(x)} \pi^\text{SFT}(y|x) \exp \left( \frac{r_\theta(x, y)}{\beta} \right)
$$
for some normalizing factor $Z(x)$.

Plug $r_\theta(x, y)$ back into the Bradley-Terry preference model:
$$
P(y_w \succ y_l) = \frac{1}{1 + \exp \left( \beta \log \frac{\pi_{\phi^*}(y_l | x)}{\pi^\text{SFT}(y_l | x)} - \beta \log \frac{\pi_{\phi^*} (y_w | x)}{\pi^\text{SFT}(y_w | x)} \right)}
$$

Therefore, we can directly fine-tune $\phi$ to maximize this value.