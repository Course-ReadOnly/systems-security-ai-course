> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 16.2 — EEPROM Programmer

## Goal

Build (or use, if pre-built hardware is what you have access to) an
EEPROM programmer to write microcode/lookup tables for your 16.1
breadboard CPU — turning an idea ("this instruction should do X") into
bits burned onto a chip your CPU actually reads.

## Requirements

1. A way to write arbitrary byte data to an EEPROM chip (e.g. an
   Arduino-based programmer, following the common Ben Eater-style
   approach, or a commercial programmer if that's what's accessible —
   either is fine, document which).
2. Verify written data by reading it back and confirming it matches
   what was written (write-then-verify, not just "the write command
   didn't error").
3. Use it for a real purpose: program a lookup table or microcode ROM
   that your 16.1 CPU actually uses (e.g. a 7-segment display decoder
   table, or instruction microcode).
4. Document the EEPROM's addressing/timing requirements you had to
   respect (write cycle timing, address setup) — getting this wrong is
   the most common source of "sometimes works" EEPROM programmers.

## Acceptance criteria

- [ ] Working programmer, demonstrated writing and reading back known
      test data correctly
- [ ] Real use case: an EEPROM programmed with actual data used by your
      16.1 CPU (or another real application if 16.1 wasn't done),
      confirmed working in that context
- [ ] Write-then-verify evidence pasted/described for at least one real
      programming session
- [ ] `git log` (for programmer source code) shows iteration

## When done

Point me at the source + `git log` and your verification evidence. I'll
check the write-then-verify discipline specifically — silently trusting
a write without reading back is how subtly-wrong EEPROM contents cause
confusing downstream bugs in the CPU that reads them.
