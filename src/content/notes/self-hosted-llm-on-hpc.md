---
title: "Running a Self-Hosted LLM on an Academic SLURM Cluster"
date: 2026-11-22
description: "What it took to serve a language model, embeddings, and retrieval for my group on shared V100 nodes."
draft: true
---

Our group runs most of its work on the institute's SLURM cluster, and a lot of that work now involves language models: coding help, pulling structured fields out of messy text, and searching our own documentation. Sending all of that to a commercial API raises cost and data questions, so I set out to build a stack we could run ourselves on hardware we already had access to.

The plan has three components. The first is an inference endpoint that serves a model over an OpenAI-compatible API. The second is retrieval (RAG) over our own documents, using a local embedding model. The third is a set of MCP servers that let a model reach the tools and data we care about.

## Component 1: inference on V100s

The GPU node I have access to has eight V100-SXM2 cards with 32 GB each. They're excellent cards, but they're Volta (compute capability sm_70), and that matters more than I expected. Much of the current serving software assumes newer architectures, so I pinned vLLM to v0.6.3, the last release line that still worked cleanly on sm_70, and started with Qwen2.5-7B-Instruct as an interim model.

I also ran a larger 27B model as a quantized GGUF through the llama.cpp CUDA server inside an Apptainer container, and got about 34 tokens per second. That's fast enough to use as a coding assistant, and I configured it as a bring-your-own-key endpoint for VS Code Copilot.

> **TODO:** Add a sentence on which serving path you're standardizing on (vLLM or llama.cpp) and why.

## Living on a shared cluster

The node is shared, so I can't treat the GPUs as mine. Everything runs through SLURM allocations, and the design has to assume other people's jobs are on the same machine. A few practical lessons came out of that:

- Interactive development happens on a login host that can't submit jobs, so the workflow is an interactive `srun` session for anything that touches a GPU.
- Home directories are capped at 10 GB, and mine filled up quickly with tooling caches. Model weights, containers, and code all live on project and scratch storage instead, and I keep subfolders tidy so nothing lands loose in the scratch root.
- Containers (Apptainer) make the CUDA stack reproducible without asking the admins to install anything.

## Component 2: retrieval

For embeddings I staged BGE-large-en-v1.5, which runs comfortably alongside the inference model. The first target corpus is our own documentation and runbooks, so new team members can ask questions and get answers grounded in how we actually do things.

> **TODO:** Fill in what's indexed so far and how retrieval quality looks.

## Where it's going

The goal is a shared endpoint the whole team can use for mixed workloads: interactive coding, batch extraction jobs, and team RAG. Right now my priority is the answer-quality ceiling on this hardware, which is why I'm also looking at the H100s I have access to through the national ACES allocation for larger models and possibly some training work.

I've written the whole setup up as a runbook. If you're trying to do something similar on older GPUs in an academic environment, I'm happy to compare notes.
