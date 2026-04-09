---
title: "What is Opencode"
date: 2026-04-08
description: "Writing about open code"
draft: false
---

Have you heard about Open Code? Did I spell that right? it might be one word I'm not sure without going and checking. Well if you're still here then what is it? I would say depending on what computing platform you're on it may manifest as something inside your terminal. I think those are called TUI. or as of 20260408 a actual desktop application for Mac only no other platforms yet. That's good newa for me because I use a Mac book pro. As a Mac app it feels more like an IDE, file editor panel, file explorer... But wait what does it do? Well this is what's different at least as of now when this stuff is still new and we're all messing around playing with it while new tech churns it out. Well it's a AI Harness, open code is an AI Harness. A harness is a new kind of tool that wraps UI around a model, agentic resources, and interaction with your computing system. That is kind of a weird thing to experience. There's a certain amount of giving in, even though clearly you are the one wielding the hammer that goes on going agentic. That is another topic all together. Why not Claude code or what's the difference and why not open Claw?! well this is a conversation about open code so if I write about that I will speak about that then. But these are all harnesses I will say and glomming them together is not a mistake. If you choose Claude your saying I want to live in Anthropics world and that's actually pretty safe. I think their ecosystem could provide a solid academic enterprise solution and the models are pretty bad ass. I mean we haven't even talked about model selection and "freedom to choose a model". this comes at a price! But opencode really opens up the gates to a world of models and at price point that doesn't make you think is my AI budget getting out of control? currently in my personal life it's almost 60 bucks a month which is the reason why I'm giving all of this a real hard look at. I think it's interesting how now paying for inference access has become a budget item. and how much will that creep ? seriously. running SOTA AI CI is costly and we're pushing the systems hard. it's crazy but what's a economically sensible agreement? So if you can settle on the options available through open codes catalog or bring your own key - BYOK. you can land on a price point possibly around 20 bucks which is the current Claude Pro price. I have barely touched on the features but for that I will allow you to now follow along below with a beautiful overview that is not too verbose.

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
