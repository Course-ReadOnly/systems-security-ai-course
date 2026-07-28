> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 15.3 — UART Driver

## Goal

Write a UART driver from the register level — the same skill as Stage
5's OS-level device driver concepts, but touching real hardware
registers directly instead of an OS abstraction layer. UART is the
right first peripheral driver because you can verify it trivially (a
serial terminal on your computer).

## Requirements

1. Configures UART registers directly (baud rate, data bits, parity,
   stop bits) — not via a vendor HAL's one-line "UART_Init()" call; the
   point is understanding the registers themselves.
2. Implements both **transmit** and **receive**, either polling-based or
   interrupt-driven (interrupt-driven is the stronger version — do
   polling first if new to this, then interrupt-driven as a follow-up).
3. Correctly handles buffer overrun on receive (what happens if data
   arrives faster than it's consumed) — document the chosen behavior.
4. Verified against a real serial terminal on your computer (e.g.
   `screen`/`minicom` connected via USB-UART).

## Acceptance criteria

- [ ] Driver builds and runs on real hardware
- [ ] Paste/describe a real serial session: sending data to the board
      and receiving it back correctly, confirmed via terminal output on
      your computer
- [ ] Baud rate/framing correctness demonstrated (readable text, not
      garbled output — garbled output means the register config is wrong)
- [ ] `git log` shows iteration
- [ ] README documenting the specific registers configured and why

## Security relevance

Requirement 3 (buffer overrun on receive) is Stage 1's memory-safety
lesson at the hardware register level: data arriving faster than it's
consumed and overwriting a fixed-size receive buffer is a real buffer
overflow, just triggered by physical signal timing instead of a
malicious input string. Embedded devices are also disproportionately
exposed here — no MMU/ASLR/stack canaries the way Stage 15's
"no OS safety net" framing already covers, so a driver-level overflow
on a microcontroller has fewer mitigations standing between it and
real impact than the equivalent bug would on a full OS.

## When done

Point me at the source + `git log` and your terminal session evidence.
I'll check the register configuration against the datasheet values you
document — this is the part that's either exactly right or produces
garbage, with no in-between.
