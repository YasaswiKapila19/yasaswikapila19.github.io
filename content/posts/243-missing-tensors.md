---
title: "243 missing tensors"
date: 2026-09-14
description: "My fine-tuned model kept repeating the same few words. I spent a while on the training before I found the bug in how the checkpoint was loaded."
---

After fine-tuning, my model was producing garbage, repeating the same few words over and over. I assumed something had gone wrong in training and spent a good amount of time adjusting the training setup.

To check whether the model could learn at all, I trained it on just five examples until it memorised them. It memorised all five, but generation still produced the same repeated words. So the training was working, and the problem was somewhere else.

The problem was in loading the checkpoint. The loading script renamed every weight slightly before loading it, and after the rename none of the names matched what the model expected. The loader was set to be lenient about mismatches, so it skipped all 243 weights without raising an error, and the model ran on its random starting values. There was also a second, smaller bug in how the generation code passed its inputs.

Since then, I do three things:

- When a loader is set to be lenient, I check exactly what it skipped.
- I keep a small memorisation test and run it before any long job.
- I pass arguments by name whenever code moves from one library to another.

This taught me to check the boring parts first, like whether the weights actually loaded, before changing anything in training.
