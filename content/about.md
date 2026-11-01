---
title: "About"
description: "Data scientist at Neuralix.AI working on large language models."
---

I'm Yasaswi, a data scientist at Neuralix.AI. I work on large language models: model architecture, distributed pretraining, and post-training with supervised fine-tuning, preference optimisation and reinforcement learning. I also make our models work with Hugging Face and vLLM.

I'm most interested in how architecture choices affect training and inference, and in using reinforcement learning to improve how models behave on real tasks.

In my own time, I post-trained Qwen2.5-1.5B with reinforcement learning and multi-teacher distillation. It's described on the [Projects]({{< relref "projects.md" >}}) page, with the code on [GitHub](https://github.com/YasaswiKapila19/rl-quant-retention) and the models on [Hugging Face](https://huggingface.co/YashKap19).

## Experience

**Neuralix.AI, Data Scientist** (January 2026 to now)

- **Pretraining.** I worked on Chimera, our own sparse mixture-of-experts model with about 10B parameters, of which about 1.9B are active per token. I helped design the architecture and trained it with Megatron-LM on five H200 nodes at about 43% MFU. I also built the conversion between Megatron and Hugging Face checkpoints and made the model run in vLLM.
- **Post-training.** I set up DAPO and multi-teacher on-policy distillation on our 10B model and improved it on 16 tasks, from grounding and instruction following to Python and long-context recall. I also trained a reasoning model with SFT on reasoning traces and a short mid-training run. It matched the instruct model after SFT and beat it after RL.
- **An air-gapped LLM stack.** For an Indian Army engagement, I built a pretraining stack from scratch in PyTorch and DeepSpeed for 1B to 3B models, with the evaluation, fine-tuning and runbooks needed to work without internet access. I also built a hybrid-search RAG system over their documents, because a model that size can't reliably recall facts from a small private dataset.

**Tata Consultancy Services, Systems Engineer** (October 2023 to July 2025)

I led the support team for an enterprise CRM built on Power Apps and ran the weekly governance calls with the client.

## Education

I studied chemical engineering at JNTU Hyderabad (B.Tech, 2019 to 2023) and, alongside it, completed a BS in Data Science and Applications at IIT Madras (2021 to 2025).

## Outside work

I enjoy driving, follow tennis, football, basketball and F1, and read manga and light novels. I also have a dog, Kali.

## Contact

Email is best: yasaswi.kapila@gmail.com. I'm happy to talk about LLM training and reinforcement learning. You can also find me on [GitHub](https://github.com/YasaswiKapila19) and [Hugging Face](https://huggingface.co/YashKap19).
