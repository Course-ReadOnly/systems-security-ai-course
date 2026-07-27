> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before 0.3/0.4/0.5 exist yet. This one is the most likely to need
> real revision once you're actually here, since it depends on the exact
> shape those three scripts end up taking. Treat this as a draft, not a
> contract.

# Project 06 — Capstone: Tying 0.1-0.5 Together

## Goal

One coherent entry point over everything built in Stage 0 — dotfiles,
workstation setup, the small automation scripts, the file organizer, and
the backup utility — instead of five disconnected tools you have to
remember how to invoke separately. This is the same composition pattern
0.2's `setup.sh` already used calling into 0.1's `install.sh`, just at
the scale of the whole stage.

## Environment

Same WSL2 Ubuntu shell. New repo, own `git init`, at
`~/00-foundations-project/0.6-capstone/`.

## Requirements

1. **`bootstrap.sh`** — a single script with subcommands, e.g.:
   - `bootstrap.sh setup` → calls 0.2's `setup.sh`
   - `bootstrap.sh organize <dir>` → calls 0.4's `organize.sh`
   - `bootstrap.sh backup <src> <dest>` → calls 0.5's `backup.sh`
   - `bootstrap.sh help` → usage for all subcommands
   (Exact subcommand set can flex based on what 0.3-0.5 actually ended up
   being — the point is one dispatcher, not duplicated logic.)
2. **No logic duplication** — `bootstrap.sh` calls into the existing
   scripts from 0.1-0.5 by path; it doesn't reimplement anything they
   already do.
3. Unknown subcommand → clear error + usage, non-zero exit (same
   discipline as 0.3's `args-demo.sh`).
4. README that ties the whole stage together: what each piece does, and
   how `bootstrap.sh` composes them.

## Acceptance criteria

- [ ] `bootstrap.sh` exists, executable, each subcommand actually invokes
      the corresponding 0.1-0.5 script (paste output proving it, not just
      the dispatch logic)
- [ ] Confirmed no duplicated logic — the real work still lives in the
      original per-project scripts
- [ ] Unknown-subcommand case pasted (error + usage + non-zero exit)
- [ ] `git log` shows iteration
- [ ] README summarizing the whole Stage 0 body of work

## When done

Point me at the script + `git log`. This closes out Stage 0 — expect a
short buffer/review session afterward targeting whatever's still logged
as a weak spot in STATUS.md before moving to Stage 1.
