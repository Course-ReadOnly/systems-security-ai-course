> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 11.2 — ELF Parser

## Goal

Go further than Stage 7's ELF loader: parse section headers, the symbol
table, and dynamic-linking information — the parts of an ELF file that
matter for *reverse engineering* a binary rather than just loading it.
This is the same category of tool Ghidra/`readelf` provide, built by hand.

## Requirements

1. Parses everything Stage 7's project did (ELF header, program
   headers) **plus**: section headers (`.text`, `.data`, `.bss`, etc.),
   the symbol table (`.symtab`/`.dynsym`), and the dynamic section
   (`DT_NEEDED` entries — which shared libraries this binary depends on).
2. Resolves and prints symbol names (not just raw offsets into the
   string table — actually dereference `.strtab`/`.dynstr`).
3. Handles stripped binaries gracefully (no symbol table present) —
   reports that clearly rather than crashing.
4. Correctly distinguishes statically-linked vs. dynamically-linked
   binaries.

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] Paste output against a real, non-trivial binary (not a "hello
      world" — something with actual library dependencies), cross-
      checked section-by-section against `readelf -S`, symbol-by-symbol
      against `readelf -s`, and dependencies against `readelf -d` /
      `ldd`
- [ ] A stripped binary tested, handled cleanly
- [ ] `git log` shows iteration
- [ ] README explaining what each section type parsed actually
      represents, in your own words

## Security relevance

Symbol tables and dynamic-linking metadata are exactly what a real RE
workflow reads first to understand a binary's capabilities before
diving into disassembly — imported/dynamic symbols name the exact
outside-world interactions (network, file, process) a binary can
perform. Requirement 3 (handling stripped binaries) matters because
real malware is routinely stripped specifically to defeat this kind of
easy triage — a parser that crashes instead of clearly reporting "no
symbol table" is itself a small analysis-tooling failure.

## When done

Point me at the source + `git log` and the `readelf` cross-checks —
those comparisons are the real correctness proof. I'll check symbol-
table string resolution specifically, since an off-by-one there produces
plausible-looking but wrong names.
