> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 7.1 — Assembly Calculator

## Goal

A calculator, again — but this time in raw x86-64 assembly (NASM),
calling Linux syscalls directly for I/O. The point of repeating the
calculator project from Stage 1 is the contrast: feel exactly what C was
doing for you (stack frames, calling convention, string-to-number
conversion) by doing it by hand.

## Requirements

1. Written in x86-64 assembly (NASM syntax), assembled with `nasm` +
   linked with `ld` (no C runtime — raw syscalls for I/O, `_start` as
   entry point).
2. Reads two numbers and an operator from stdin (via the `read` syscall),
   performs `+ - * /`, prints the result (via `write`).
3. Correct exit via the `exit`/`exit_group` syscall (no relying on
   falling off the end).
4. Handles division by zero without crashing the process — a controlled
   error message and clean exit instead.
5. Uses the System V AMD64 calling convention correctly if you factor
   any logic into callable functions/labels (not required to, but if you
   do, do it correctly — register-clobbering is the classic bug here).

## Acceptance criteria

- [ ] Assembles and links cleanly (`nasm` + `ld`, no warnings)
- [ ] Paste output for each operator plus the division-by-zero case
- [ ] Confirmed via `strace` that only the syscalls you intended are
      being made (no hidden libc calls sneaking in) — paste relevant
      `strace` output
- [ ] `git log` shows iteration
- [ ] README documenting the syscall numbers used and the calling
      convention, in your own words

## Security relevance

Every buffer overflow/ROP technique Stage 13 will teach you to exploit
happens at exactly this level — raw registers, a stack with no bounds
checking, a calling convention enforced by nothing but convention. You
won't hit an overflow in a 4-function calculator, but writing at this
level once, by hand, is what makes "the return address lives on the
stack right next to your buffer" a fact you've actually seen rather
than a diagram you memorized.

## When done

Point me at the source + `git log` plus the `strace` output. I'll check
register usage around syscalls specifically (clobbering a register the
kernel expects unclobbered is the most common way this class of project
breaks in subtle, hard-to-debug ways).
