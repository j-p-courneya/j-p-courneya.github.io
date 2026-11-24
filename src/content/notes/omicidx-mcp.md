---
title: "An MCP Server for Sequencing Metadata"
date: 2026-11-24
description: "Letting a language model search public SRA and GEO metadata and our lab's own datasets through one set of tools."
draft: true
---

<!-- TODO: add the tool names your server exposes and one real example query and result. -->

A surprising amount of bioinformatics time goes into finding data. Someone asks whether there's public RNA-seq for a given parasite stage, or whether we already have long-read WGS for a species on our server, and the answer involves a mix of SRA searches, GEO pages, and asking around the lab. I wanted to be able to ask that question once, in plain language, and get an answer that covers both places.

## Two sources, one interface

The server I'm building speaks the Model Context Protocol (MCP), so any MCP-capable client (Claude, an IDE agent, or the self-hosted model on our cluster) can call it as a tool.

It searches two things:

1. **Public metadata through OmicIDX.** OmicIDX keeps SRA and GEO metadata in a form that's far easier to query than the raw NCBI interfaces. The MCP server wraps those queries so the model can filter by organism, assay, platform, and study.
2. **Our lab's own datasets.** These come from a dataset catalog I'm building, where every dataset on our server gets a small YAML "card," one file per dataset. The card fields follow SRA and GEO metadata conventions on purpose, so a public study and one of ours can be described the same way and returned side by side.

## Why YAML cards

I wanted the lab's catalog to be something people can read and edit without a database. A YAML file per dataset is easy to review in a pull request, easy to validate, and easy for an agent to draft from what's already on disk, with a person checking it before it's merged. I'm starting with the datasets we've already deposited publicly, since their metadata is already clean.

## What I've learned building it

- Tool descriptions matter as much as the code. The model decides which tool to call from the description, so vague descriptions lead to wrong calls.
- Return less. A search that returns 500 runs overwhelms the model's context; summarizing to studies first, with a way to drill into runs, works much better.
- Keep the public and private sources in separate tools. It makes it obvious in every answer where a dataset came from.

The repo is private for now while the lab catalog fills in.
