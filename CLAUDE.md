# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A small collection of standalone, single-file interactive web toys, each living in its own subfolder. There is no build system, package manager, or test suite — every project is a self-contained `index.html` with inline CSS and JavaScript that runs directly in a browser.

## Running a project

Open the relevant `index.html` directly in a browser, e.g.:

```
open focus-sprint/index.html
```

No build, install, or server step is required.

## Architecture notes

- **focus-sprint/** — A Pomodoro-style focus timer. Everything (markup, styles, logic) lives in `focus-sprint/index.html`:
  - The countdown ring is drawn manually on a `<canvas>` each tick (`drawRing`/`updateDisplay`) rather than via CSS animations.
  - Completion chimes are synthesized at runtime with the Web Audio API (`playChime`) — no audio assets.
  - Streak/completion stats persist across sessions via `localStorage` under the `focusSprintData` key, with day-over-day streak logic in `recordCompletion`.
  - Mode switching (focus / short break / long break) just swaps `totalSeconds` and resets the timer; it's driven by `data-minutes`/`data-mode` attributes on the mode buttons.

When adding new toys, follow the same pattern: one self-contained `index.html` per subfolder, no external dependencies, state persisted via `localStorage` if it needs to survive reloads.
