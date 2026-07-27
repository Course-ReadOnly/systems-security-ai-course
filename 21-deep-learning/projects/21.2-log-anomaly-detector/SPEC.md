> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 21.2 — Log Anomaly Detector

## Goal

Apply deep learning to Stage 14's log-parsing domain: detect anomalous
sequences of log events using an RNN/sequence model, rather than
hand-written detection rules. This is explicit foreshadowing of Stage
23's "AI log analyzer" — a smaller, standalone version of that idea.

## Requirements

1. Uses your Stage 14 log parser (or a similar normalized log format) to
   produce sequences of events as model input.
2. Trains a sequence model (an RNN/LSTM, or a simpler autoencoder-based
   approach reconstructing "normal" sequences — either is a reasonable
   architecture choice, document which and why) to learn what "normal"
   log sequences look like.
3. Detects anomalous sequences — either injected synthetic anomalies
   (if a real labeled anomalous dataset isn't available) or real
   anomalies in a public log-anomaly dataset (e.g. HDFS/BGL datasets
   used in log-anomaly-detection research are a reasonable starting
   point).
4. Evaluated with precision/recall on detecting the known anomalies —
   same "not just accuracy" discipline as Stage 20, doubly important
   here since anomalies are by definition rare (severe class imbalance).
5. At least one detected anomaly inspected manually — does it correspond
   to something that would actually matter to a defender (tying back
   to Stage 14's threat-hunting framing)?

## Acceptance criteria

- [ ] Trains successfully on real or realistic log sequence data
- [ ] Precision/recall on anomaly detection reported, with the anomaly
      rate (class balance) stated explicitly
- [ ] At least one detected true-positive anomaly inspected and
      discussed for real-world relevance
- [ ] At least one false positive inspected — why did the model flag it,
      and is that a reasonable mistake or a sign of a modeling problem?
- [ ] `git log` shows iteration
- [ ] README explaining the sequence-model architecture chosen and why

## When done

Point me at the source + `git log` and the precision/recall results.
Given the severe class imbalance inherent to anomaly detection, I'll
check the evaluation metric choice hardest — accuracy alone would be
almost meaningless here, and I'll want to see that's understood, not
just avoided by convention.
