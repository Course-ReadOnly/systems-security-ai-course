> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 8 — Operating Systems

**Time budget:** 8–10 weeks part-time / 4 weeks full-time

## Objectives

Go inside a real, small, readable kernel (xv6) instead of only reading
about scheduling/paging/filesystems in the abstract. This stage cashes
in Stage 5's process/memory concepts and Stage 7's assembly literacy —
xv6's source is small enough to actually read end to end, unlike Linux.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Full free textbook | [OSTEP](https://pages.cs.wisc.edu/~remzi/OSTEP/) |
| 02 | Build a real OS (MIT course + xv6) | [MIT 6.828/6.S081](https://pdos.csail.mit.edu/6.828/) |

**Topics:** scheduling, virtual memory, filesystems, drivers, paging,
context switching.

## Projects

| # | Project | Folder |
|---|---|---|
| 8.1 | Modify xv6 (guided exercises) | `projects/8.1-xv6-modifications/` |
| 8.2 | Write a new scheduler | `projects/8.2-new-scheduler/` |
| 8.3 | Add system calls | `projects/8.3-add-syscalls/` |

Suggested order: 8.1 (get comfortable in the codebase) → 8.3 (syscalls
are a smaller, more contained change) → 8.2 (the scheduler touches the
most interconnected code, do it last).
