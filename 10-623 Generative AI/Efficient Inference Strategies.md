# Paged Attention
Paged attention brings virtual memory and page table to GPU to manage KV cache allocation and access.

This reduces fragmentation and **allows more requests to run concurrently**.

# Speculative Decoding
1. Use a large target model to prefill the prompt.
2. Use a small draft model to propose next tokens.
3. Use a large target model to verify or reject these proposals in chuns.

Advantage: reduce large model calls per token to improve throughput.

