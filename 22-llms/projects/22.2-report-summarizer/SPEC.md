> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 22.2 — Malware Report Summarizer

## Goal

Summarize Stage 12-style malware analysis reports (yours, or public
ones) into consistent, structured summaries — a real productivity tool
for the "too many reports, not enough analyst hours" problem defensive
teams actually have.

## Requirements

1. Takes a malware analysis report (your own from 12.2, or a public
   write-up) as input, produces a structured summary: sample
   identification, behavior summary, IOCs, and a severity/risk framing.
2. Consistent output schema across different input report styles/
   formats — the summarizer's value is in normalizing messy, varied
   source material into something scannable.
3. **Extracts IOCs into the same structured format as your Stage 12.1/
   17.2 IOC tools** — reuse that schema rather than inventing a new one.
4. Handles a report that doesn't contain enough information for some
   fields (e.g. no IOCs mentioned) — states that explicitly rather than
   hallucinating plausible-looking fake indicators. This is the
   single most important failure mode to guard against in this project.

## Acceptance criteria

- [ ] Runs successfully summarizing at least 3 different reports
      (varying source styles) into the consistent structured format
- [ ] **Explicit test for the hallucination failure mode**: feed it a
      report with sparse/missing information in some fields, paste
      output confirming it says "not stated" rather than inventing
      a plausible-sounding fake value
- [ ] IOC extraction cross-checked against manual reading of at least
      one report, confirming accuracy
- [ ] `git log` shows iteration
- [ ] README documenting the output schema and prompt design

## When done

Point me at the source + `git log` and the hallucination-test evidence
specifically — that's the test I'll look at first, since a summarizer
that invents indicators is actively worse than a human just reading the
report themselves.
