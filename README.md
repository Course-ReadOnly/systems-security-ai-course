# Systems → Security → AI Course

A self-paced, project-driven path from Linux fundamentals through C,
systems programming, security, and AI/LLMs — 100% free resources, real
projects at every stage, reviewed like actual engineering work rather
than rubber-stamped.

## Start here

| File | What it's for |
|---|---|
| [`ROADMAP.md`](ROADMAP.md) | The full stage-by-stage plan and every free resource used — the primary textbook |
| [`LEARNING_GUIDE.md`](LEARNING_GUIDE.md) | How to actually use this course: realistic time expectations, what to prioritize, evidence-over-self-reporting norms |
| [`STATUS.md`](STATUS.md) | Live progress: current stage/project, completed work, logged weak spots — the single source of truth for "where things are" |
| [`CLAUDE.md`](CLAUDE.md) | Operating instructions for Claude Code acting as instructor — pacing rules, review standards, teaching mode |
| [`SECURITY-CONCEPTS.md`](SECURITY-CONCEPTS.md) | Cross-cutting reference for the vulnerability classes/principles referenced throughout project specs' "Security relevance" sections |

## Structure

```
00-foundations/          Stage 0 — Linux, bash, git (see README.md inside)
01-c-programming/        Stage 1 — C
02-data-structures/      Stage 2
...
25-portfolio/            Stage 25 — final portfolio curation
```

Each stage folder has its own `README.md` (objectives, resources,
project list). Each project folder has a `SPEC.md` (goal, requirements,
acceptance criteria) and the learner's own solution alongside it.

`samples/` holds small reusable test fixtures for exercises that need
real input data.

## Using this with Claude Code

Open this repo in Claude Code — `CLAUDE.md` auto-loads and the assistant
picks up from `STATUS.md` automatically. Default pacing is one topic/
project at a time, reviewed before moving on; see `CLAUDE.md`'s golden
rules for the full operating model (and how to deliberately override the
default pacing if you want content generated further ahead).

## Forking this for your own use

See `LEARNING_GUIDE.md`'s "Forking this for yourself" section — short
version: keep `ROADMAP.md`/`CLAUDE.md`/`LEARNING_GUIDE.md` as-is, replace
`STATUS.md` with your own empty starting point, and resist the urge to
bulk-generate the whole course upfront even though the tooling allows it.
