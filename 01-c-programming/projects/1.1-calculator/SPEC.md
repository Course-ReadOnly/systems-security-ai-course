> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.1 — Calculator

## Goal

First real C program. Read an arithmetic expression, evaluate it, print
the result — the smallest project that still forces you through
`argv`/stdin parsing, basic control flow, and real error handling
(the C way: return codes and checked input, no exceptions).

## Requirements

1. Accepts an expression either as command-line arguments
   (`./calc 3 + 4`) or interactively from stdin — pick one and be
   consistent.
2. Supports `+ - * /` on integers or doubles (your choice, but handle it
   correctly — no silent integer truncation if you claim float support).
3. Handles bad input without crashing: division by zero, malformed
   expressions, non-numeric tokens — print a clear error, don't segfault
   or silently print garbage.
4. Compiled with a `Makefile` (`make` builds it, `make clean` removes
   build artifacts).

## Acceptance criteria

- [ ] Builds cleanly with `make`, no warnings with `-Wall -Wextra`
- [ ] Correct output pasted for at least: one of each operator, a
      division-by-zero case, and one malformed-input case
- [ ] Compiled and run under `valgrind` at least once — paste output
      showing no memory errors/leaks
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log`. "Review my code" for a real review —
error handling and `-Wall -Wextra` cleanliness are what I'll check first.
