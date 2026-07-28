> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 25 — AI × Cybersecurity

**Time budget:** 6–8 weeks part-time / 3 weeks full-time

## Objectives

No single course covers this — it's an integration stage combining
Windows/RE/malware/detection knowledge (Stages 6, 11-14) with the
ML/LLM tooling built in Stages 21-23. Every project here should feel
like "a real tool from an earlier stage, made significantly more capable
by adding a model on top" — not an AI demo bolted onto nothing.

## Projects

| # | Project | Folder |
|---|---|---|
| 25.1 | AI malware triage tool | `projects/25.1-malware-triage/` |
| 25.2 | AI IOC extractor | `projects/25.2-ioc-extractor/` |
| 25.3 | AI log analyzer | `projects/25.3-log-analyzer/` |
| 25.4 | AI binary classifier | `projects/25.4-binary-classifier/` |
| 25.5 | AI decompiler helper | `projects/25.5-decompiler-helper/` |
| 25.6 | AI-powered fuzzing assistant | `projects/25.6-fuzzing-assistant/` |
| 25.7 | AI CTF assistant | `projects/25.7-ctf-assistant/` |

Seven projects is a lot — treat this as a menu to draw from rather than
a strict must-do-all-seven list, similar to Stage 1's easy/medium/hard
framing. Pick the ones that connect to what interests you most; each
one stands alone.

**Same prompt-injection caution as Stage 23 applies here, more sharply**
— these tools sit even closer to real security decisions (triage
verdicts, IOC extraction, fuzzing guidance). See
`SECURITY-CONCEPTS.md`'s "Prompt Injection" entry.
