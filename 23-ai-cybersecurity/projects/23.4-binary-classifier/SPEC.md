> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 23.4 — AI Binary Classifier

## Goal

Push Stage 20.2's classical-ML malware classifier toward Stage 21-style
deep learning, using **learned** features from raw binary content
(e.g. byte-sequence embeddings, or a CNN over a binary's byte-histogram/
image representation — a known research technique) instead of only
hand-engineered features.

## Requirements

1. A deep-learning model (not classical ML — that's 20.2) classifying
   malicious/benign using features learned from raw binary data, not
   fully hand-engineered ones.
2. Same rigor as 20.2/21.1: real train/test split, precision/recall/F1,
   stated class balance.
3. **Directly compares against your 20.2 classical model on the same
   test set** — does the deep-learning approach actually do better, and
   is the improvement worth its reduced interpretability? This
   comparison, honestly reported either way, is the actual point.
4. Same isolated-environment safety rules as Stage 12 for any real
   samples used.

## Acceptance criteria

- [ ] Trains successfully, isolated-environment confirmed for any real
      samples
- [ ] Precision/recall/F1 on a held-out test set, compared side-by-side
      against 20.2's results on the same split
- [ ] Honest discussion: did deep learning actually help here, or was
      20.2's simpler model comparable/better? Either answer is fine —
      an honest "it wasn't worth it" is a legitimate, valuable finding
- [ ] `git log` shows iteration
- [ ] README documenting the feature-learning approach used

## When done

Point me at the source + `git log` and the side-by-side comparison.
I want to see the comparison is genuinely apples-to-apples (same test
data, same metrics) — this is where the real learning value of this
project lives.
