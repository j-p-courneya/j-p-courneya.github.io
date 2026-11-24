---
title: "Teaching Nextflow Config, Not Code"
date: 2026-11-24
description: "Lessons from running a hands-on Nextflow session over Zoom for collaborators in Mali."
draft: true
---

<!-- TODO: link your Nextflow Summit 2026 talk recording or slides if they're public, and confirm the talk title. -->

In July I ran a three-hour Nextflow session over Zoom for eight collaborators in Mali, built around `snp_call_nf`, a variant-calling pipeline for *Plasmodium* that a colleague maintains. I later presented the approach at the Nextflow Summit 2026. The core idea is simple: most people who use a pipeline will never write one, so teach them the parts they'll actually touch.

## The goal for the session

By the end, every learner should be able to copy the pipeline, edit the sample sheet, launch a run on pre-staged test data, and know what to do when it fails. Running their own data was deliberately out of scope. With eight people, an international connection, and a shared server, that would have eaten the whole session.

## Config is the skill

Pipeline users live in config files: resource limits, executors, profiles, paths. So the session spent real time on how Nextflow reads configuration, including one detail that bit me while preparing. Overrides in a `-c` file have to sit inside the same profile block the pipeline uses, because Nextflow applies the profile after it reads your file. A top-level `errorStrategy` in my training config was silently replaced by the pipeline's own retry setting until I moved it.

## The server mattered as much as the lesson

The collaborators' server is big (128 threads, close to 1 TB of RAM) but has no working scheduler, so everything ran on Nextflow's local executor with a training config that capped each learner's resources. A full test run took about 16 minutes on its own, so I budgeted 20 to 25 with everyone running at once.

A few setup lessons I'd pass on to anyone teaching on a shared machine:

- Pre-build the pipeline's software environment once and point every learner at it. Eight people building the same conda environment at once is a session-killer.
- Don't let learners copy the whole repo. The reference folder was 16 GB; they copied the code and symlinked the references.
- Exclude the `.nextflow` cache when copying. Otherwise learners inherit the staging account's run history and their tasks point at someone else's work directories.
- Start every session inside `tmux`, so a dropped connection doesn't kill a running pipeline.
- Be careful with `LD_PRELOAD` in environment scripts. It loads into the JVM too, and Nextflow fails with errors about native threads.

## Finding a real bug along the way

Testing an optional flag turned up a pipeline bug: calling `.collect()` on an empty channel still emits an empty list, so a downstream step ran once per genome interval with nothing to process and crashed. The fix is a one-line filter after the collect. Breaking things on purpose while preparing a lesson is a good way to find out what a pipeline really does.

<!-- TODO: say whether the .collect() fix was reported or merged upstream. -->

The session went well, and the format (config first, real runs on staged data, limited deliberate breakage) is the one I'll reuse.
