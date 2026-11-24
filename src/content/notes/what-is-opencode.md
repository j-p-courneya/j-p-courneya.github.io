---
title: "What is OpenCode?"
date: 2026-04-08
description: "An open-source AI coding harness that lets you pick your own models, and why that matters for an AI budget."
draft: false
---

Have you heard of OpenCode? Depending on your platform, it shows up as a terminal UI (a TUI) or, as of April 2026, as a desktop app that's Mac-only for now. That suits me fine since I work on a MacBook Pro. The desktop app feels more like an IDE, with a file editor panel and a file explorer.

So what does it do? OpenCode is an AI harness: a tool that wraps a UI around a model, agentic resources, and access to your computer. That's a strange thing to experience at first. Going agentic means giving up a certain amount of control, even though you're clearly still the one swinging the hammer. That's a topic for another post.

Why not Claude Code, or OpenClaw? They're all harnesses, and grouping them together is fair. Choosing Claude means choosing to live in Anthropic's world, which is actually a pretty safe place to be. I think their ecosystem could make a solid enterprise option for academia, and the models are excellent.

The bigger question is model choice, and that comes with a price tag. OpenCode opens the gates to a whole catalog of models at prices that don't make you wonder whether your AI budget is out of control. My personal AI spending is currently close to $60 a month, which is why I'm taking a hard look at all of this. Paying for inference has quietly become a budget line, and I'm curious how far that creeps. Running state-of-the-art AI is expensive and we're pushing these systems hard, so what's an economically sensible arrangement? If you can settle on the options in OpenCode's catalog, or bring your own key (BYOK), you can land around $20 a month, which is the current Claude Pro price.

I've barely touched on the features, so here's an overview that isn't too verbose.

-----

## What OpenCode Actually Is

OpenCode is a free, open-source (MIT license) AI coding agent built for the terminal. It runs as a persistent background server and connects via a TUI — a terminal UI with panels, a sidebar, and session management. Sessions survive disconnects and SSH drops; you reconnect and pick up exactly where you left off.

### The Model Freedom Thing

This is OpenCode's defining characteristic. It supports 75+ model providers — Anthropic, OpenAI, Google Gemini, Mistral, local models via Ollama, and more. You bring your own API key (BYOK) for any of them. This is the core tradeoff: Claude Code locks you into Anthropic's ecosystem and bills you for every token. OpenCode lets you route to whatever model fits the task and your budget, or run entirely offline with a local model at zero cost.

OpenCode Zen is their curated tier — a handpicked set of models they've benchmarked specifically for coding agents, removing the guesswork about which provider performs reliably.

### How It Works

- **TUI mode** — terminal-native, keyboard-driven, works over SSH, runs anywhere
- **Desktop app** — Mac-only as of early 2026; feels closer to a lightweight IDE with a file explorer and editor panels
- **Agent system** — you can configure specialized agents with custom prompts, model assignments, and scoped tool access for specific workflows
- **MCP support** — implements the Model Context Protocol, letting the agent connect to external tools and services in a standardized way

### The Honest Tradeoff

Claude Code is more polished — better at multi-step planning, cleaner context handling, less babysitting required. OpenCode gets close, especially on end-to-end tasks, but the gap exists. What OpenCode gives you in return is provider independence, local model support for air-gapped or confidential codebases, and a cost structure you control. The tool itself is free. You pay only for the inference you actually use.

For a personal or research budget trying to stay under $20/month, that flexibility is the whole argument.
