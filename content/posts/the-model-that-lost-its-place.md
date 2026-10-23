---
title: "The model that lost its place"
date: 2026-10-04
description: "Our speed-up path quietly dropped the positional encoding. The model didn't crash. It just forgot word order."
---

Language models don't naturally know the order of the words they read. Positional encoding is what tells them. We use a variant called YaRN, which stretches that sense of position so a model trained on shorter text can read longer documents.

We added YaRN to our model, checked that it worked, and moved on.

## The fast path

To make generation faster, a GPU can record a sequence of operations once and then replay that recording over and over, skipping a lot of overhead. These recordings are called CUDA graphs, and they're one of the easiest speed-ups available.

The catch is that the recording only contains what was actually passed into it. Our YaRN settings were wired into the normal code path but never reached the recorded one. So whenever the model ran through the fast path, it silently fell back to no positional encoding at all.

Nothing crashed. Outputs just got a little worse in ways that were easy to blame on anything else.

## What gave it away

The fix itself was small. Finding it took longer. What finally worked was running the same input through the normal path and the recorded path, then comparing the outputs side by side. They should have matched. They didn't.

> If you have a fast path and a slow path, they need the same tests. The fast path is the one users actually hit.

I now keep a check that compares both paths on a few fixed inputs, and it runs whenever either one changes.
