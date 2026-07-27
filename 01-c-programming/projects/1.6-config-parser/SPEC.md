> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.6 — Config Parser

## Goal

Parse a simple flat `key=value` config file into an in-memory structure
you can query by key. This is the first project requiring you to design
your own data structure (an array or linked list of key/value pairs) and
manage its memory explicitly — direct prep for Stage 2.

## Requirements

1. Parses a file of lines like `key=value`, one per line.
2. Supports comments (lines starting with `#`) and blank lines — both
   skipped, not treated as malformed entries.
3. Handles whitespace around `=` sensibly (`key = value` and `key=value`
   both work the same).
4. Exposes a lookup function: given a key, return its value (or a clear
   "not found" signal — don't return garbage or crash on a missing key).
5. All memory allocated for parsed entries is freed before exit — no
   leaks.
6. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Paste a sample config file and program output showing several keys
      correctly looked up, including one lookup for a key that doesn't
      exist (handled cleanly)
- [ ] Comment lines and blank lines confirmed skipped, not misparsed
- [ ] `valgrind` output pasted showing zero leaks (this is the real test
      of whether your free logic is correct, not just present)
- [ ] `git log` shows iteration

## Security relevance

Any parser is an attack surface the moment its input can come from
somewhere untrusted — "parser confusion" (a parser disagreeing with
whatever *reads its output later* about what a malformed line means) is
a real, named bug class. Stage 13.2's fuzzer will eventually try to
break exactly this kind of code; writing it carefully now is the
counterpart to breaking it later.

## When done

Point me at the source + `git log`. Memory ownership is what I'll check
hardest here — who allocates each string, who's responsible for freeing
it, and whether that's actually consistent.
