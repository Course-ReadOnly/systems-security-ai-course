> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.4 — Text Statistics Tool

## Goal

A `wc`-like tool, but doing more than `wc` — forces real string handling
in C (no built-in string class, everything is a `char*` and manual
bookkeeping) plus reading input from either a file argument or stdin,
the standard Unix tool convention.

## Requirements

1. `./textstats <file>` or `./textstats < input`  — must support both a
   file argument and stdin (so it composes in a pipeline).
2. Reports at minimum: line count, word count, character count, longest
   line (length + the line itself), and average word length.
3. Correctly handles: empty file, a file with no trailing newline, lines
   with multiple consecutive spaces (word count shouldn't overcount).
4. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Output pasted against a real text file (a few paragraphs), and
      cross-checked against `wc` for line/word/char count agreement
- [ ] Empty-file and no-trailing-newline edge cases pasted
- [ ] Piped input case pasted (`cat file | ./textstats`)
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log`. I'll check the word-counting logic
against multiple-space/tab edge cases specifically, since that's where
naive implementations usually break.
