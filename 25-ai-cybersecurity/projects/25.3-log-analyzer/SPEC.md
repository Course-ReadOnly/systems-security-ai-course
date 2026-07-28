> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 25.3 — AI Log Analyzer

## Goal

Extend Stage 22.2's log-anomaly-detector and 23.3's threat-hunting
assistant into one combined tool: the deep-learning anomaly detector
flags candidates, the LLM explains *why* each one is anomalous in plain
language a human can quickly evaluate — combining a statistical signal
with a natural-language explanation layer.

## Requirements

1. Pipeline: 22.2's (or an extended) anomaly-detection model flags
   candidate anomalous log sequences → an LLM generates a plain-English
   explanation of what's unusual about each flagged sequence, grounded
   in the actual log content (RAG-style, same discipline as 23.3).
2. Explanation must reference the **actual specific log fields/values**
   that triggered the anomaly flag — not a generic "this seems unusual"
   non-explanation.
3. Evaluated on real or realistic log data with known anomalies (reuse
   22.2's evaluation data), checking both detection quality (precision/
   recall, from 22.2) and explanation quality (do the explanations
   actually match what's really anomalous, on manual review).

## Acceptance criteria

- [ ] Full pipeline runs end-to-end
- [ ] Paste at least 3 flagged anomalies with their generated
      explanations, and your assessment of whether each explanation is
      actually accurate/specific
- [ ] At least one case where the explanation was vague/wrong,
      discussed honestly
- [ ] `git log` shows iteration
- [ ] README documenting the pipeline

## When done

Point me at the source + `git log`. I'll check explanation specificity
hardest — a generic explanation that would apply to any anomaly isn't
actually adding value over the raw detection signal from 22.2 alone.
