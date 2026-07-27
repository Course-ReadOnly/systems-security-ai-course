> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 5.2 — A Malloc Implementation

## Goal

Implement `malloc`/`free`/`realloc` yourself, on top of raw memory from
`sbrk`/`mmap` — the thing you've been calling for free since Stage 1,
built from scratch. This is where "memory management" stops being an
abstraction and becomes an explicit free-list/bookkeeping problem you own.

## Requirements

1. Your own `my_malloc`/`my_free`/`my_realloc` (don't shadow the real
   `malloc` name — link/test against your own explicitly).
2. Requests underlying memory from the OS via `sbrk` or `mmap` (your
   choice, document which and why).
3. Tracks free blocks (a free list is the standard approach) and reuses
   freed memory for future allocations rather than only ever growing.
4. Splits/coalesces blocks — allocating less than a free block splits it;
   freeing adjacent free blocks merges them, rather than fragmenting
   forever.
5. Correct behavior on edge cases: `malloc(0)`, freeing `NULL`,
   double-free detection (at minimum: don't corrupt state catastrophically
   — full detection/abort is a reasonable stretch goal).

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] A test program using your allocator for a realistic workload
      (e.g. a linked list or array built via `my_malloc`) — paste output
      proving correctness
- [ ] Fragmentation test: alloc/free a pattern designed to test
      splitting/coalescing, paste before/after showing blocks actually
      merge back together rather than fragmenting
- [ ] Edge cases (`malloc(0)`, `free(NULL)`) tested and pasted
- [ ] Compare against real `malloc` on the same workload for a sanity
      check (doesn't need to match performance, just correctness)
- [ ] `git log` shows iteration
- [ ] README explaining your free-list design and the splitting/
      coalescing strategy

## When done

Point me at the source + `git log`. I'll check the free-list bookkeeping
hardest — off-by-one errors in block-header sizes are the single most
common bug in a project like this, and they tend to corrupt memory
silently rather than crash immediately.
