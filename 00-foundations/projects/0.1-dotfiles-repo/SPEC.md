# Project 01 — Dotfiles Repo

## Goal

Turn your shell/editor configuration into a version-controlled, reproducible
setup. This is the first "real" Linux CLI habit: don't configure a machine
by hand and lose it, track it in Git and be able to rebuild it anywhere.

## Environment

Do this inside your WSL2 Ubuntu shell (from Lecture 01), not Windows.

## Requirements

1. **Git repo.** Create `~/dotfiles`, `git init` it. It does not need a
   remote yet, but you can push it to GitHub if you want a backup.
2. **Track at least these files:**
   - `.bashrc` (or `.zshrc` if you switch shells later)
   - `.gitconfig`
   - `.vimrc` or your editor's config (even a minimal one)
3. **Use symlinks, not copies.** The files under version control in
   `~/dotfiles` should be the *actual* files your shell reads — done via
   symlinks from `$HOME` into the repo. Two acceptable approaches:
   - **Plain `ln -s`**, done manually or via your own small install script.
     This is the most educational route: you'll actually understand what a
     symlink is and how `$HOME` resolves config, with zero abstraction.
   - **GNU Stow.** A tiny tool built exactly for this — organizes dotfiles
     into per-tool package directories and symlinks them into `$HOME` with
     one command (`stow bash`, `stow git`, ...). Slightly less manual typing,
     still teaches real symlinks underneath. Reasonable if you want the repo
     to look clean as it grows.
   Skip full-featured managers like chezmoi for now — they add templating
   and a config layer that hides the mechanics this project exists to teach.
   Revisit chezmoi later if you're managing dotfiles across multiple machines.
4. **`install.sh` script.** A script that, run on a fresh machine, sets up
   all the symlinks (i.e. reproduces your environment from a clean clone).
   This is the actual "systems programming habit" this project is teaching:
   idempotent, rerunnable setup scripts.
5. **README.md** in the repo describing what's in it and how to run
   `install.sh`.

## Acceptance criteria

- [ ] `~/dotfiles` is a git repo with at least 3 tracked config files
- [ ] Config files in `$HOME` are symlinks pointing into `~/dotfiles`, not copies
      (verify with `ls -la ~` — symlinks show as `file -> target`)
- [ ] `install.sh` exists, is executable (`chmod +x`), and running it on a
      clean checkout recreates the symlinks without manual steps
- [ ] `git log` shows more than one commit — i.e. you iterated, not one dump
- [ ] README explains the setup in your own words

## When done

Point me at the repo (path or paste `install.sh` + a `git log` /
`ls -la ~` output) and say "review my code" — I'll check symlink correctness,
script idempotency (does re-running it break anything?), and general Bash
hygiene (quoting, `set -e`, etc. — some of this is Stage 0 Lecture 03
territory, don't worry if it's rough yet).

## Sources consulted for this spec

- [Why GNU Stow for dotfile management](https://rickcogley.github.io/dotfiles/explanations/gnu-stow.html)
- [Best Dotfile Managers for a Portable Dev Setup (2026)](https://briandetering.net/2026/06/25/best-dotfile-managers-2026/)
