---
title: "Teaching Nextflow to Collaborators in Mali"
date: 2026-11-24
description: "Lessons from a three-hour, Zoom-based Nextflow course on a collaborator's server with no working scheduler."
draft: true
---

This summer I designed and taught a Nextflow course for our collaborators in Mali, built around the [snp_call_nf](https://github.com/bguo068/snp_call_nf) variant-calling pipeline for *Plasmodium*. It was a three-hour session over Zoom for up to eight learners, with an optional office hour afterward, and it ran on July 29, 2026. It went well, and getting there taught me a lot about teaching people who will run a pipeline rather than write one.

## Who the course was for

The learners were going to be pipeline users. They needed to copy the pipeline, point it at a sample sheet, launch a run, and know what to do when something failed. That shaped everything: less time on writing processes, more time on configuration, sample sheets, and reading errors. I later turned this framing into a talk at the Nextflow Summit 2026 called "Teaching Nextflow Config, Not Code."

Everything ran on pre-staged test data. With eight people joining internationally over Zoom, running on their own files was out of scope for the session.

## The server

The course ran on the collaborators' own server, a large shared machine with 128 threads and close to a terabyte of RAM. SLURM was installed but its daemons weren't running, so we used Nextflow's local executor with a training config that capped resources per session. A full run on the bundled test data took about 16 minutes on its own (115 tasks), so I budgeted 20 to 25 minutes with all eight learners running at once.

> **TODO:** Confirm whether learners ran the full test-data pipeline or `-stub-run` during the live session.

## Things that would have broken the class

Most of the preparation went into finding problems before learners hit them. A few worth sharing:

- **Copy carefully.** The pipeline's reference folder is about 16 GB, so learners rsync the repo with the reference excluded and symlink it instead. Excluding the hidden `.nextflow*` files turned out to be essential. Without that, learners inherited the staging account's run cache, and their tasks pointed into someone else's work directories.
- **Config precedence.** The pipeline sets its retry behavior inside a profile, and Nextflow applies profiles after the `-c` config files, so my top-level overrides were silently replaced. Nesting the training overrides inside the same profile fixed it.
- **Java on a shared server.** A stale system-wide `JAVA_HOME` pointed at a Java install that no longer existed. Nextflow only worked when its environment was properly activated, and setting `LD_PRELOAD` to fix a tool in the other environment broke the JVM entirely. The fix was to call those tools by absolute path.
- **One shared tools environment.** The pipeline's tool environment was built once and shared. Eight people each building their own conda environment over a slow connection would have eaten the whole session.
- **tmux first.** Learners started a tmux session before anything else, so a dropped Zoom or SSH connection didn't kill a running pipeline.

## A bug we found along the way

While testing an optional mode that skips some steps, I found that a `.collect()` on an empty channel still emits an empty list, which sent joint genotyping off to run fourteen times on nothing and crash. The one-line fix is to filter out empty lists after the collect. We kept that mode out of the course and I passed the fix along to the pipeline's author.

## What I'd keep

Keep the scope small, stage everything in advance, test as a regular user account, and teach people how to read a failure. A learner who can find the failing task's work directory and read its `.command.err` is ready to run the pipeline on their own data afterward.
