---
title: "Only teach what it can learn"
date: 2026-10-23
description: "My first multi-task RL run learned almost nothing about math. The fix was in the data, not the algorithm."
---

I have been running reinforcement learning on a small open-weight model in my own time. I train it on four kinds of tasks at once: answering questions from retrieved documents, producing flat and nested JSON, following instructions, and solving math problems.

The first run went well for three of these. Retrieval answers and structured output improved clearly, but math barely moved.

The method I use is GRPO. It samples several answers to the same question and learns by comparing them. If all the answers are wrong, or all of them are right, there is nothing to compare, and the model learns nothing from that question. Most of my math questions were too hard for this model. It got every attempt wrong, so most of the math in each batch contributed nothing to training.

The run also made answers shorter everywhere, even in ordinary chat. I don't know yet which part of the mix caused this. It could be the retrieval data, the instruction-following data, or the way I wrote the rewards, and I will need a separate experiment to find out.

Before the second run, I measured what the model could already do. For every question, I sampled four answers, and if all four were wrong, I sampled four more. I then kept only the questions it solved sometimes but not always. About 10,000 questions were left after this filter.

These are the results of the second run, compared with the starting model:

| Benchmark | Before | After |
|---|---|---|
| IFEval | 43.2 | 57.5 |
| GSM8K | 74.2 | 80.2 |
| IFBench (constraint types never seen in training) | 17.0 | 22.3 |

All three gains held up under a paired significance test. The IFBench result is the one I care about most. None of its constraint types appeared in training, so the improvement shows the model got better at following instructions in general.

I now have two models that are good at different things. I am combining them into one through distillation, with the original model as a third teacher for everyday chat, so that the shorter answers stay limited to the tasks that needed them.
