> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 25.7 — AI CTF Assistant

## Goal

An LLM-backed assistant for your **own** CTF lab practice (pwn.college/
ROP Emporium/PortSwigger challenges you're already working, from Stage
13) — a tool that helps you reason through a challenge (hints, approach
suggestions) without just handing you the answer, mirroring this
course's own "escalating hints, not free answers" philosophy.

## Requirements

1. Given a CTF challenge's description/binary/source (from your own
   in-progress Stage 13 work), the assistant provides **escalating
   hints** — a first-level hint is vague/directional, later levels get
   more specific, only the final level gives the actual approach. It
   should never jump straight to the answer.
2. Explicitly designed to encourage you to attempt the next step
   yourself before requesting the next hint level — the tool's own UX
   should discourage skipping straight to the strongest hint.
3. Used on **your own designated practice-platform challenges only**
   (pwn.college, ROP Emporium, PortSwigger) — never against a live CTF
   competition's challenges in a way that would violate that
   competition's rules, and never against real, non-practice targets.

## Acceptance criteria

- [ ] Runs successfully against a real challenge from your Stage 13 work
- [ ] Paste a session showing the escalating-hint behavior across at
      least 3 hint levels for one real challenge, ending in you actually
      solving it
- [ ] Confirm/discuss whether the hint escalation actually felt useful
      versus either too vague to help or too quick to give away the
      answer — tune based on this before calling it done
- [ ] `git log` shows iteration
- [ ] README stating explicitly this is for your own designated-
      platform practice, not live competitions or real targets

## When done

Point me at the source + `git log` and the hint-escalation session.
I'll check whether the hint levels are genuinely graduated (not just
three copies of the same vagueness, or a level-1 hint that's already
basically the answer).
