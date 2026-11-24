---
title: "Building an MCP Server for Sequencing Metadata"
date: 2026-11-07
description: "Letting a language model search SRA and GEO through OmicIDX, alongside a catalog of our own lab's datasets."
draft: true
---

A surprising amount of bioinformatics time goes into finding data before anyone analyzes it. Is there a public dataset that matches this study design? Which of our own runs used that library prep? Where on the server did those reads end up? The answers are usually spread across SRA, GEO, and a lab's memory of what it has on disk.

I wanted a language model to be able to answer those questions directly, so I'm building an MCP server that does two things.

## Public metadata through OmicIDX

The first half searches public sequencing metadata from SRA and GEO through OmicIDX, which indexes those records and makes them queryable. Exposed as MCP tools, that lets a model search for studies, samples, and runs by organism, assay, or keyword, and come back with accessions a person can verify.

> **TODO:** List the tools the server exposes today (for example, study search, sample lookup, run lookup) and an example query that worked well.

## Our own data as dataset cards

The second half covers the lab's own data. Our server holds long- and short-read whole-genome sequencing and RNA-seq across several species, and most of it was only discoverable by asking the right person.

The approach is one YAML "dataset card" per dataset, with fields built on the same SRA and GEO metadata vocabulary. Using the public schema means a card for our own run and a record from SRA can be compared side by side, and it makes depositing data later much easier.

I started with the lab's datasets that are already deposited publicly, since their metadata already exists and can be checked against the official record. Cards are generated with help from an agent that reads what's on disk, but a person reviews every card before it goes in. That review step matters, because a confident wrong card is worse than no card.

## Why MCP

The Model Context Protocol gives the model a standard way to call tools, so the same server works in whatever client a person prefers. It also keeps the model honest: when it answers a data question, it's citing accessions and cards that came from a tool call, and you can check each one.

This server also feeds a larger idea I'm working on, a visual gallery of our datasets in the style of Sebastian Raschka's LLM Architecture Gallery, where each dataset gets a tile that helps people see what's available at a glance.

> **TODO:** Add the current status (prototype, in team use) and anything surprising you learned building it.
