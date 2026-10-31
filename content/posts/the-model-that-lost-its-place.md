---
title: "The model that lost its place"
date: 2026-10-04
description: "Our CUDA-graph fast path silently dropped the positional encoding, and nothing threw an error."
---

Language models don't naturally know the order of the words they read. Positional encoding is what gives them this information. We use a variant called YaRN, which stretches the model's sense of position so that a model trained on shorter text can handle longer documents. We added YaRN to our model and checked that it worked.

To make generation faster, a GPU can record a sequence of operations once and then replay that recording again and again, which skips a lot of overhead. These recordings are called CUDA graphs, and they are one of the easiest ways to speed up inference.

A recording only contains what was passed into it at the time. Our YaRN settings were connected to the normal code path but never reached the recorded one, so whenever the model ran through the fast path, it fell back to having no positional encoding at all. This didn't cause any errors. The outputs were only slightly worse, which made it easy to blame on something else.

The fix was small, but finding the problem took much longer. I found it by running the same input through both the normal path and the recorded path and comparing the outputs, which should have been identical but weren't. I now keep a check that compares both paths on a few fixed inputs, and it runs whenever either one changes.
