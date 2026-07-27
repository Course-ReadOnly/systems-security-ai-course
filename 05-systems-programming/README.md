> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 5 — Systems Programming

**Time budget:** 8–10 weeks part-time / 4 weeks full-time

## Objectives

The core Linux/POSIX systems programming stage: processes, threads,
pipes, signals, memory management, and network sockets, all from
first principles. This is arguably the single highest-leverage stage in
the whole roadmap — the shell, malloc, and HTTP server projects here
recur conceptually in Stage 8 (OS), Stage 9 (Networking), and Stage 13
(Offensive Security) alike.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Canonical course (CS:APP) | [CMU 15-213](https://www.cs.cmu.edu/~213/) |
| 02 | Alternative full course | [Stanford CS107](https://web.stanford.edu/class/cs107/) |
| 03 | Reference book | [CS:APP site materials](https://csapp.cs.cmu.edu/) |

**Topics:** processes, threads, fork, pipes, signals, mmap, epoll, memory
management.

## Projects

| # | Project | Folder |
|---|---|---|
| 5.1 | A shell | `projects/5.1-shell/` |
| 5.2 | A malloc implementation | `projects/5.2-malloc/` |
| 5.3 | A thread pool | `projects/5.3-thread-pool/` |
| 5.4 | An HTTP server | `projects/5.4-http-server/` |
| 5.5 | A static web server | `projects/5.5-static-web-server/` |

Suggested order: 5.1 (processes/fork/exec) → 5.2 (memory) → 5.3 (threads)
→ 5.4 → 5.5 (5.5 is a focused, simpler variant of 5.4 — do 5.4 first).
