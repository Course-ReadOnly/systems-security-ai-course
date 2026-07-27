> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 23.2 — AI IOC Extractor

## Goal

Improve on Stage 12.1/17.2's rule-based IOC extraction with an
LLM-assisted approach — catching indicators that rigid regex/pattern
matching misses (obfuscated URLs, indicators described in prose within
a report) while still validating outputs rigorously.

## Requirements

1. Given raw, messy input (a sample's strings output, or a prose
   analysis report), extracts IOCs using an LLM **in addition to** your
   existing rule-based extractor — the comparison between the two is
   the actual point of this project.
2. **Every LLM-suggested indicator is validated programmatically**
   (an "IP" must actually parse as a valid IPv4/v6, a "hash" must be the
   right length/format) before being trusted — never take LLM output
   as ground truth without a real check.
3. Directly compares LLM-found IOCs against your rule-based extractor's
   findings: what did each approach find that the other missed?

## Acceptance criteria

- [ ] Runs against real input, paste the LLM-suggested IOC list
      alongside the rule-based extractor's list for the same input
- [ ] Validation logic demonstrated rejecting at least one plausible-
      but-invalid LLM suggestion (this will happen — show it being
      caught, not just assumed to happen)
- [ ] Discussion of what each approach found that the other didn't
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log` and the comparison. I'll check the
validation layer hardest — an LLM confidently suggesting a fake-but-
plausible-looking IOC that isn't caught is a real, dangerous failure
mode for this exact project.
