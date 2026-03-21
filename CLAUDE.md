# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file HTML5 canvas game ("Jeep Mountain Run") — a side-scrolling obstacle avoidance game. No build tools, no dependencies, no tests. Everything lives in `index.html` (HTML + CSS + vanilla JS).

## Development

Open `index.html` directly in a browser. No server needed.

```
open index.html
```

## Architecture

The game uses a single `<canvas>` element with a `requestAnimationFrame` loop. Key sections in the JS:

- **Game state machine**: `STATE.MENU → STATE.PLAYING → STATE.GAMEOVER`, controlled by `state` variable
- **Jeep physics**: lane-based movement (3 lanes) with gravity-based jumping. Properties on the `jeep` object
- **Obstacle system**: `OBSTACLE_TYPES` defines all obstacle types with `minLevel` for progressive difficulty. `spawnObstacle()` picks from available types based on current level
- **Parallax rendering**: 2 mountain layers, clouds, and trees scroll at different speeds via `updateParallax()`
- **Collision detection**: AABB-based in `checkCollisions()`. Full-width obstacles (water, mud, ice, gap) apply surface effects; discrete obstacles (rocks, logs) deal damage
- **Difficulty progression**: every 500m increases level (up to 10), which unlocks harder obstacles and raises `baseSpeed`
