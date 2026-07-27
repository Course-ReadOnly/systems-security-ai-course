> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 8.3 — Add System Calls

## Goal

Add real, new system calls to xv6, end to end — the syscall table, the
kernel-side implementation, and a user-space program that calls them.
This is the concrete mechanics behind everything you've been calling
(`read`, `write`, `fork`) since Stage 5, now from the implementer's side.

## Requirements

1. Add **at least two** new syscalls to xv6 (not just one — the second
   one should go faster since you'll already understand the plumbing,
   which is itself the point).
2. Suggested candidates: a syscall returning some kernel-tracked stat
   (e.g. process count, or a custom per-process counter), and a syscall
   that does something with observable side effects (e.g. one that
   modifies process state in a way a user program can then observe).
3. Correctly wire through every layer xv6 requires: syscall number
   definition, the syscall table entry, the kernel-side handler, and the
   user-space stub/declaration.
4. A user-space test program that calls both new syscalls and prints
   their results.
5. Basic argument validation in the kernel-side handler (don't trust
   user-space pointers/values blindly) — this is a real security
   principle (never trust the caller), not busywork.

## Acceptance criteria

- [ ] xv6 builds and boots with the new syscalls added
- [ ] User-space test program calling both syscalls, output pasted
      showing correct results
- [ ] At least one deliberately-bad call tested (e.g. an invalid pointer
      argument, if applicable) — kernel handles it without crashing/
      panicking
- [ ] `git log` shows iteration, ideally one commit per syscall added
      showing the pattern repeating
- [ ] README documenting each new syscall's number, signature, and
      purpose

## When done

Point me at your fork + `git log`. I'll check the kernel-side argument
handling first — trusting a user-supplied pointer without validation is
a real, exploitable class of kernel bug, and this project is exactly
where that habit either gets built or doesn't.
