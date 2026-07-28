> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 7.2 — ELF Loader

## Goal

Parse a real ELF binary's headers and (at minimum) understand/print
enough of its structure to reason about how the OS would actually load
and run it. This is deliberately scoped as **parsing/understanding**, not
a full competing implementation of `execve` — a genuine loader is a much
bigger undertaking; this is direct prep for Stage 11's "write an ELF
parser" project, which goes further.

## Requirements

1. Parses the ELF header of a real binary: magic number/class (32/64-bit),
   entry point address, program header table location/count, section
   header table location/count.
2. Parses and prints the **program headers** (the `PT_LOAD` segments
   specifically — these are what actually gets mapped into memory at
   load time): virtual address, file offset, size, permissions.
3. Correctly handles both 32-bit and 64-bit ELF (or explicitly documents
   supporting only one, with why).
4. Rejects non-ELF files cleanly (checks the magic bytes first, doesn't
   assume every input file is well-formed).

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Paste output parsing a **real binary on your system** (e.g. `/bin/ls`
      or your own compiled program), and cross-check the `PT_LOAD`
      segments you printed against `readelf -l` on the same file —
      they must agree
- [ ] Non-ELF file tested (e.g. a text file), rejected cleanly rather
      than misparsed
- [ ] `git log` shows iteration
- [ ] README explaining, in your own words, what a `PT_LOAD` segment
      actually is and why it's the part that matters for loading

## Security relevance

ELF-parsing code is a real attack surface in its own right — a
malformed or adversarially-crafted binary handed to a loader, a
disassembler, or an AV/EDR product's static-analysis engine is exactly
the kind of untrusted input a parser-confusion bug lives in (see
`SECURITY-CONCEPTS.md`'s "Injection" and general parser-hardening
themes). Requirement 4's "reject non-ELF files cleanly" is the same
discipline as any other untrusted-input parser in this course — the
difference here is that real tools built on exactly this logic (Stage
11's parser, and eventually disassemblers/loaders generally) get fed
files by people actively trying to break them.

## When done

Point me at the source + `git log` plus the `readelf -l` comparison —
that comparison is the actual proof of correctness here, not just "it
printed something that looks plausible."
