# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the game

Open `index.html` directly in a browser — no build step, no server required:

```
open index.html
```

## Architecture

The entire app lives in a single file: `index.html`. It is structured in three sections:

1. **CSS** (`<style>`) — all styling inline in the `<head>`. Color palette: dark navy background (`#1a1a2e`, `#16213e`, `#0f3460`), red for X (`#e94560`), teal for O (`#a8dadc`).

2. **HTML** (`<body>`) — static 3×3 grid of `.cell` divs with `data-i` attributes (0–8) as the only board representation in the DOM. Score display and a single "New Game" button.

3. **JavaScript** (`<script>`) — no framework, no modules. Three mutable globals drive all state:
   - `board`: `Array(9)` of `null | 'X' | 'O'`
   - `current`: `'X' | 'O'` — whose turn it is
   - `gameOver`: boolean
   - `scores`: `{ X, O, D }` — persists across rounds (not reset by `init()`)

   Key functions:
   - `init()` — resets board/turn/gameOver, preserves scores, calls `render()`
   - `render()` — single source of truth; rewrites all cell classes/text and score DOM from state
   - `checkWin(player)` — checks `player` against the hardcoded `WINS` array of 8 winning index combos
   - `handleClick(e)` — delegated to `#board`; updates state then calls `render()`, then checks win/draw

## Git workflow

This repo is pushed to GitHub at `https://github.com/MeganToday/tic-tac-toe`.

**Commit and push after every meaningful unit of work** — do not batch multiple unrelated changes into one commit, and do not leave work uncommitted at the end of a session. This ensures we can always revert to a known-good state and never lose progress.

Commit messages must be clear and specific about what changed and why:

```
git add index.html
git commit -m "short description of what changed and why"
git push
```

Examples of good commit messages:
- `Add AI opponent with minimax algorithm`
- `Fix win detection not highlighting diagonal combos`
- `Style score panel with player colors`

After completing any feature, bug fix, or meaningful improvement — commit and push immediately before moving on to the next task.
