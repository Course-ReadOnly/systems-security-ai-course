> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 14.1 — Detection Rules (Sigma)

## Goal

Write real Sigma rules mapped to MITRE ATT&CK techniques — the standard,
tool-agnostic detection-rule format, translatable to a real SIEM's query
language. This turns Stage 13's exploitation techniques into things a
defender would actually be watching for.

## Requirements

1. Write **at least 4 Sigma rules**, each explicitly mapped to a
   specific MITRE ATT&CK technique ID.
2. At least one rule should detect a technique you personally exploited
   in Stage 13 (e.g. a specific web attack pattern, or a binary
   exploitation artifact) — closing the loop between attack and
   detection yourself.
3. At least one rule should be **behavioral** (suspicious argument
   patterns/parent-child process relationships for a legitimate system
   tool), not hash- or filename-based — see `SECURITY-CONCEPTS.md`'s
   "Living-Off-The-Land" entry for why hash-based detection is
   structurally blind to this entire attack style.
4. Test each rule against **both** a log sample that should trigger it
   and one that shouldn't (a true positive and a true negative case) —
   using Sigma's own testing tooling or a manual log-matching check.
5. Document, per rule, what specific log field/pattern it keys on and
   why that's a reasonable, not-overly-broad signal.

## Acceptance criteria

- [ ] 4+ Sigma rules, each with an ATT&CK technique ID cited
- [ ] At least one rule is behavioral (argument/parent-process pattern),
      not hash- or filename-based, with a note on why that's necessary
- [ ] Paste a true-positive test (sample log that should match, rule
      fires) and a true-negative test (log that shouldn't match, rule
      doesn't fire) for each rule
- [ ] At least one rule tied explicitly to something exploited in Stage
      13, with the connection documented
- [ ] `git log` shows iteration

## When done

Point me at the rules + `git log` and the test evidence. I'll check
specificity — same principle as Stage 12's YARA rules: a rule that also
fires on benign activity teaches analysts to ignore it.
