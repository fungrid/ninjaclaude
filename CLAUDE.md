# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Ninja Duo Run — a browser-based endless runner game where the player controls two ninjas simultaneously. Red ninja (front) jumps with Right Arrow, Blue ninja (back) jumps with Left Arrow. Touch/click supported via left/right screen halves. Hosted on GitHub Pages.

## Architecture

The entire game is a single `index.html` file (~500 lines) with inline CSS and JavaScript using the HTML5 Canvas API. No build step, no dependencies, no frameworks.

Key classes and systems in the `<script>` block:
- **Ninja** — Player character with physics (gravity, double jump), death state, and sprite drawing. Two instances: `redNinja` (x=200) and `blueNinja` (x=80).
- **Obstacle** — Two types: `block` (red spike pillars to jump over) and `gap` (holes in the ground to jump across). Some blocks are `tall`, requiring double jump.
- **World scrolling** — Obstacles exist in world-space coordinates. `worldScroll` increases each frame; `obstacle.screenX()` converts to screen position. Ninjas stay at fixed screen X positions.
- **Game loop** — `requestAnimationFrame`-based loop: `update()` handles physics/collisions/spawning, `draw()` renders background/ground/obstacles/ninjas.
- **Ground rendering** — `drawGround()` dynamically cuts gap holes out of the ground surface.

## Development

Open `index.html` directly in a browser. No server required. To preview:
```
open index.html
```

There are no tests, linters, or build commands. All changes are made directly to `index.html`.

## Game Constants

Tunable values at the top of the script: `GRAVITY`, `JUMP_FORCE`, `BASE_SPEED`, `GROUND_Y`, `NINJA_SIZE`, `MIN_OBSTACLE_GAP`, `MAX_OBSTACLE_GAP`. Speed increases with distance via `BASE_SPEED + distance * 0.0003`.
