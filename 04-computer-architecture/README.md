> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 4 — Computer Architecture

**Time budget:** 4–6 weeks part-time / 2 weeks full-time

## Objectives

Understand what's actually happening below the C you've been writing —
registers, the fetch/decode/execute cycle, memory, and how a CPU is built
from logic gates up. This demystifies everything from here on: Stage 7
(Assembly) is what you write once you understand what a CPU project here
executes, and Stage 8 (OS) assumes this mental model already exists.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Full course | [Berkeley CS61C](https://cs61c.org/) |
| 02 | Hardware-up, hands-on | [Ben Eater — 8-bit computer (YouTube)](https://www.youtube.com/c/BenEater) |
| 03 | Build a CPU from NAND gates | [NAND2Tetris](https://www.nand2tetris.org/) |

**Topics:** binary, logic gates, CPU, registers, ALU, pipelines, cache,
memory, interrupts, MMU.

## Projects

| # | Project | Folder |
|---|---|---|
| 4.1 | CPU simulator | `projects/4.1-cpu-simulator/` |
| 4.2 | CHIP-8 emulator | `projects/4.2-chip8-emulator/` |
| 4.3 | Simple assembler | `projects/4.3-simple-assembler/` |

Suggested order: 4.1 → 4.3 → 4.2 — build a simulator for your own toy
instruction set, then an assembler that targets it, before tackling
CHIP-8 (a real, pre-existing spec with a much bigger opcode set).
