> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 24.4 — A Kernel Module

## Goal

Write and load a real Linux kernel module — code running in kernel
space on a real (or VM-hosted, strongly recommended) Linux system, a
step beyond Stage 8's xv6 work since this is a real, modern kernel with
real consequences for mistakes.

## Requirements

1. **Do this inside a VM**, not your host machine directly — a kernel
   module bug can crash or corrupt a real system, and this is exactly
   where that risk is real, not hypothetical.
2. A loadable kernel module (`insmod`/`rmmod`) that does something
   observable — e.g. a `/proc` entry you can read, or logging to
   `dmesg` on load/unload.
3. Correct module init/exit functions, with all resources acquired in
   init cleanly released in exit (no resource leaks across
   load/unload cycles).
4. Load and unload it **repeatedly** to confirm it's actually clean
   (a module that "works" once but leaks/crashes on the second
   load/unload has a real bug).

## Acceptance criteria

- [ ] Module builds against your kernel's headers, loads and unloads
      successfully — **explicitly confirm this was done in a VM**
- [ ] Paste `dmesg` output showing correct init/exit behavior
- [ ] Paste evidence of at least 3 repeated load/unload cycles with no
      degradation (no leaked resources, no warnings accumulating in
      `dmesg`)
- [ ] `git log` shows iteration
- [ ] README documenting what the module does and confirming the VM
      safety precaution

## Security relevance

Same caution as Stage 8.3, at higher stakes on a real modern kernel:
any user-space-facing interface this module exposes (a `/proc` entry,
an ioctl) needs the same never-trust-the-caller discipline. Dirty COW
(CVE-2016-5195 — see `SECURITY-CONCEPTS.md`) is what happens when a
real kernel gets this wrong.

## When done

Point me at the source + `git log` and the repeated-cycle evidence.
I will not consider a "worked once" demo sufficient for this project —
kernel modules that leak on unload are a real, common failure mode this
project specifically needs to demonstrate isn't present.
