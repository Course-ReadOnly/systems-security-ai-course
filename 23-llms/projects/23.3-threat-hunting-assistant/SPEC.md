> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 23.3 — Threat-Hunting Assistant

## Goal

An LLM-backed assistant over Stage 14's log/hunting domain — given
normalized logs (your 14.3 log parser's output) and a natural-language
question ("show me anything unusual from host X last week"), help
surface candidates for a human analyst to investigate. This is a RAG-
shaped project: the LLM needs *your actual log data* as grounding, not
just its training knowledge.

## Requirements

1. Uses **retrieval** over your actual normalized log data (from 14.3)
   — the LLM must be answering based on real log content you provide it
   (via RAG/context injection), not general knowledge about what logs
   "usually" look like.
2. Accepts natural-language questions about the log data, returns
   relevant log entries/summaries as the answer, not just a generic
   LLM response disconnected from the actual data.
3. Explicitly cites which log entries its answer is based on — an
   analyst needs to verify, not just trust, any AI-surfaced finding.
4. Handles a question with no relevant matches in the data honestly
   ("no matching entries found," not a fabricated-sounding answer).

## Acceptance criteria

- [ ] Runs successfully against your real 14.3 log output
- [ ] Paste at least 3 real natural-language queries with answers,
      **each citing the specific underlying log entries** used
- [ ] A no-match query tested, confirmed to say so honestly rather than
      inventing a plausible answer
- [ ] `git log` shows iteration
- [ ] README documenting the retrieval approach (how log data gets into
      the LLM's context)

## When done

Point me at the source + `git log`. I'll check that answers are
genuinely grounded in the retrieved log data (not just plausible-
sounding LLM output loosely related to the question) and that citations
actually point at real, correct source entries.
