> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 23.1 — Reverse-Engineering Assistant

## Goal

An LLM-backed tool that helps with Stage 11-style RE work — e.g. taking
decompiled/disassembled function output and generating a plain-English
explanation, or suggesting a likely function name/purpose. The point is
learning to build **useful, honest** LLM tooling for a technical domain,
not a demo that looks impressive on cherry-picked examples.

## Requirements

1. Takes real input from your Stage 11/17 work (decompiled C-ish
   pseudocode from Ghidra, or raw disassembly) and produces a plain-
   English summary of what the function likely does.
2. Uses a real LLM API (or a strong open-weight model run locally) with
   a deliberately engineered prompt — not just "paste the code, ask
   'what does this do?'" with no structure/context given to the model.
3. **Ground-truth comparison**: run it against functions you've
   *already* manually reverse-engineered (from 11.1's crackmes or
   11.2/11.3's parser work) and compare the LLM's explanation against
   your own known-correct understanding.
4. Explicitly surfaces when the LLM is uncertain or likely wrong — a
   tool that confidently states incorrect things about a binary is worse
   than no tool; design the prompt/output to hedge appropriately rather
   than hide uncertainty.

## Acceptance criteria

- [ ] Runs successfully against real decompiled/disassembled input
- [ ] Paste at least 3 comparisons: LLM's explanation vs. your own
      ground-truth understanding of the same function, noting where it
      was right, wrong, or plausibly-wrong-in-a-dangerous-way
- [ ] At least one case where the tool's output is **wrong** discussed
      honestly — what happened, and does the tool's uncertainty framing
      (if any) catch it
- [ ] `git log` shows iteration
- [ ] README documenting the prompt design and model/API used

## When done

Point me at the source + `git log` and the ground-truth comparisons.
I care more about the honest wrong-answer analysis here than a
cherry-picked success — a tool that's right 80% of the time but you
can't tell which 80% is genuinely dangerous in this domain.
