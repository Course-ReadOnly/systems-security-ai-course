> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 5.3 — A Thread Pool

## Goal

Concurrency, for real: a fixed pool of worker threads pulling tasks off
a shared queue, using `pthread` mutexes/condition variables correctly.
This is the project where race conditions and deadlocks stop being
textbook warnings and start being things you actually have to debug.

## Requirements

1. A fixed number of worker threads created at startup (configurable
   count).
2. A thread-safe task queue: submitting a task from the main thread must
   be safe while workers are concurrently pulling from it — real
   mutex/condition-variable synchronization, not a busy-wait/spin loop.
3. Workers block (don't busy-wait, wasting CPU) when the queue is empty,
   and wake up promptly when work arrives.
4. Graceful shutdown: a way to signal "no more work is coming," let
   in-flight tasks finish, then join all threads cleanly — no
   thread leaks, no hangs.
5. Demonstrated with a real workload (e.g. submitting N tasks that each
   do some CPU work, or a parallel computation like summing chunks of an
   array) — must show actual concurrent execution, not accidentally
   serialize everything.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean, linked against `pthread`
- [ ] Paste output from a real workload demonstrating multiple tasks
      completing, with evidence they actually ran concurrently (e.g.
      timestamps, or total wall-clock time less than sum of individual
      task times)
- [ ] Run under **ThreadSanitizer** (`-fsanitize=thread`) or `helgrind`
      (valgrind's thread checker) — paste output showing no data races
      detected. This is the real correctness test for this project, more
      than `valgrind`'s normal leak check.
- [ ] Graceful shutdown demonstrated: all threads join, no hang, no
      leaked tasks
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log` plus the ThreadSanitizer/helgrind
output specifically — that's what I'll check first, since a thread pool
that merely "looks correct" in casual testing frequently still has a
real race hiding in it.
