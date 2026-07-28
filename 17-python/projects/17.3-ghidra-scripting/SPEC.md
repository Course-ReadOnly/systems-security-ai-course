> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 17.3 — Ghidra Scripting

## Goal

Automate part of Stage 11's reverse-engineering workflow using Ghidra's
Python scripting API — the actual, professional way RE work scales
beyond one binary at a time. This is direct prep for Stage 25's "AI
decompiler helper" project, which builds on exactly this scripting
interface.

## Requirements

1. A Ghidra script (Python, via Ghidra's scripting API) that automates a
   real analysis task — e.g. listing all function names matching a
   pattern, extracting all string references and their calling
   functions, or auto-renaming functions based on a heuristic (like
   detected library calls).
2. Runs against a real binary you've analyzed before (from Stage 11) —
   demonstrating it produces genuinely useful output, not a toy example.
3. Can run in **headless mode** (Ghidra's `analyzeHeadless`), not just
   interactively — this is what makes it actually automatable/batchable.

## Acceptance criteria

- [ ] Script runs successfully inside Ghidra (interactive or headless)
      against a real binary — paste the output
- [ ] Headless-mode run demonstrated specifically (the interactive-only
      version doesn't satisfy this requirement)
- [ ] Output cross-checked manually against a few functions in Ghidra's
      GUI to confirm the script's findings are actually correct
- [ ] `git log` shows iteration
- [ ] README explaining what the script automates and why it's useful

## Security relevance

Scripted, headless analysis (Requirement 3) is what makes RE work scale
past "one analyst, one binary, one afternoon" into something that keeps
up with real malware volume — the same reason Stage 25's AI-assisted
tooling builds on exactly this scripting interface rather than
replacing manual RE outright. The manual spot-check requirement exists
because an automation script that's subtly wrong at scale is worse than
no automation — it produces confident, wrong answers across every
binary it touches, not just one.

## When done

Point me at the source + `git log` and the headless-mode run evidence.
I'll check that the script's findings are actually correct against a
manual spot-check, not just "the script ran without throwing an error."
