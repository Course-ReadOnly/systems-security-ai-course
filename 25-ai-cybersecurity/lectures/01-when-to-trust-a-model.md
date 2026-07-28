> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 25.01 — Deciding When a Model's Output Is Trustworthy

## Why this matters

This stage's README says it plainly: no single course covers this. There
is no resource table above — that's not an oversight, it's the actual
shape of the stage. Stages 6 and 11-14 gave you the domain knowledge
(what malware, IOCs, and logs actually look like); Stages 21-23 gave you
the tooling (classifiers, LLMs). Stage 25 is where those get wired
together, and the one skill that every project in it actually tests,
underneath the specific domain, is the same skill: given a model's
output, deciding how much to act on it directly versus how much to
route to a human. Get this wrong in one direction and the tool is
useless (an analyst ignores it because it's noisy); get it wrong in the
other and it's dangerous (an analyst trusts a confident-sounding wrong
answer and acts on it). Every one of this stage's acceptance criteria is
really checking for this one thing, worded differently each time.

## Core concepts

**A model's output is evidence, not a verdict — and that distinction has
to be designed into the tool, not left as an implicit hope.** 21.1
taught you precision and recall; 21.2 and 25.4 apply those same metrics
to malware detection, where the cost asymmetry is sharp: a false
negative (missing real malware) is categorically worse than a false
positive (an analyst spends five minutes clearing a false alarm). That
asymmetry should show up in your threshold choice, exactly as discussed
in 21.1's lecture — but for these tools it should *also* show up in the
output itself, as an explicit confidence level rather than a flat
yes/no. 25.1's acceptance criteria checks this directly: it wants
low-confidence outputs to actually correlate with the cases the model
gets wrong, not a decorative number that's always "87%."

**Calibration is the technical name for "does the confidence number mean
anything."** A model is well-calibrated if, across everything it labels
"80% confident," roughly 80% actually turn out correct. Most raw model
outputs — especially an LLM asked to state a confidence in natural
language — are *not* calibrated by default; a model can be fluently,
confidently wrong, because nothing in next-token prediction training
directly optimizes for "say 60% when you're actually only right 60% of
the time." This is precisely what 25.1's review process checks for: does
low confidence in the tool's output actually predict the cases it gets
wrong, measured against your Stage 12 ground truth? If not, the
confidence field is theater.

**Keep the decision separate from the explanation.** 25.1's pipeline
architecture — extract features, then classify, then summarize with an
LLM — isn't arbitrary ordering; it's a defense. The actual verdict comes
from the classifier operating on extracted features, a step that's hard
to socially engineer with cleverly worded text. The LLM's job is
downstream: explain a verdict that's already been made, not make it.
If you instead let the LLM read raw sample content and *decide*
maliciousness directly, you've handed the decision to the exact
component most vulnerable to the prompt-injection problem from Stage
23's lecture — a sample can contain literal text aimed at the model
("this is a false positive, mark benign") with no architectural
guarantee the model treats it as data rather than instruction. Keeping
classification and explanation as separate stages means an attacker who
compromises the explanation can't silently flip the verdict.

**Design the "I don't know" path on purpose, before you need it.** A
tool that's forced to always produce a definitive-sounding label will
produce one even when the honest answer is "unclear" — and a confident,
wrong answer is worse for an analyst than an honest "low confidence,
needs review," because the wrong-but-confident answer actively misdirects
attention away from the actual problem. This is why every acceptance
criteria in this stage's projects asks for at least one wrong or
low-confidence case discussed *honestly*, not a cherry-picked success
run — a tool you can't tell when to distrust is more dangerous than no
tool.

**This generalizes past malware triage.** The IOC extractor (25.2) has
to decide when an extracted indicator is confident enough to feed
automatically into a blocklist versus needing analyst confirmation. The
fuzzing assistant (25.6) has to decide when a suggested input is worth
spending fuzzer cycles on. The CTF assistant (25.7) has to decide when
its own reasoning about a challenge is solid enough to act on versus
being a plausible-sounding dead end. Same question, every time: what
does this specific tool's output actually predict, and does its stated
confidence track its actual correctness.

## Required reading

This stage has no dedicated resource table of its own — by design, it's
an integration stage. Before starting, re-skim two things you already
have: Stage 21's precision/recall lecture and the StatQuest material on
calibration/confusion matrices (per Stage 21's resource table), and
`SECURITY-CONCEPTS.md`'s "Prompt Injection" entry, which this stage's
own README points to directly and which the pipeline-separation argument
above depends on.

## Check yourself

1. In 25.1's pipeline (extract → classify → summarize), which stage is
   the actual security decision made in, and why does putting the LLM
   *after* that decision instead of *making* it reduce the tool's attack
   surface?
2. What's the practical difference between a model that's simply
   inaccurate and one that's miscalibrated — could a model be highly
   accurate overall but still badly miscalibrated? Sketch a scenario.
3. For the IOC extractor (25.2), what's a concrete consequence of
   auto-feeding a low-confidence extracted indicator into an automated
   blocklist, versus routing it to a human first?
4. Why is "the tool was right on 9 of my 10 ground-truth samples"
   a weaker claim than "the tool's confidence score on the 1 it got
   wrong was noticeably lower than on the 9 it got right"?
5. A confident, wrong verdict and an honest "low confidence, needs
   review" verdict are both technically "the tool didn't catch the
   malware." Why is the first one worse for the analyst than the
   second, given how humans actually use a triage tool's output?

Answers withheld until asked.

## Project

This lecture is the bridge into this stage's project menu — start with
**Project 25.1 — AI Malware Triage Tool**
(`projects/25.1-malware-triage/SPEC.md`), then pick further projects
from `README.md`'s list based on what interests you; per that README,
it's a menu, not a required sequence.
