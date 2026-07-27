> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 24.5 — An eBPF Monitor

## Goal

Write a real eBPF program that observes kernel/syscall activity —
the modern, safe alternative to 24.4's kernel module for many
observability use cases (the verifier prevents whole classes of the
crashes 24.4 has to be careful about). This closes the loop back to
Stage 14's monitoring/detection themes, now at the kernel level.

## Requirements

1. An eBPF program (via a framework like `bcc`, `libbpf`, or `bpftrace`
   for the scripting-first version) that attaches to a real kernel
   event — e.g. a syscall entry (like `execve`, to log process
   creation) or a network event.
2. Passes data from kernel-space back to user-space (via a map/ring
   buffer) and displays it meaningfully — not just "the eBPF program
   loaded," but actually observing and reporting real events as they
   happen.
3. Runs for a meaningful period while generating real activity on the
   system (e.g. running various commands while an `execve` monitor is
   attached) and correctly reports it.
4. Note explicitly which eBPF program type/attach point was used and
   why.

## Acceptance criteria

- [ ] eBPF program loads successfully and attaches to a real kernel
      event
- [ ] Paste output showing real events captured live (e.g. process
      execs as they happen, while you run other commands in another
      terminal)
- [ ] `git log` shows iteration
- [ ] README documenting the attach point and data-passing mechanism
      used

## When done

Point me at the source + `git log` and the live-capture evidence. I'll
check that what's captured is genuinely live/real (not a canned/mocked
demo) and that the kernel-to-userspace data path is correctly designed
for the volume of events this attach point could realistically produce.
