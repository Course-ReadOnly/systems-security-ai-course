> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 6.2 — Custom DLL (Build + Load)

## Goal

Build your own DLL and load it dynamically via `LoadLibrary` — understand
imports/exports from the *authoring* side before Stage 11/12 has you
reading them from the reversing side in a disassembler. Understanding
how a DLL's export table actually works is what makes tools like Ghidra's
import/export views meaningful later, rather than just names on a screen.

## Requirements

1. A DLL exporting at least two functions (via `__declspec(dllexport)`
   or a `.def` file — try both across two functions if you want the
   comparison).
2. A separate executable that loads the DLL **dynamically** at runtime
   via `LoadLibrary`/`GetProcAddress` (not load-time linking against a
   `.lib` — dynamic loading is the point, since that's what malware/
   plugin systems actually do).
3. Correctly handles a missing DLL or missing exported function (checks
   return values of `LoadLibrary`/`GetProcAddress`, doesn't just call
   through a null pointer).
4. Uses `dumpbin /exports` (or equivalent) to inspect your own DLL's
   export table and confirm it matches what you expect.
5. Correctly calls `FreeLibrary` when done.

## Acceptance criteria

- [ ] DLL builds, exports confirmed via `dumpbin /exports` (paste the
      output)
- [ ] Host executable successfully loads the DLL and calls both exported
      functions — paste output
- [ ] Missing-function case tested (request a function name that doesn't
      exist) — handled cleanly, not a crash
- [ ] `git log` shows iteration
- [ ] README explaining the difference between what you did here
      (dynamic loading) and static/load-time linking, in your own words

## When done

Point me at the source + `git log` plus the `dumpbin` output. I'll check
that the export table actually matches the code (no mismatched
name-mangling issues) and that every `LoadLibrary`/`GetProcAddress`
return value is actually checked before use.
