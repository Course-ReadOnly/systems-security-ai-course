> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.8 — JSON Parser

## Goal

The hardest of the "medium" tier — a real recursive-descent parser for a
useful subset of JSON. This is the first project with genuine recursive
structure (objects/arrays can nest arbitrarily) and is direct rehearsal
for Stage 2's tree-shaped data structures.

## Requirements

1. Parses: objects `{}`, arrays `[]`, strings, numbers, booleans
   (`true`/`false`), and `null`. Nested objects/arrays must work to
   arbitrary depth (bounded only by memory/stack, not a hardcoded limit).
2. Represents the parsed result as an in-memory tree (a tagged union or
   similar — your design) that can be walked/queried after parsing.
3. Rejects malformed JSON with a clear error (and ideally a position/line
   indicator) rather than crashing or silently parsing garbage.
4. At minimum, a way to pretty-print the parsed structure back out, to
   prove the parse round-trips correctly.
5. No memory leaks, including on the malformed-input error path (freeing
   partially-built structures correctly is the hard part here).
6. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Paste output parsing a real nested JSON sample (at least 3 levels
      deep, mixing objects and arrays) and pretty-printing it back
- [ ] At least 2 malformed-input cases pasted, showing clear errors, not
      crashes
- [ ] `valgrind` output pasted for **both** a successful parse and a
      malformed-input case — the error path leaking memory is the most
      common bug in parsers like this
- [ ] `git log` shows iteration

## Security relevance

Recursive-descent parsers have a real, recurring CVE history: deeply
nested input causing stack-overflow crashes (a denial-of-service, and
sometimes worse) is a documented bug class across production JSON/XML
parsers, not a hypothetical. Consider (as a stretch, not required) what
your parser does with input nested a few thousand levels deep — that
experiment is exactly what Stage 13.2's fuzzer would eventually try
against it automatically.

## When done

Point me at the source + `git log`. I'll check the malformed-input error
path's memory handling first — that's where this project usually breaks.
