> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.5 — Hex Editor

## Goal

First "medium" project — read a binary file and display it the way
`xxd`/`hexdump` do (hex bytes + ASCII side by side), then support
editing a single byte and writing the change back. This is direct prep
for Stage 7 (Assembly) and Stage 11 (Reverse Engineering), where reading
raw bytes is a daily activity.

## Requirements

1. `./hexed <file>` — displays the file's contents: offset, hex bytes
   (16 per row is conventional), and the printable-ASCII representation
   of the same bytes (non-printable shown as `.`).
2. Support editing: given a byte offset and a new hex value, write that
   single byte back to the file without corrupting anything else in it.
3. Handles files that aren't a clean multiple of 16 bytes (partial last
   row) correctly — don't crash or misalign the display.
4. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Output pasted against a real binary file (a small `.png` or
      compiled binary works well), formatting compared against real
      `xxd` output for the same file
- [ ] Byte-edit demonstrated: paste before/after hex dump plus a `cmp`/
      `diff` confirming only the intended byte changed
- [ ] Non-multiple-of-16 file size tested and pasted
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log`. I'll check the edit path specifically
— that writing one byte can't accidentally truncate or corrupt the rest
of the file.
