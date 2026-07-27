> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 23.6 — AI-Powered Fuzzing Assistant

## Goal

Extend Stage 13.2's mutation-based fuzzer with LLM-guided input
generation — using a model to suggest structurally interesting seed
inputs/mutations (e.g. for a parser, generating syntactically-plausible-
but-edge-case inputs) rather than purely random mutation, and measuring
whether that actually improves coverage/crash-finding.

## Requirements

1. Extends your 13.2 fuzzer with an LLM-guided input-generation mode —
   e.g. the LLM generates or mutates seed inputs based on the target's
   expected input format (if fuzzing a parser, ask it to generate
   tricky-but-valid-looking inputs, edge cases, boundary values).
2. **Measures code coverage** (not just crash count) for both the
   original random-mutation approach and the LLM-guided approach against
   the same target, over a comparable time/iteration budget — this
   comparison is the actual point of the project.
3. Reports honestly whether LLM guidance helped, hurt, or made no
   meaningful difference — a null result is a legitimate, useful finding
   here, not a failure of the project.

## Acceptance criteria

- [ ] Both fuzzing modes (original random, LLM-guided) run against the
      same target for a comparable budget
- [ ] Coverage measurements (e.g. via `gcov`/`llvm-cov` or similar)
      pasted for both modes, compared side-by-side
- [ ] Crash-finding results compared side-by-side too
- [ ] Honest discussion of which approach actually performed better and
      why you think that is
- [ ] `git log` shows iteration
- [ ] README documenting the LLM-guidance approach used

## When done

Point me at the source + `git log` and the coverage comparison. I'll
check the comparison is genuinely controlled (same target, same budget)
— an uncontrolled comparison would make the conclusion meaningless
regardless of which way it points.
