> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 15.2 — Small Firmware Project

## Goal

A real, complete embedded application running on your 15.1 bootloader
(or standalone if you skip 15.1) — something with actual sensor/
peripheral interaction, not just a blinking LED.

## Requirements

1. Pick a concrete, real firmware project involving at least one
   peripheral beyond a basic GPIO LED — e.g. reading a sensor over I2C/
   SPI, or a simple state machine responding to a button with debouncing.
2. Correct interrupt handling if used (a common source of embedded bugs:
   doing too much work inside an ISR, or missing volatile on
   shared state).
3. Runs reliably over a sustained period (not just "worked once") —
   demonstrate it running continuously for a meaningful stretch of time.
4. Reasonable power/resource awareness — document any deliberate choices
   around sleep modes/power, even if minimal for this project.

## Acceptance criteria

- [ ] Firmware flashes and runs correctly on real hardware
- [ ] Description/recording of it working, including the peripheral
      interaction (e.g. sensor readings printed over UART, or observable
      physical behavior)
- [ ] Sustained-operation evidence (ran correctly for an extended period,
      not just a single successful boot)
- [ ] `git log` shows iteration
- [ ] README describing the hardware setup and what the firmware does

## Security relevance

Requirement 2's `volatile`/ISR-scope warning is a real-time cousin of
the race conditions covered in `SECURITY-CONCEPTS.md` — an interrupt
handler racing the main loop over shared state without `volatile` (or
proper synchronization) is the embedded equivalent of a TOCTOU bug,
just triggered by a hardware interrupt instead of a scheduler
preemption. This class of bug is also exactly why "worked once" isn't
evidence (Requirement 3) — timing-dependent bugs surface intermittently
by nature.

## When done

Point me at the source + `git log` and your evidence of it running. I'll
check interrupt/shared-state handling if used — `volatile` correctness
and ISR scope are the classic sources of "works sometimes" embedded bugs.
