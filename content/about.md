---
title: "About"
description: "Data scientist at Neuralix.AI working on large language models."
---

I'm Yasaswi, a data scientist at Neuralix.AI. I work on large language models: model architecture, distributed pretraining, and post-training with supervised fine-tuning, preference optimisation and reinforcement learning. I also make our models work with Hugging Face and vLLM.

I'm most interested in how architecture choices affect training and inference, and in using reinforcement learning to improve how models behave on real tasks.

In my own time, I post-trained Qwen2.5-1.5B with reinforcement learning and multi-teacher distillation. It's described on the [Projects]({{< relref "projects.md" >}}) page, with the code on [GitHub](https://github.com/YasaswiKapila19/rl-quant-retention) and the models on [Hugging Face](https://huggingface.co/YashKap19).

## Experience

**Neuralix.AI, Data Scientist** (January 2026 to now)

I build custom LLMs for the Indian Army, trained and run on air-gapped infrastructure.

- **Pretraining.** We pretrained two models from scratch: a 10B-parameter sparse mixture-of-experts model, with about 1.9B parameters active per token, and a 3B dense model. I worked on the architecture and trained the 10B model with Megatron-LM on five H200 nodes at about 43% MFU. I also built a pretraining stack from scratch in PyTorch and DeepSpeed, the conversion between Megatron and Hugging Face checkpoints, and the setup to serve the models in vLLM.
- **Post-training.** I set up DAPO and multi-teacher on-policy distillation on the 10B model and improved it on 16 tasks, from grounding and instruction following to Python and long-context recall. I also trained a reasoning model with SFT on reasoning traces and a short mid-training run. It matched the instruct model after SFT and beat it after RL.
- **Retrieval.** I built a hybrid-search RAG system over their documents, because a model can't reliably recall facts from a private dataset that small.

**Tata Consultancy Services, Systems Engineer** (October 2023 to July 2025)

I led the support team for an enterprise CRM built on Power Apps and ran the weekly governance calls with the client.

## Education

I studied chemical engineering at JNTU Hyderabad (B.Tech, 2019 to 2023) and, alongside it, completed a BS in Data Science and Applications at IIT Madras (2021 to 2025).

## Outside work

I enjoy driving, follow tennis, football, basketball and F1, and read manga and light novels. I also have a dog, Kali.

## Contact

Email is best: yasaswi.kapila@gmail.com. I'm happy to talk about LLM training and reinforcement learning. You can also find me on [GitHub](https://github.com/YasaswiKapila19) and [Hugging Face](https://huggingface.co/YashKap19).
