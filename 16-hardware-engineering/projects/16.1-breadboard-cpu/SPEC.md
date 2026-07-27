> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 16.1 — Breadboard CPU

## Goal

Build a minimal CPU from discrete 74-series logic ICs on a breadboard —
Ben Eater's classic project, and the physical-hardware version of Stage
4's simulated CPU. Nothing here is simulated; every register, every
clock edge is real voltage on a real wire.

## Requirements

1. A functioning CPU built from 74-series logic chips (following the
   NAND2Tetris/Ben Eater style build — you're not expected to design the
   architecture from scratch, but you must build and understand it, not
   just follow steps blindly).
2. At minimum: a clock, a program counter, a small register set, an ALU
   capable of addition, and simple instruction decoding.
3. Can load and run a small hand-assembled program (even a few
   instructions — e.g. counting up and displaying a value on LEDs).
4. Understand and be able to explain every module's role — this gets
   verified in review by explanation, not just a working build.

## Acceptance criteria

- [ ] Photo/video evidence of the working breadboard build
- [ ] A real program run on it, with observable output (e.g. LEDs
      showing a counting sequence), described or recorded
- [ ] Written explanation, in your own words, of each module (clock,
      PC, registers, ALU, decoder) and how data flows between them on
      each clock cycle
- [ ] `git log` (for any documentation/schematics/microcode you wrote)
      shows iteration

## When done

Point me at your documentation + `git log` and the photo/video evidence.
Since I can't inspect a physical breadboard directly, this review leans
heavily on your written explanation actually demonstrating understanding
— I'll ask follow-up questions about specific signal timing/data flow to
check it's real, not memorized.
