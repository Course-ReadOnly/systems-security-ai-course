> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.9 — Text Editor

## Goal

First "hard" project — a real terminal text editor: raw-mode terminal
input, a screen buffer you render yourself, and file load/save. This
pulls together everything so far (file I/O, manual memory management,
string handling) plus new territory: terminal control and an explicit
program loop reacting to keypresses in real time.

## Requirements

1. Puts the terminal into raw mode (`termios`) so keypresses are read
   immediately, not line-buffered — and **restores the terminal on
   exit/crash**, including on `Ctrl-C` (a broken terminal on exit is an
   automatic fail here, it's happened to everyone who's skipped this).
2. Loads a file into an editable in-memory buffer, displays it, supports
   cursor movement (arrow keys), inserting/deleting characters, and
   saving back to disk.
3. Handles a file that doesn't exist yet (starts a new empty buffer,
   creates the file on save).
4. Quits cleanly on a defined key combo, restoring the terminal.
5. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Since this one's interactive and hard to paste as text: a short
      description + a `script`(1) session log or screen-recording-derived
      transcript showing open → edit → save → reopen, proving the save
      actually persisted the edit
- [ ] Confirm (explicitly test) the terminal is restored correctly after
      both a clean quit and a forced `Ctrl-C` — paste `stty -a` or similar
      before/after showing terminal settings are unchanged
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## Security relevance

Terminal emulators process escape sequences embedded in whatever content
they display — malicious files crafted to inject escape sequences into
a victim's terminal (moving the cursor, hiding text, even injecting fake
commands) are a real, if niche, vulnerability class. It's worth knowing
that displaying untrusted file content isn't automatically safe just
because it's "only text."

## When done

Point me at the source + `git log` plus your session transcript. I'll
check the raw-mode cleanup path hardest — an editor that leaves your
terminal broken on crash is the single most common failure mode here.
