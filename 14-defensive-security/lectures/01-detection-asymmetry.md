> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 14.01 — The Detection Asymmetry

## Why this matters

Stage 13 taught you to find *one* working path in. This stage asks a
structurally harder question: how does a defender, who has to cover
*every* path in, actually do that with finite time and finite log
volume? The honest answer is they mostly can't — not completely — and
almost every design decision in modern detection engineering (Sigma,
ATT&CK, behavioral rules over hash lists) is a direct response to that
asymmetry. Understanding *why* the field is shaped this way is what
lets you write a detection rule that survives contact with a real
attacker instead of one that only catches the exact sample you tested
it against.

## Core concepts

**The attacker only needs one working technique; the defender has to
have coverage for all of them.** This isn't a minor disadvantage, it's
the central fact that shapes the entire field. It means a defender
can't just "watch for bad things" — the search space of possible bad
things is enormous and constantly growing, so detection engineering is
really the discipline of *prioritizing* which small slice of that space
is worth writing rules for, and accepting that the rest is a gap by
necessity, not by oversight.

**MITRE ATT&CK exists to make that prioritization tractable.** It's a
taxonomy of *behaviors* attackers actually use in the real world
(credential dumping, living-off-the-land binary abuse, lateral
movement via a specific protocol), organized by tactic (why an attacker
does it) and technique (how). The payoff: instead of defending against
an infinite space of possible malware, you defend against a finite,
documented, continuously-updated space of *behaviors* — and you can
honestly say "we have detection coverage for technique T1055" instead
of a vague "we have antivirus."

**Signature-based detection (hash or filename matching) is cheap and
brittle in exactly the way this asymmetry punishes.** A file hash
identifies one specific binary. Rename the file, recompile it, flip a
byte — new hash, same malware, detection gone. Signature matching
optimizes for the case an attacker controls completely (their own
file), which is the worst possible thing to optimize for given they
only need to change it once to slip past you.

**Behavioral detection targets what's actually expensive for the
attacker to change: what the technique has to *do* to work.** A
credential-dumping technique has to touch LSASS memory somehow,
regardless of which specific tool does it or what that tool is named
today. A living-off-the-land attack abuses a legitimate, already-
trusted system binary (`powershell.exe`, `certutil.exe`) specifically
*because* it won't show up on any malware hash list — but its
*argument patterns* and *parent-process relationships* (a Word process
spawning PowerShell with an encoded command, say) are much harder for
the attacker to disguise without also breaking the technique. That's
the actual content of the "behavioral, not hash-based" requirement in
14.1's spec — see `SECURITY-CONCEPTS.md`'s "Living-Off-The-Land
(LOLBins) and Signature Evasion" entry for the full picture. This is
also why the asymmetry never fully closes: behavioral rules are more
durable than hashes, but a patient attacker can still study a
published Sigma rule and adjust the behavior just enough to fall
outside its specific field/threshold — detection engineering is an
arms race, not a solved problem.

**Sigma is the format that makes a detection idea portable.** A rule
written once, in Sigma's generic YAML structure (a log source, a
selection of field/value conditions, a condition combining them),
translates into a specific SIEM's query language (Splunk SPL, Elastic
DSL, etc.) via a backend converter. Writing your logic in Sigma instead
of directly in one tool's query syntax means the detection idea
outlives any one product — closer to how you'd write portable C
instead of one compiler's inline-assembly extension.

**A rule's specificity is the whole game.** A rule that also fires on
normal admin activity trains analysts to ignore its alerts — the same
failure mode as a YARA rule from Stage 12 that matches too broadly.
14.1 explicitly requires a true-positive *and* true-negative test per
rule for exactly this reason: a rule you've only confirmed fires on the
bad case, and never confirmed it *doesn't* fire on a normal case, is
unverified in the direction that actually matters in production.

## Required reading

Per this stage's `README.md` resource table: [MITRE
ATT&CK](https://attack.mitre.org/) — browse the technique pages for
whichever tactic (e.g. Credential Access, Execution) you plan to write
a rule against first, then the [Sigma project](https://github.com/SigmaHQ/sigma)
repo's rule-writing documentation for the YAML structure itself.

## Check yourself

1. Why is a hash-based detection rule structurally worse-suited to
   this asymmetry than a behavioral one, even though a hash rule is
   easier to write and produces fewer false positives when it does
   match?
2. What does mapping a Sigma rule to a specific ATT&CK technique ID
   buy you, organizationally, beyond just documentation — think about
   what a security team can now measure that they couldn't before?
3. LOLBin abuse specifically exploits a system binary already being
   trusted. What has to be true about that binary's *normal* usage
   pattern for a behavioral rule targeting it to stay specific instead
   of drowning in false positives?
4. If a Sigma rule you wrote for a technique you exploited in 13.1
   would also have fired on your own legitimate use of the same tool
   during normal work, what does that tell you about the rule?
5. The detection asymmetry means gaps are inevitable, not just
   possible. Given that, what's the actual argument for writing
   detection rules at all, rather than treating full coverage as the
   goal and giving up when it's unreachable?

Answers withheld until asked — work through 14.1's rule-writing first;
the true-positive/true-negative testing requirement is where most of
these stop being abstract.

## Project

This lecture is the bridge into **Project 14.1 — Detection Rules
(Sigma)** (`projects/14.1-detection-rules/SPEC.md`). Start there.
