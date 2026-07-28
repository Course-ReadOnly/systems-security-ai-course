> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 17.4 — Threat-Intel Collector

## Goal

Pull real, current threat-intel data from public feeds automatically —
the "keeps running and stays useful over time" project, as opposed to
17.1-17.3's one-shot analysis tools. Combines 17.2's normalization work
with real external data sources.

## Requirements

1. Pulls data from **at least one real, free/public threat-intel
   source** (e.g. a public IOC feed, an RSS feed of security advisories,
   or a public API with a free tier — research and pick one; document
   why you chose it).
2. Runs on a schedule (even just documented as "intended to run via
   cron," doesn't need to actually be deployed) — designed for repeated,
   automated execution, not a one-off manual run.
3. Normalizes incoming data using your 17.2 IOC parser's schema (reuse,
   don't duplicate) where applicable.
4. Handles the feed being temporarily unavailable/rate-limited gracefully
   — doesn't crash, logs the failure, can be safely re-run.
5. Avoids duplicate storage of the same intel across repeated runs (a
   real "collector" accumulates over time, it doesn't just re-fetch and
   duplicate everything each run).

## Acceptance criteria

- [ ] Runs successfully against a real, live public feed — paste actual
      current output (not a mocked/fake feed)
- [ ] Re-run demonstrated: running it twice in a row doesn't duplicate
      already-collected intel
- [ ] Feed-unavailable case simulated (e.g. point it at a bad URL
      temporarily) and shown to fail gracefully, not crash
- [ ] `git log` shows iteration
- [ ] README documenting the feed source, why it was chosen, and the
      intended run schedule

## Security relevance

A threat-intel collector is itself part of the security tooling supply
chain — feeding bad or duplicated data into downstream detection rules
(Stage 14) or blocklists degrades their quality the same way a noisy
YARA rule does. Requirement 4 (graceful failure on an unavailable feed)
matters because a collector that crashes instead of logging a missed
window creates a silent gap in intel coverage — exactly the kind of
failure that's invisible until someone asks "why didn't we know about
this indicator."

## When done

Point me at the source + `git log` and the live-feed output. I'll check
the deduplication logic and graceful-failure handling — a collector
that silently duplicates data or dies on the first network hiccup isn't
actually usable unattended, which is the whole point of this project.
