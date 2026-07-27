# Project 02 — Linux Workstation Setup Script

## Goal

Extend 0.1's symlink script into a real bootstrap script: one command that
takes a *bare* fresh Ubuntu/WSL2 install to your actual working environment —
packages installed, dotfiles linked, nothing done by hand. This is the
difference between "I have config files in a repo" (0.1) and "I can rebuild
my whole dev environment on a new machine in one shot" (0.2).

## Environment

Same WSL2 Ubuntu shell as 0.1. Test idempotency by actually re-running
against a machine that already has everything installed — don't just trust
that it would work.

## Requirements

1. **New script, `setup.sh`, in its own repo** at
   `~/00-foundations-project/0.2-workstation-setup/` — a sibling of
   `0.1-dotfiles-repo`, its own `git init`, not nested inside it.
2. **Package installation.** Use `apt-get install -y` for a real list of
   tools you actually want on a fresh box — at minimum: `git`, `curl`,
   `build-essential`, `vim`. Add more if you use them.
3. **Idempotency check before installing.** Don't blindly re-run
   `apt-get install` for everything every time — check whether a package/tool
   is already present first (`command -v` or `dpkg -s`), and skip with a
   message if so. This is the actual scripting skill this project is
   teaching: conditionals, not just a flat command list.
4. **Calls into 0.1's `install.sh`** for the symlink step, rather than
   duplicating that logic. `setup.sh` should be the outer script;
   `install.sh` stays the inner one it calls.
5. **Exit on failure.** Use `set -e` (or explicit `if` checks with useful
   error messages) so a failed `apt-get install` doesn't silently continue
   into a half-configured state.
6. **README update** describing what `setup.sh` does, in what order, and
   how it relates to `install.sh`.

## Acceptance criteria

- [ ] `setup.sh` exists, is executable, and running it on a machine that
      already has everything installed produces no errors and no duplicate
      work (idempotency, verified by actually re-running it — paste output)
- [ ] At least one real conditional check (`command -v` / `dpkg -s` / similar)
      gating an install step, not just a flat list of `apt-get install` calls
- [ ] Script exits non-zero on a real failure (test this: temporarily break
      something — e.g. a typo'd package name — and confirm it stops rather
      than plowing ahead)
- [ ] `install.sh` from 0.1 is called from `setup.sh`, not duplicated
- [ ] `git log` shows iteration (more than one commit)
- [ ] README explains what the script does and why, in your own words

## When done

Point me at the script + a `git log`, and show me: a clean first run, a
re-run against an already-configured machine (idempotency), and one
deliberately-broken run (failure handling). Say "review my code" and I'll
check error handling, quoting, and whether the idempotency checks are
actually correct or just happen to look right.
