> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 18.4 — CLI Toolkit

## Goal

A small, real CLI tool with subcommands — the Go equivalent of Stage
0.3's `getopts`-based arg parsing, but for a language/ecosystem where
distributable single-binary CLI tools are extremely common in the
security tooling world (this is genuinely how a lot of the tools you'll
use in later stages are built and shipped).

## Requirements

1. At least 3 subcommands (e.g. reusing ideas from earlier projects —
   a `scan` subcommand wrapping 18.1's logic, a `serve` subcommand
   wrapping 18.2, etc. — or entirely new small utilities, your choice).
2. Proper CLI conventions: `-h`/`--help` at both the top level and
   per-subcommand, clear usage on invalid invocation, non-zero exit on
   error.
3. Compiles to a **single, dependency-free binary** (Go's default
   static-linking behavior) — demonstrate it running on a machine
   without your dev environment set up (or at least confirm via `ldd`/
   file-dependency check that it's statically linked).
4. Uses a real flag-parsing approach — either the standard library's
   `flag` package structured for subcommands, or a well-known library
   (`cobra`) if you want the more realistic experience of what most real
   Go CLIs use.

## Acceptance criteria

- [ ] Builds a single binary (`go build`), no external runtime deps
- [ ] Paste `-h` output at top level and for at least one subcommand
- [ ] Paste each subcommand actually working
- [ ] Invalid-invocation case pasted (bad subcommand/flag), showing
      clear error + non-zero exit
- [ ] Confirm static linking (e.g. `file` or `ldd` output on the binary)
- [ ] `git log` shows iteration

## Security relevance

Worth noticing explicitly: single-binary, statically-linked distribution
(Requirement 3) is *why* so much real security tooling ships this way —
a tool an analyst can copy onto an isolated VM or air-gapped box and run
immediately, with no dependency install step (and no matching increase
in that box's attack surface from a package manager reaching out to the
network), is operationally safer in exactly the contexts Stage 12's
isolated-analysis work cares about.

## When done

Point me at the source + `git log`. I'll check the subcommand structure
is genuinely modular (each subcommand's logic isolated, not one giant
switch statement with everything tangled together).
