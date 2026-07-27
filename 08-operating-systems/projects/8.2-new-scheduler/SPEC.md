> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 8.2 — Write a New Scheduler

## Goal

Replace xv6's default round-robin scheduler with a different policy —
the project where "scheduling algorithm" stops being a diagram in OSTEP
and becomes code that determines which process actually gets the CPU
next, with observable, measurable consequences.

## Requirements

1. Implement a different scheduling policy than xv6's default — e.g.
   priority-based scheduling, or a simple multi-level feedback queue
   (OSTEP covers both; pick one and understand it before coding it).
2. Processes need a way to be assigned/observe their priority (a new
   syscall or a sensible default assignment scheme).
3. Demonstrate the policy actually changes behavior versus the default:
   a workload of processes with different priorities/characteristics
   where completion order visibly differs from round-robin.
4. Don't break existing xv6 functionality — the rest of the OS (syscalls,
   filesystem, shell) must still work correctly with your scheduler in
   place.

## Acceptance criteria

- [ ] xv6 builds and boots with the new scheduler
- [ ] A test workload (multiple processes, deliberately different
      priorities/burst lengths) run under **both** the old and new
      scheduler, with output/timing showing the actual behavioral
      difference — this comparison is the real proof of this project,
      not just "it compiles"
- [ ] Confirm existing xv6 functionality (shell, basic programs) still
      works correctly under the new scheduler
- [ ] `git log` shows iteration
- [ ] README explaining the scheduling policy chosen and why, plus what
      the before/after comparison demonstrates

## When done

Point me at your fork + `git log` and the before/after comparison. I'll
check that the comparison is actually controlled (same workload, only
the scheduler changed) — an uncontrolled comparison doesn't prove
anything.
