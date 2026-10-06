**Pre-train the model on a different task from the target task, using much larger amounts of data. Fine-tune the model on the target task.**

Pre-training: initialize parameters randomly, then…
- Option A: unsupervised pre-training on very large set of unlabeled instances.
- Option B: supervised pre-training on a very large set of labeled instances.

Fine-tuning: initialize parameters to values from pre-training, then...
- (optionally) add a small prediction head.
- train on the target task.