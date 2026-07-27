> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.10 — Terminal UI

## Goal

Builds on 1.9's raw-terminal-mode groundwork toward a small reusable
TUI (text user interface): drawing boxes/menus and handling navigation,
the same rendering-loop shape used by real tools like `htop`/`vim`'s
status bar, without pulling in a library like ncurses (do it raw, that's
the point of this stage).

## Requirements

1. Raw-mode terminal input/output (reuse or build on 1.9's approach).
2. Renders at least: a bordered box, and a selectable menu (arrow
   keys move a highlighted selection, Enter selects).
3. Handles terminal resize gracefully — or explicitly documents that it
   doesn't and why, rather than silently rendering garbage on resize.
4. A concrete demo app using it (e.g. a simple file browser listing a
   directory, navigable with arrows) — not just an unused library.
5. Cleans up terminal state on exit, same discipline as 1.9.
6. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Session transcript (same approach as 1.9) showing the demo app's
      navigation actually working
- [ ] Terminal-restore-on-exit confirmed, including forced `Ctrl-C`
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## Security relevance

Same escape-sequence caution as 1.9, plus a resource-cleanup angle: a
TUI tool that doesn't restore terminal state reliably on every exit path
(including signals) is the same category of bug as a security tool
(think Stage 9's port scanner or Stage 13's fuzzer) that leaves a system
in a bad state after a crash — cleanup-on-every-path is a habit, not a
one-off fix.

## When done

Point me at the source + `git log` plus your session transcript. I'll
check whether the rendering logic redraws efficiently (full-screen
flicker on every keypress is a common early mistake) and reuses 1.9's
terminal-handling rather than duplicating it.
