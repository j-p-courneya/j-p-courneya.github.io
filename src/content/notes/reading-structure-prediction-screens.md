---
title: "Reading a Structure Prediction Screen Without Fooling Yourself"
date: 2026-11-24
description: "Why a promising interface score turned out to be an artifact of how the constructs were built."
draft: true
---

> **TODO:** This describes unpublished project work. Check with the PI before naming specific proteins or sharing numbers.

Structure prediction is a cheap way to screen candidate protein pairs before anyone goes to the bench. On one of our malaria projects I set up a multimer prediction pipeline on GPU nodes through the national ACES allocation, using AlphaPulldown to run predictions across many pairs of parasite and host proteins.

The first pass looked promising. The second pass, with better controls, taught me more.

## Two scores that disagreed

We scored predicted complexes two ways. One score rewards the size and quality of the predicted interface. The other, ipTM, reflects how confident the model is about the relative placement of the two chains.

The interface score produced some high values, well into the range people treat as encouraging. ipTM, meanwhile, was uniformly low across every pair we ran. When two scores disagree that cleanly, the interesting question is which one is measuring your biology and which one is measuring your inputs.

## The controls did the work

The thing that settled it was interleaving negative controls into the screen: proteins that live in a compartment where they could not plausibly meet the target. Those controls scored about as well as the real candidates. Whatever signal we were seeing, it wasn't specificity.

Going back through the inputs, the high interface scores tracked with truncated domain constructs. Shorter constructs can pack against a partner in a way that racks up contacts without the model being confident about the arrangement at all, and the interface score counts those contacts.

## What I took from it

- Run negative controls inside the same screen, not as a separate sanity check afterward. If a control scores like a hit, the pipeline is telling you something about itself.
- Treat construct boundaries as part of the experiment. Truncations change the score, not only the structure.
- When two metrics disagree, believe the more conservative one until you can explain the gap.
- A screen that produces no hits is still a result, as long as you can say why the apparent hits weren't real.

GPU time made it cheap to run the whole matrix, controls included, which is what made the artifact visible. The cost of the controls was a few more jobs in the queue, and they saved the project from chasing a number.

> **TODO:** Add where the project went next, once that's shareable.
