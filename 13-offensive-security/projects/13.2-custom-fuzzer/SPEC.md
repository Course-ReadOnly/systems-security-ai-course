> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 13.2 — Custom Fuzzer

## Goal

Build a basic mutation-based fuzzer and use it to find a real crash in
one of your own Stage 1/5 C programs (a program you wrote and can safely
crash and debug — not a live/shared target). This is the automated,
systematic version of the manual exploitation you practiced in 13.1.

## Requirements

1. A mutation-based fuzzer: takes a seed input, applies random mutations
   (bit flips, byte insertions/truncations, boundary values), and feeds
   the result to a **target program you wrote yourself** (a good
   candidate: your Stage 1 file copier or text-statistics tool, or a
   deliberately-unsafe test program — document which).
2. Detects crashes (target program segfaulting/aborting) and saves the
   crashing input for later reproduction.
3. Runs for a meaningful number of iterations, tracking basic stats
   (inputs tried, crashes found).
4. When a crash is found: reproduce it deterministically (rerun the
   saved crashing input), and analyze it with `gdb`/AddressSanitizer to
   identify the actual bug (e.g. a buffer overflow) — this closes the
   loop back to Stage 1's memory-safety lessons.

## Acceptance criteria

- [ ] Fuzzer builds/runs cleanly
- [ ] Paste a fuzzing run finding **at least one real crash** in a
      target you wrote — if your existing programs are all crash-free
      (a good sign for those projects, but not useful here), write a
      small deliberately-vulnerable test program and say so explicitly
- [ ] The crashing input saved and reproduced deterministically — paste
      both the fuzzer's discovery and a standalone rerun confirming it
- [ ] Root-cause analysis of the crash (via `gdb`/ASan) pasted,
      identifying the specific bug
- [ ] `git log` shows iteration

## When done

Point me at the fuzzer + `git log` and the crash evidence. I'll check
that the crash is actually reproducible outside the fuzzing loop (a
"crash" that doesn't reproduce standalone isn't proven yet) and that the
root-cause analysis is genuinely correct, not just plausible-sounding.
