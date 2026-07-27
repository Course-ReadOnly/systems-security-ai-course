# How to Use This Course

## Who this is for

Self-directed learners going Systems → Security → AI who are willing to
actually build the projects, not just read about them. See `ROADMAP.md`
for the full stage-by-stage plan and `CLAUDE.md` for how an AI instructor
(Claude Code) drives session-to-session teaching from `STATUS.md`.

## What this is, and isn't

- **`ROADMAP.md`** is the primary textbook — every resource linked there
  is free, and reading it is not optional. Anything generated per-stage
  (lectures, specs) is a thin *bridge*: why a topic matters, what to focus
  on vs. skim, and the project deliverable. It is deliberately not a
  rewrite of Beej's Guide, OSTEP, or whatever the actual source is.
- **This is not hand-holding.** Projects are mandatory checkpoints,
  reviewed for real bugs and bad patterns — not rubber-stamped. If a
  project gets skipped, that gets logged as a gap, not quietly absorbed.

## Realistic time expectations

Per `ROADMAP.md`'s own estimates: roughly **3–3.5 years part-time**
(10–15 hrs/week) or **13–17 months full-time**, end to end. Stopping
partway still leaves a real, portfolio-worthy skillset — most stages
stand on their own. Time estimates are cumulative per stage; add ~15%
buffer on top.

## Priority, not just sequence

Not every topic carries equal weight later, and the roadmap's ordering
alone doesn't tell you that. Two examples:

- C pointers/memory management (Stage 1) is load-bearing for nearly
  everything through Stage 12 (malware analysis) and beyond —
  underinvesting here compounds for years.
- Memorized filesystem trivia (Stage 0) is not load-bearing — skim it.

Each stage's `README.md` states its **Objectives** up front specifically
so you can tell foundational topics from merely-useful context. Weight
your study time toward what's flagged as foundational, not just what
comes first chronologically.

## Evidence, not self-reporting

Every project's acceptance criteria expects **pasted, real output** for
each claim — "idempotent" means "verified by actually re-running it and
showing the output," not "I tested it." This isn't busywork: it's the
actual professional habit, and skipping it here just means learning to
skip it somewhere the cost is much higher.

## Getting stuck is the point, up to a limit

This isn't designed to stop you from finding answers online — it's
designed so shortcuts now create gaps that cost more later. Escalating
hints instead of immediate solutions exist because working through the
stuck state *is* the skill being built, especially early on. If you're
using a different AI, or none, apply the same discipline yourself: several
genuine attempts and the linked resource before reaching for a full
solution.

## Security concepts, referenced not repeated

Most project specs — including ones well before the dedicated security
stages (11-14) — include a "Security relevance" section tying that
project's concept to a real vulnerability class or exploitation
technique. Rather than re-explain each concept inline every time it
recurs, those sections point to `SECURITY-CONCEPTS.md`, a single
reference covering memory safety, mitigation bypasses (and why ROP
exists), race conditions, injection, crypto misuse, and more. Read the
relevant entry when a spec points you there — it's meant to build a
coherent mental model across the whole course, not just decorate
individual projects with buzzwords.

## Sample data

`samples/` holds small, reusable test fixtures (sample text, etc.) for
exercises that need real input rather than inventing your own each time.
Stage-specific fixtures (sample source files, binaries, etc.) get added
under each stage as it's actually reached — not generated speculatively
ahead of time, since they're closer to project content than incidental
test data.

## Forking this for yourself

- Copy `ROADMAP.md`, `CLAUDE.md`, and this file as-is.
- Replace `STATUS.md` with your own — it's the one genuinely personal,
  session-state file, not template content.
- Stage folders can be scaffolded ahead (empty project directories are
  fine), but resist bulk-generating every `SPEC.md`/lecture up front just
  because you can. Content written far ahead of your actual pace tends to
  be generic and need rewriting anyway once your real gaps are visible —
  `CLAUDE.md`'s default is one topic at a time for exactly this reason.
