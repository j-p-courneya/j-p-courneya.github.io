---
title: "A Claude Skill for NIH Data Management and Sharing Plans"
date: 2026-11-24
description: "Why I rebuilt my open-source DMSP skill to mirror the new 2026 NIH format page."
draft: true
---

NIH changed its Data Management and Sharing Plan format for applications due on or after May 25, 2026 (NOT-OD-26-046). The new format is a form: seven elements, mostly checkboxes, one limitations text box capped at 300 words, a two-column data table capped at 100 words, and a set of Genomic Data Sharing questions.

I'd already built an open-source Claude skill for drafting DMSPs, [nih-dmsp-skill](https://github.com/j-p-courneya/nih-dmsp-skill), released under the MIT license. When the new format came out, I tested it against the official page and found the output was too detailed. It was writing a thorough essay for a form that now mostly wants boxes checked.

## What changed

I reworked the skill to mirror the format page itself. Given a description of the study, it now produces:

- The plan as a filled-in version of the NIH format page, as a Word file, with the right boxes checked and the two text fields kept inside their limits.
- A separate markdown companion with budget justification language, the assumptions it made, and a review checklist.

Splitting the output that way keeps the plan itself short, which is what reviewers expect now, and puts the reasoning somewhere the investigator can check it.

## Why a skill

A skill is a folder of instructions and reference material that Claude loads when a task calls for it. For something like a DMSP, that means the current rules travel with the instructions instead of depending on what a model happens to remember about an older format. It's also easy for other research support people to install and adapt.

> **TODO:** Add a short example (a sample input and what the generated plan looked like), and how people at your institution have used it.

If you support grant writers and want to try it, the repo has examples and installation instructions. Issues and pull requests are welcome.
