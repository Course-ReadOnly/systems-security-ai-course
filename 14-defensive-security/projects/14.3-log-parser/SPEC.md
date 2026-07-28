> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 14.3 — Log Parser

## Goal

Build the tool that makes 14.2's manual hunting scale: a parser that
normalizes messy real-world logs (varying formats, timestamps,
encodings) into a consistent structure, queryable across log lines
instead of read one at a time.

Sample inputs are provided at `samples/access.log` (Apache/nginx
Combined Log Format, including a brute-force login pattern and a
SQLi-shaped query string — useful for the querying/filtering
requirement below) and `samples/access-corrupted.log` (the same log
with a few lines truncated/garbled — for the malformed-line
requirement) — a real public sample is still worth sourcing too if you
want more scale/variety.

## Requirements

1. Parses at least one real log format (e.g. Apache/nginx access logs,
   or Windows Event Log exports, or Zeek `conn.log` — pick one with
   available sample data).
2. Normalizes fields into a structured format (JSON/CSV) — consistent
   field names and timestamp format regardless of source-log quirks.
3. Handles malformed/partial lines gracefully (a truncated or corrupted
   log line shouldn't crash the whole parse — skip and count it, don't
   silently drop it either).
4. Supports basic querying/filtering after parsing (e.g. "show all
   entries from IP X," or "entries in this time range") — the payoff
   that makes normalization worthwhile.

## Acceptance criteria

- [ ] Parses a real (or realistic public sample) log file correctly —
      paste before (raw log) / after (normalized structured output)
- [ ] Malformed-line handling demonstrated: a deliberately corrupted log
      file parsed, with a count of skipped/malformed lines reported, not
      silently swallowed
- [ ] At least one query/filter demonstrated against the normalized
      output
- [ ] `git log` shows iteration
- [ ] README documenting the log format targeted and the normalized
      schema chosen

## Security relevance

Already directly stated in the "When done" note below, worth making
explicit: a log parser that silently drops malformed lines is a real,
easy-to-miss availability problem for security specifically — the one
dropped line in a threat-hunting context (Stage 14.2) could be the
exact evidence of an intrusion. Requirement 3's "skip and count, don't
silently drop" discipline is a small design choice with outsized
consequences once this tool sits between a defender and the truth.

## When done

Point me at the source + `git log`. I'll check the malformed-line
handling first — a log parser that silently drops bad lines without
telling you is dangerous in exactly the threat-hunting context this
project exists for (a dropped line could be the one that mattered).
