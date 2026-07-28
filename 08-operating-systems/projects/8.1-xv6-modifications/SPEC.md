> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 8.1 — Modify xv6 (Orientation)

## Goal

Get xv6 building, booting (in QEMU), and modified in small, real ways
before attempting the bigger 8.2/8.3 projects. The goal here is
comfort navigating a real (if small) kernel codebase — not a big feature.

## Requirements

1. Build xv6 from source and boot it in QEMU successfully.
2. Add a **new, trivial user-space program** to xv6 (e.g. a `hello`
   command) — this exercises the build system and confirms you
   understand how user programs get built/included.
3. Make **one small, real kernel-side change** with observable effect —
   e.g. modify the kernel boot message, or add a print statement in a
   syscall path and confirm it fires. Small, but must be a genuine kernel
   change, not just the user-space program from #2.
4. Document, in your own words, the boot sequence you observed (from
   QEMU start to shell prompt) — this is the orientation this project is
   actually for.

## Acceptance criteria

- [ ] xv6 builds and boots cleanly in QEMU — paste the boot output
- [ ] New user-space program built and run inside xv6 — paste a shell
      session showing it
- [ ] Kernel-side change demonstrated with before/after evidence (e.g.
      the modified boot message, or your added print statement's output)
- [ ] `git log` shows iteration (against your own fork/copy of xv6, not
      the original repo)
- [ ] README describing the boot sequence in your own words

## Security relevance

This project is orientation, not depth, so the security payoff is
positional rather than technical: everything from here through 8.3 (and
Stage 26's kernel module work later) happens *inside* the trust
boundary that Stage 13 attacks and Stage 14 defends from the outside.
Getting comfortable navigating real kernel source now is what makes
"kernel-mode vs. user-mode" something you've actually walked across,
not just a diagram.

## When done

Point me at your fork + `git log` and the boot/session evidence. This
one's about orientation, not depth — I'll mainly check you can navigate
and actually modify the codebase before 8.2/8.3.
