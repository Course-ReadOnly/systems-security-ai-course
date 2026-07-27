> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before Stage 0 is done. Revisit and adjust when actually reached.

# Project 1.3 — File Copier

## Goal

Reimplement `cp` (the basic case) from scratch, using low-level file
I/O. The point is understanding what `cp` actually does at the syscall
level — buffered reads/writes, byte counts, and every failure mode you've
been taking for granted (missing source, no permission, destination
already exists) — not just calling a library function that does it for you.

## Requirements

1. `./filecopy <source> <dest>` — copies `source` to `dest` byte-for-byte.
2. Uses a fixed-size buffer and a read/write loop (no reading the whole
   file into memory at once, regardless of size).
3. Real error handling: source doesn't exist, no read permission on
   source, no write permission on destination directory — each a clear
   error message and non-zero exit, not a crash.
4. Verify correctness: after copying, the destination must be byte-
   identical to the source (you'll prove this in acceptance criteria).
5. `Makefile`.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Paste a successful copy, then `diff` (or `cmp`) showing source and
      dest are identical
- [ ] Paste each error case (missing source, permission denied) showing
      a clear message and non-zero exit — `echo $?` after each
- [ ] Tested against a large-ish file (a few MB) to confirm the buffered
      read/write loop actually works, not just small files
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## Security relevance

A fixed-size buffer plus a read/write loop is exactly the shape of code
where classic buffer overflows live — get the bounds arithmetic wrong
here (an off-by-one on buffer size, trusting a read count without
checking it) and you've written the same bug ROP Emporium's Stage 13
challenges exist to exploit. Getting this loop provably correct now is
direct rehearsal for spotting it broken later.

## When done

Point me at the source + `git log`. I'll check the buffer loop handles
partial reads/writes correctly (a short `read()` isn't EOF) and whether
error messages actually reflect `errno`, not a generic string.
