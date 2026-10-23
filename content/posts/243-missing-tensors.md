---
title: "243 missing tensors"
date: 2026-09-14
description: "My fine-tuned model was babbling. The training was fine. Loading it was not."
---

After fine-tuning, my model produced garbage: the same few words, over and over. I assumed something was wrong with the training, so I spent a while adjusting it.

Then I tried the most boring test I know. I trained the model on just five examples until it had memorised them perfectly. If a model can't repeat five answers it has memorised, the problem isn't learning.

It had memorised them. It still babbled.

## The real problem

The weights were fine. They were never making it into the model.

The script that loaded the checkpoint renamed every weight slightly before loading it, and after the rename, none of the names matched what the model expected. The loader was set to be forgiving about mismatches, so it didn't complain. It skipped all 243 weights and ran the model on random numbers.

There was a second, smaller bug in how the generation code passed its inputs, which didn't help.

## What I do now

- When a loader is set to be forgiving, I check exactly what it skipped.
- I keep a tiny memorisation test and run it before any long job.
- I name arguments explicitly whenever code crosses from one library into another.

The training run had been fine all along. I'd been debugging the wrong half of the problem.
