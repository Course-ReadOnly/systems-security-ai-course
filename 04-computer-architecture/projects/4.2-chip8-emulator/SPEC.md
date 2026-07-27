> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 4.2 — CHIP-8 Emulator

## Goal

A real, pre-existing, well-documented instruction set (unlike 4.1's
toy ISA) — CHIP-8 is the traditional "first emulator" for a reason: small
enough to finish, real enough to run actual games. Builds directly on
4.1's fetch/decode/execute structure at a larger scale.

## Requirements

1. Implements the CHIP-8 spec: 16 registers, a 4KB memory space, the
   stack, delay/sound timers, and the ~35 opcodes.
2. Loads a real CHIP-8 ROM (public-domain test ROMs and simple games
   exist) and executes it correctly.
3. Renders the 64×32 monochrome display — a terminal-based
   character-grid renderer is enough, doesn't need to be graphical.
4. Handles the 16-key hex keypad input (map to a real keyboard subset).
5. Timers (delay/sound) decrement correctly at 60Hz — get this wrong and
   games run at the wrong speed.

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] A public-domain CHIP-8 test ROM (e.g. an opcode test ROM) run
      successfully — paste output/confirmation of which opcodes passed
- [ ] A real simple game ROM (e.g. Pong or similar) actually playable —
      screen-recording-derived transcript or detailed description of a
      session proving it works
- [ ] Timer behavior verified (game runs at a believable, consistent
      speed, not wildly too fast/slow)
- [ ] `git log` shows iteration
- [ ] README noting which opcodes are implemented (all ~35, or a
      documented subset)

## Security relevance

An emulator that faithfully executes untrusted "programs" (ROMs here)
is a miniature version of the trust boundary Stage 12's malware sandbox
depends on — the interesting security question for any emulator is
always "can guest code do anything the host didn't intend to allow,"
even if this project's ROMs are harmless games.

## When done

Point me at the source + `git log` plus your test evidence. I'll check
opcode-decoding correctness against the spec first — CHIP-8's biggest
common bug is a handful of opcodes with confusingly similar encodings
getting swapped.
