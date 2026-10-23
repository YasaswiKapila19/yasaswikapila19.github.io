---
title: "Training where the internet isn't"
date: 2026-07-20
description: "Lessons from building a training setup for machines that will never see the internet."
---

Some of my work runs on machines with no internet connection at all. You can't install a missing package or download a dataset you forgot. Every gap means another trip with a drive.

That changes how you build things.

## Bring everything at once

Anything that needs the internet becomes a script you run once, somewhere else. Download the data, save it, carry the whole folder in. Pin every library to an exact version, because the one you test with has to be the one that arrives.

## Fall back instead of failing

The fastest attention code needs very specific versions of very specific software. So our model tries the fastest option first, then a slower one, then a plain one that always works. A slower run beats no run when you can't fix the environment yourself.

## Rehearse before the real thing

Short smoke tests and simple written runbooks mean the first time code runs on the real hardware is never its first time running anywhere. When you can't search for an error message, you want very few error messages.

## Watch a few numbers

I track the same handful of numbers on every run: how fast it's going, how much memory it's using, and whether the loss is falling the way it should. If those look right, most other things usually are.
