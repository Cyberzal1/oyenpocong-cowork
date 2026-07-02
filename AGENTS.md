# AGENTS.md

## Architecture
This is a static, dependency-free single-page site: everything (markup, CSS, JS) lives in `index.html`. There is no bundler, framework, or build step. It is deployed to Netlify as a static site.

## Key files
- `index.html` — the whole page: 9 `<section class="panel">` slides forming a scroll-snap deck, an SVG-based mascot rendered from `<template>` elements, a scroll-progress rail/counter, and a fixed music player widget at the bottom-left.
- `assets/background-music.mp3` — looping background audio used by the music player.

## Conventions
- Styling is done via CSS custom properties defined in `:root` (colors, fonts) — reuse these tokens rather than hardcoding new colors.
- Each slide section follows the same header pattern: a `.brandmark` link (points to the author's Threads profile), a numbered `.badge`, then an eyebrow/heading/rule.
- Scroll-reveal animations use the `.reveal` class + `IntersectionObserver`; respect `prefers-reduced-motion`.
- The music player (`#bg-music` audio element + `.music-player` controls) is self-contained in an IIFE near the end of the body — play/pause, volume slider, and mute button all sync to the audio element's state.

## Non-obvious decisions
- The mascot poses (`calm`, `point`, `think`) are stored as `<template>` tags and cloned into `.mascot[data-pose]` placeholders on `DOMContentLoaded`, to avoid duplicating the SVG markup per instance.
- Background music autoplay is intentionally NOT triggered on load (browsers block unmuted autoplay) — the user must press play.
