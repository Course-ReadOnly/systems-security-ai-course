> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 25.5 — AI Decompiler Helper

## Goal

Extend Stage 17.3's Ghidra scripting and 23.1's RE assistant into a
tool integrated directly into the RE workflow: a Ghidra script that
queries an LLM to suggest function names/variable names/comments for
decompiled code, applying suggestions back into the Ghidra database
itself — not just a separate standalone summarizer.

## Requirements

1. A Ghidra script (building on 17.3) that, for a given function,
   sends its decompiled pseudocode to an LLM and gets back suggested:
   a function name, variable names, and a summary comment.
2. **Applies suggestions back into Ghidra's actual database** (renaming
   functions/variables, adding comments via the API) — not just printing
   suggestions to a console, disconnected from the tool you're actually
   using.
3. Includes a review/confirm step — suggestions get applied only after
   explicit acceptance (auto-applying unreviewed LLM suggestions to a
   real analysis database is a bad practice this tool shouldn't
   normalize).
4. Tested against real functions you've already manually reverse-
   engineered (from 11.1-11.4), comparing the LLM's naming suggestions
   against your own already-known-correct understanding.

## Acceptance criteria

- [ ] Script runs inside Ghidra, successfully queries the LLM and
      receives suggestions for real decompiled functions
- [ ] Paste evidence of suggestions actually being applied to the
      Ghidra database (renamed functions/variables visible in the GUI)
- [ ] Review/confirm step demonstrated (a suggestion rejected, showing
      it's not auto-applied)
- [ ] At least 3 comparisons against your own known-correct
      understanding from earlier RE projects
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log` and the before/after Ghidra evidence.
I'll check the review-step actually gates application (not just a UI
formality that always proceeds) and whether suggestions are genuinely
useful versus generic-sounding.
