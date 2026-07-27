> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 14.2 — Threat-Hunting Exercises

## Goal

Proactive hunting through logs for signs of compromise **without** a
rule already telling you what to look for — the skill that exists
because attackers adapt faster than signatures do. Uses LetsDefend's
free-tier exercises (or an equivalent sample-log source) as the raw
material.

## Requirements

1. Complete **at least 3 threat-hunting scenarios** on LetsDefend's free
   tier (or equivalent public sample-log exercises if LetsDefend access
   changes).
2. For each, document your **hunting process**: the hypothesis you
   started with, what you queried/looked at, what led you to the finding
   (or to ruling it out) — the process is the deliverable here, not just
   the final verdict.
3. At least one exercise should involve correlating **multiple** log
   sources/events to reach a conclusion (a single log line rarely tells
   the whole story in real incidents).

## Acceptance criteria

- [ ] 3+ documented hunting exercises, each with hypothesis → process →
      conclusion clearly laid out
- [ ] At least one demonstrates multi-source correlation explicitly
- [ ] `git log` shows iteration (write-ups committed as completed)

## When done

Point me at the write-ups + `git log`. I'll check whether the process
is actually reconstructable from your notes — could someone else follow
your reasoning and reach the same conclusion, or does the write-up skip
straight to an unexplained verdict?
