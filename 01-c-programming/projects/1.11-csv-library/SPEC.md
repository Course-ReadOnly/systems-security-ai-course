> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.11 — CSV Library

## Goal

The last Stage 1 project, and the first framed explicitly as a
**library**, not a one-off program: a clean, reusable API for
reading/writing CSV that something else could link against, with a
small CLI demo on top proving it works. Direct rehearsal for structuring
C code across multiple files with a real header/implementation split —
prep for how every project from Stage 2 onward is organized.

## Requirements

1. Split into a library (`csv.h`/`csv.c`) and a separate demo CLI
   (`main.c`) that links against it — not one monolithic file.
2. Correctly handles the actually-hard parts of CSV: quoted fields
   containing commas, quoted fields containing embedded newlines, and
   escaped quotes (`""` inside a quoted field).
3. Provides both a reader (parse a CSV file into rows/fields) and a
   writer (given rows/fields, produce correctly-quoted CSV output).
4. Round-trip correctness: writing out a parsed file and re-parsing it
   must reproduce the same data.
5. No memory leaks. `Makefile` builds both the library and the demo.

## Acceptance criteria

- [ ] Builds cleanly (library + demo), `-Wall -Wextra` clean
- [ ] Paste a sample CSV with at least one quoted-comma field, one
      quoted-newline field, and one escaped-quote field, plus the
      parsed output showing all three handled correctly
- [ ] Round-trip test pasted: parse → write → parse again → diff against
      the original data, showing no loss
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log`. I'll check the header/implementation
split (is the public API actually clean, or are internals leaking
through the header) and the quoted-field edge cases specifically —
that's where nearly every CSV parser has a bug.
