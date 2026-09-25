Scaling laws for transformer LLMs.

# Power Law
Most scaling laws for transformer LLMs fit a power law.
$$
f(x) = cx^{-k}
$$

# Kaplan et al. (2020)
Key takeaways:
1. **Three quantities dominate: N = # parameters, D = # tokens, C = # FLOPS.**
2. Model shape doesn't matter much: A wide range of shapes achieve similar performance.
3. Performance improves as both N and D increase.
4. **Large models are more sample efficient**: large models require fewer samples to reach the same performance as small models.
5. Convergence is not critical for good performance: tap off at an inflection point reduces compute by several orders of magnitude. 
6. **Best batch size follows a power law**: and is huge (e.g. 1-2M tokens).

**Sample efficiency: performance obtained per training token.**
“every time we increase the model size 8x, we only need to increase the data by roughly 5x to avoid a penalty.”

**Compute efficiency: performance obtained per unit of computation.**
For a fixed increase in compute (FLOPS), Kaplan allocates more additional compute to increasing model size than to increasing data size.

# Hoffman et al. (2022)
Hoffman disagrees with Kaplan on compute efficiency.

For a fixed increase in computational budget (FLOPS), Hoffman allocates same additional compute to increasing model size and to increasing data size.

# Data Filtering vs. Scaling Law
Phi family of small LLMs: Instead of increasing model and data size, improve the quality of data.

Goyal et al. (2024):
- With small compute, highly aggressive filtering is best.
- With large compute, less aggressive filtering is best.

Note that **quality of data is application dependent**.