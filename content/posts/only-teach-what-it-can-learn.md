---
title: "Only teach what it can learn"
date: 2026-10-23
description: "My first multi-task RL run learned nothing about math. The fix was in the data, not the algorithm."
---

I've been running reinforcement learning on a small open-weight model in my own time, across four kinds of task at once: answering from retrieved documents, producing flat and nested JSON, following instructions, and math.

The first run went well on three of them. Retrieval answers and structured output improved clearly. Math barely moved.

## Why math didn't move

The method I use, GRPO, learns by comparing several answers to the same question. If all of them are wrong, or all of them are right, there is nothing to compare, and the question teaches the model nothing.

Most of my math questions were simply too hard for this model. It got every attempt wrong, so most of the math in each batch produced no learning at all.

The run also had a side effect: answers got shorter everywhere, even on ordinary chat. I don't yet know which part of the mix caused it. It could be the retrieval data, the instruction-following data, or how I wrote the rewards. Finding out properly needs its own experiment.

## The fix

Before the second run, I measured what the model could already do. For every question, I sampled four answers. If all four were wrong, I sampled four more. Then I kept only the questions it solved sometimes but not always. About 10,000 questions survived.

The second run, compared with the starting model:

| Benchmark | Before | After |
|---|---|---|
| IFEval | 43.2 | 57.5 |
| GSM8K | 74.2 | 80.2 |
| IFBench (constraint types never seen in training) | 17.0 | 22.3 |

Each of these gains held up under a paired significance test. The IFBench result matters most to me, because it means the model learned to follow instructions, not just the instructions I trained on.

## What's next

Two models now do different things well. I'm combining them into one by distillation, with the original model as a third teacher for everyday chat, so the shorter answers don't spread beyond the tasks that wanted them.
