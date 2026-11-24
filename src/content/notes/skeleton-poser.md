---
title: "Skeleton Poser: Building a Tool for My Own Shirt Designs"
date: 2026-11-24
description: "A Three.js app for posing 3D skeletons and exporting clean art for screen printing."
draft: true
---

Outside of work I design and screen print shirts. The designs run toward psychedelia and mysticism, and skeletons show up constantly, somewhere in the lineage of Grateful Dead poster art.

Drawing a skeleton in a specific pose is the slow part. I can do the rendering and composition in Adobe, but getting the anatomy right in an unusual pose means hunting for reference every time. So I built [Skeleton Poser](https://github.com/j-p-courneya/skeleton-poser), a browser app that lets me pose a 3D skeleton and export the result as clean line art to build a design around.

## Why Three.js

I wanted it to run anywhere: Mac, Windows, or just a browser tab. Three.js meant one codebase for all of those, no install, and a straightforward path to hosting it on GitHub Pages so anyone with the link can use it.

## Design decisions

- **Posing** is a mix of free manipulation and preset positions. Presets cover the poses I reach for repeatedly; free posing handles everything else.
- **Clean art only.** The app exports the drawing, not color separations. Separations are a printing decision I'd rather make in Adobe with the full design in front of me.
- **Multiple skeletons and props** are on the list, not in it yet.

> **TODO:** Add what the export actually produces (SVG, PNG, line weights) and how it drops into your Adobe workflow.

## What it's like building for yourself

The requirements conversation is short and the feedback loop is immediate: I use the first working version on a real design and find out within an hour what's missing. The repo is public, so if posing a skeleton in a browser is useful to you, help yourself.

> **TODO:** Add a screenshot or an example shirt design made with it.
