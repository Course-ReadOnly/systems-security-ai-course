> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 11.1 — Solve Crackmes (Write-ups)

## Goal

Deliberate, hands-on RE practice against purpose-built targets, with
real documentation of your process — not just "I got the flag." The
write-up is the actual deliverable; solving the crackme is what makes it
possible to write.

## Requirements

1. Solve **at least 5 crackmes** from crackmes.one, spanning a range of
   difficulty (check their difficulty ratings — don't pick 5 trivial
   ones).
2. For **each**, write a short analysis: what tool(s) you used (Ghidra/
   Radare2/gdb), what the binary's protection logic actually did, and
   the key insight that cracked it.
3. At least one crackme solved via **static analysis alone** (Ghidra/
   objdump, no running the binary) and at least one via **dynamic**
   analysis (gdb, actually stepping through execution) — both skills are
   required, not just whichever's more comfortable.
4. If any crackme includes anti-debugging tricks (timing checks,
   `ptrace`-based self-detection, etc. — check
   `SECURITY-CONCEPTS.md`'s "Anti-Analysis" entry if one trips you up),
   document how you identified and worked around it — that's often the
   actual interesting part of the write-up, not the final flag.

## Acceptance criteria

- [ ] 5+ crackmes solved, each with a written analysis (a markdown file
      per crackme is a reasonable format)
- [ ] At least one write-up is explicitly static-only, one explicitly
      dynamic — noted as such
- [ ] Each write-up includes the actual key/input that satisfies the
      crackme, plus *why* it works (the logic you reverse-engineered),
      not just the answer
- [ ] `git log` shows iteration (one commit per crackme is reasonable)

## When done

Point me at the write-ups + `git log`. I'll check whether the
explanations actually demonstrate understanding of the binary's logic,
versus just reporting a found string/patched byte without explaining
why it worked.
