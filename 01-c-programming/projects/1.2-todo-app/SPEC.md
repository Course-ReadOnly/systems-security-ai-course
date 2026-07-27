> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.2 — Todo App

## Goal

A persistent CLI todo list — first real exposure to C file I/O
(`fopen`/`fread`/`fwrite`/`fclose` or the `open`/`read`/`write` syscalls)
and to a program that has state surviving between runs, not just one-shot
computation like the calculator.

## Requirements

1. Subcommands: `add "task text"`, `list`, `done <n>`, `remove <n>`.
2. Tasks persist to a file on disk between runs (plain text or a simple
   binary format — your call, but document the format in the README).
3. `list` shows task number, done/not-done status, and text.
4. Handles a missing/empty todo file gracefully on first run (creates it,
   doesn't crash).
5. `Makefile` (`make` / `make clean`).

## Acceptance criteria

- [ ] Builds cleanly with `make`, `-Wall -Wextra` clean
- [ ] Paste a full session: add a few tasks, list them, mark one done,
      remove one, list again — showing state actually persists across
      separate invocations of the program
- [ ] First-run-with-no-file case pasted, showing it doesn't crash
- [ ] `valgrind` run pasted, no leaks
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log`. I'll check the file I/O error
handling (what happens if the file is corrupt/unreadable) and whether
task numbering stays consistent after a `remove`.
