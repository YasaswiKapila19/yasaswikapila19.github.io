---
title: "Projects"
description: "Things I've built in my own time, with code and models you can try."
items:
  - date: "Oct 2026"
    title: "RL post-training and multi-teacher distillation on Qwen2.5-1.5B"
    summary: "Two RL teachers merged into one student that beats the original model on RAG, instruction following, JSON and math."
    links:
      - name: "GitHub"
        url: "https://github.com/YasaswiKapila19/rl-quant-retention"
      - name: "Hugging Face"
        url: "https://huggingface.co/YashKap19/Qwen2.5-1.5B-MOPD"
---

## RL post-training and multi-teacher distillation on Qwen2.5-1.5B

I wanted to see how far a 1.5B model could be pushed on the tasks a small RAG assistant actually needs, without breaking anything else.

I first trained two teachers from Qwen2.5-1.5B-Instruct with reinforcement learning (DAPO in verl). One learned grounded answering from documents and JSON output, and the other learned math and instruction following. I then merged both into one student with multi-teacher on-policy distillation, with the original model as a third teacher to keep its general behaviour in place.

Every model was scored on the same frozen, decontaminated test set of 15,768 items across 24 benchmarks, with paired significance tests. Compared with the original model, the student:

- answers HotpotQA correctly 49% of the time instead of 28%, and cites a supporting document 85% of the time instead of 13%;
- scores 59 on IFEval instead of 43, and 80 on GSM8K instead of 74;
- isn't significantly worse on any of the 24 benchmarks.

Along the way, I found that my first RL run had learned to game its instruction-following reward. It answered "✅✅✅" when asked for a summary with an emoji after every sentence. I fixed this in the second teacher by gating the reward with a reward model. I also patched verl so that three teacher models and the trainer fit on two H100s, and the whole distillation run took about two hours.

This taught me to read the model's outputs before trusting any score.

- Code and write-up: [github.com/YasaswiKapila19/rl-quant-retention](https://github.com/YasaswiKapila19/rl-quant-retention)
- Final model: [Qwen2.5-1.5B-MOPD](https://huggingface.co/YashKap19/Qwen2.5-1.5B-MOPD)
- Teachers: [RAG and JSON](https://huggingface.co/YashKap19/Qwen2.5-1.5B-RL-RAG-JSON), [math and instruction following](https://huggingface.co/YashKap19/Qwen2.5-1.5B-RL-Math-IF)
- Training data: [qwen2.5-1.5b-rl-mopd-mixes](https://huggingface.co/datasets/YashKap19/qwen2.5-1.5b-rl-mopd-mixes)
