> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached.

# Project 24.4 — Ethernaut Write-Up

## Goal

The security half of this stage: a full pass through Ethernaut
(OpenZeppelin's smart contract security wargame), with a real
vulnerability-by-vulnerability write-up — the same pattern this course
already uses for crackmes in Stage 11 and ROP Emporium in Stage 13.
Ethernaut is a designated legal practice platform built exactly for
this; see the Stage 24 README's scope/safety note before starting.

## Requirements

1. Complete at least the first 15 Ethernaut levels (there are more; 15
   is the floor, not a ceiling — keep going if it's landing well).
2. For **each** level, write up: what the vulnerability class is (name
   it — reentrancy, integer overflow, delegatecall misuse, access
   control, front-running, etc.), the specific line(s)/mechanism in the
   contract that make it exploitable, the exploit itself (your actual
   solving transaction/script), and how you'd fix the contract to close
   the hole.
3. At least 3 of your write-ups must include a **proof-of-concept
   exploit contract or script** you wrote (not just "I called function
   X with argument Y through the console") — the same standard as a
   real audit report, not a walkthrough summary.
4. Cross-reference each vulnerability class against
   `SECURITY-CONCEPTS.md` where a matching entry exists (e.g.
   reentrancy is a close cousin of the Race Conditions/TOCTOU entries)
   — add a note there yourself if a genuinely new class shows up that
   isn't covered yet.

## Acceptance criteria

- [ ] At least 15 Ethernaut levels completed
- [ ] Written report per level: vulnerability class named, root cause
      explained, exploit described, fix described
- [ ] At least 3 levels backed by an actual exploit contract/script in
      the repo, not just prose
- [ ] `git log` shows real iteration (write-ups added as you go, not
      one final dump)
- [ ] At least one explicit cross-reference to an existing
      `SECURITY-CONCEPTS.md` entry, or a proposed new entry if none fits

## Security relevance

This project *is* the security relevance — it's the Stage 24 equivalent
of Stage 13's exploit labs, applied to smart contracts instead of web/
binary targets. Requirement 4's explicit ask to cross-reference (or
propose) `SECURITY-CONCEPTS.md` entries is intentional: reentrancy is a
close cousin of the "Race Conditions" entry, access-control bugs mirror
"Access Control / Scoping," and documenting that connection yourself is
part of the exercise, not something to have handed to you.

## When done

Point me at the write-ups and `git log`. I'll pick 2-3 levels and ask
you to explain the exploit without looking at your own notes — for the
reentrancy-class levels especially, being able to explain *why* the
external call before the state update is the actual bug (not just
"reentrancy is when you call back in") is the real bar here.
