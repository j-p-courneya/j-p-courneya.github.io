---
title: "Adding a DNA Mode to RustQC"
date: 2026-11-24
description: "Extending a fast Rust QC tool to cover the DNA sequencing work our core actually runs."
draft: true
---

Read QC is the first step of almost every pipeline I run, and for years that has meant FastQC. It works, but it's slow enough on large runs that it shows up in the wall-clock time of the whole workflow.

[RustQC](https://github.com/seqeralabs/rustqc) is Seqera's Rust reimplementation of that idea, and it's fast. What it didn't cover was all of the DNA sequencing work our core does day to day, so I built a `rustqc dna` extension for our own use.

> **TODO:** Describe what DNA mode actually adds (which metrics or checks), and what it speeds up compared with your previous QC step.

## Why I'm not sending it upstream

This is a fork for us, not a contribution. The extension solves our problems and carries assumptions about our data, and I'd rather keep it honest about that than file a pull request that asks the maintainers to support choices they didn't make.

That said, I asked Phil Ewels, who develops RustQC, where the project is heading. I'd like to help with what he actually needs rather than what I happened to build, and I expect to learn more from working on the real roadmap than from maintaining a fork in parallel.

> **TODO:** Add what came of that conversation, and whether any of this ended up upstream after all.

## Learning Rust by having a reason to

The other honest reason for this project is that I wanted to write Rust with a real problem in front of me. QC is a good place for it: the logic is simple, the data is large, and the performance difference is immediately visible. Working inside someone else's well-built codebase taught me more about the language than any tutorial had.
