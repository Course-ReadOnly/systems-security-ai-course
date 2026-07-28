> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.7 — INI Parser

## Goal

A step up from 1.6: real INI format, with `[section]` headers grouping
keys. Forces a two-level data structure (sections, each containing its
own key/value pairs) instead of one flat list — the natural next step in
data-structure complexity before Stage 2 formalizes this.

A sample input file is provided at `samples/example.ini` (implicit
global section, both comment styles, and a duplicate `[server]` header
already included) — use it to get started, but write your own
edge-case files too as you find gaps.

## Requirements

1. Parses INI-format files: `[section]` headers, `key=value` lines
   underneath each, comments (`;` or `#`), blank lines.
2. Keys before the first `[section]` header belong to an implicit
   "global"/unnamed section — decide how you represent that and document
   it.
3. Lookup function takes both a section name and a key, returns the
   value (or a clear not-found signal).
4. Correctly handles duplicate section headers appearing twice in the
   same file (merge, or last-wins — your call, but be consistent and
   document it).
5. No memory leaks. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Sample multi-section INI file + program output pasted, showing
      correct section-scoped lookups (same key name in two different
      sections resolving to different values)
- [ ] Global/pre-section keys case pasted
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## Security relevance

Same theme as 1.6, one layer deeper: a scoping bug here (a key
"leaking" between sections) is structurally the same mistake as an
access-control bug that lets data meant for one context bleed into
another — a pattern that recurs seriously in Stage 13's web-exploitation
labs (access control is one of PortSwigger's core vulnerability
categories).

## When done

Point me at the source + `git log`. I'll check that section-scoping is
actually enforced (a key in section A shouldn't leak into a lookup
against section B) and the memory-ownership story for the two-level
structure.
