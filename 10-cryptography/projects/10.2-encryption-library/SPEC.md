> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 10.2 — Small Encryption Library

## Goal

A companion to 10.1, but framed the opposite way: **implement** a
well-known cipher yourself (this is where Cryptopals-style
from-scratch implementation belongs, unlike 10.1). The point is
understanding a real cipher's internals — never use this library for
anything real, and say so explicitly.

## Requirements

1. Implement a real, well-specified cipher from scratch — AES (at least
   one mode, e.g. CBC or CTR) is the standard choice, matching
   Cryptopals' progression.
2. Correctness verified against **official test vectors** (NIST
   publishes AES test vectors) — this is non-negotiable; "it encrypts
   and decrypts back to the same thing" is not proof of correctness,
   matching a published test vector is.
3. A small CLI or library API to encrypt/decrypt a file or string.
4. **A prominent, explicit disclaimer** (README, and ideally in the
   code) that this is an educational implementation, not
   audited/production-safe, and must never be used to protect anything
   real.

## Acceptance criteria

- [ ] Builds/runs cleanly
- [ ] **Paste output matching at least 2 official NIST test vectors**
      exactly — this is the actual correctness proof for this project
- [ ] Round-trip (encrypt then decrypt) demonstrated on real data beyond
      the test vectors
- [ ] `git log` shows iteration
- [ ] README contains the educational-use disclaimer, plus an
      explanation of the cipher/mode implemented in your own words

## Security relevance

The disclaimer requirement exists because a home-grown crypto
implementation is exactly the "rolled your own" risk `SECURITY-CONCEPTS.md`'s
"Cryptographic Misuse" entry and 10.1's spec both warn against —
correct-looking output on your own test cases proves nothing about
resistance to side-channel attacks (non-constant-time comparisons,
timing leaks), and matching NIST test vectors proves only functional
correctness, not that this implementation is safe to protect anything
real with. Understanding AES's internals here is what makes 10.1's
"never implement your own cipher" rule land as informed judgment
rather than an arbitrary restriction.

## When done

Point me at the source + `git log` and the test-vector evidence. If the
test vectors don't match exactly, nothing else about this project
matters yet — that's the first thing I'll check.
