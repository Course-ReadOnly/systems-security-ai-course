> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 17.2 — IOC Parser

## Goal

A Python reimplementation/extension of Stage 12's IOC extractor — but
now built to parse **structured threat-intel formats** (e.g. STIX/TAXII-
style JSON, or simpler CSV feeds) rather than just raw strings out of a
binary. The shift here is from "extract indicators from one sample" to
"normalize indicators from many different external sources."

Sample inputs are provided at `samples/stix-bundle.json` (a simplified
STIX 2.1-shaped bundle) and `samples/feed.csv` (a plain CSV feed) — one
IP indicator deliberately appears in both, formatted differently (plain
vs. `/32` CIDR), specifically to exercise the normalize-before-dedup
requirement below. All values are synthetic (RFC 5737 documentation IP
ranges, `.test` domains) — not real infrastructure or malware.

## Requirements

1. Parses IOCs from at least two different structured input formats
   (e.g. a STIX bundle and a plain CSV feed) into one common internal
   representation.
2. Normalizes indicator types consistently (an IP is always represented
   the same way regardless of which input format it came from).
3. Deduplicates indicators that appear across multiple input sources.
4. Outputs a single, unified report (JSON/CSV) combining all sources.

## Acceptance criteria

- [ ] Runs cleanly against real or realistic sample data in both input
      formats, paste the unified output
- [ ] Deduplication demonstrated: an indicator appearing in both input
      sources shows up once in the output, not twice
- [ ] `git log` shows iteration
- [ ] README documenting the two input formats supported and the common
      internal schema chosen

## Security relevance

Normalization correctness (Requirement 2) has real consequences at
scale: a blocklist that treats `203.0.113.5` and `203.0.113.5/32` as
two different indicators because normalization missed a CIDR-notation
case fails to actually block the second occurrence — a false sense of
coverage is worse than an obviously incomplete one. This is the same
class of consistency problem as 21.x's ML feature engineering, applied
to threat-intel plumbing instead of model inputs.

## When done

Point me at the source + `git log`. I'll check the normalization logic
— is an IP really recognized as the same indicator regardless of source
formatting quirks (leading zeros, CIDR notation vs. plain, etc.)?
