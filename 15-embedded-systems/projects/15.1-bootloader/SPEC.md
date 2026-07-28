> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 15.1 — Bootloader

## Goal

The first code that runs on the board, before any "real" firmware — a
minimal bootloader that initializes just enough hardware to load and
jump to a second-stage application. This is the embedded-hardware
equivalent of Stage 4/7's boot-sequence concepts, made real on physical
hardware instead of an emulator.

## Requirements

1. Runs on real hardware (an STM32 dev board or similar ARM Cortex-M
   target) — minimal startup code (clock init, stack pointer setup)
   before jumping to application code.
2. Loads/jumps to a separate application binary (even a trivial one, e.g.
   blinking an LED) — demonstrating the bootloader → application handoff.
3. At minimum, a basic integrity check before jumping (e.g. a checksum
   of the application image) — don't jump to garbage if the image is
   invalid.
4. Documents the memory layout used (where the bootloader lives, where
   the application is expected to be) — this is load-bearing information
   for anything built on top of it later.

## Acceptance criteria

- [ ] Bootloader flashes and runs on real hardware
- [ ] Paste/describe evidence of successful handoff to a real
      application (e.g. an LED blinking, confirming the app actually ran)
- [ ] Corrupted-image case tested (deliberately corrupt the application
      image) — bootloader detects it and doesn't jump to garbage
- [ ] `git log` shows iteration
- [ ] README documenting the memory layout (bootloader region vs.
      application region)

## Security relevance

Requirement 3's integrity check is a miniature version of **Secure
Boot** — the real-world chain-of-trust model where each stage
cryptographically (or, here, minimally via checksum) verifies the next
before executing it, so a compromised or corrupted image can't silently
run. A bootloader that jumps to whatever's in flash unconditionally has
no way to distinguish a legitimate update from tampered/malicious
firmware — the exact gap real embedded-security work spends significant
effort closing.

## When done

Point me at the source + `git log` and a description/recording of it
running on real hardware. I'll check the integrity-check logic and the
memory-layout documentation — this is exactly the kind of detail that
silently breaks everything built on top of it later.
