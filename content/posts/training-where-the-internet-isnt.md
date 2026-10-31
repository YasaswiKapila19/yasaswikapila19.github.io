---
title: "Training where the internet isn't"
date: 2026-07-20
description: "Lessons from building a training setup for machines that will never see the internet."
---

Some of my work runs on machines that have no internet connection at all. On these machines, you can't install a missing package or download a dataset you forgot, and every gap means another trip with a drive. Over time, this changed the way I set things up.

Anything that needs the internet becomes a script that I run once, on a different machine. I download the data, save it, and carry the whole folder in. I also pin every library to an exact version, because the version I test with has to be the same one that arrives on the machine.

The fastest attention code only works with exact versions of its dependencies. So our model first tries the fastest option, then a slower one, and finally a plain version that always works. When I can't fix the environment myself, a slower run is still better than no run.

I run short smoke tests and follow simple written runbooks, so code never runs for the first time on the real hardware. Without the internet I can't search for an error message, so I try to run into most of the errors before I get there.

On every run, I track the same few numbers: how fast it is going, how much memory it is using, and whether the loss is falling the way it should. If these look right, most other things usually are too.
