> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before 0.3 is done. Revisit and adjust when actually reached if
> it no longer fits your pace/gaps at that point.

# Project 04 — File Organizer Script

## Goal

Automate sorting a messy directory into subfolders by file type, building
on 0.3's argument parsing and functions. The real point isn't the sorting
logic — it's practicing the "check before you move/overwrite" discipline
from this session's dotfiles incident, applied to `mv` instead of symlinks.

## Environment

Same WSL2 Ubuntu shell. New repo, own `git init`, at
`~/00-foundations-project/0.4-file-organizer/`.

## Requirements

1. **`organize.sh`** — takes a target directory (argument, default to
   current directory if omitted).
2. Sorts files into subfolders by extension — at least 3 real categories
   (e.g. `images/`, `documents/`, `scripts/`) plus an `other/` catch-all.
3. **`--dry-run` flag** — prints what *would* move, without touching
   anything. Must actually leave the directory untouched, not just claim to.
4. **Conflict handling** — if a file already exists at the destination
   path, don't silently overwrite it; skip and report it clearly.
5. At least one bash function, actually used (not just present).
6. README.

## Acceptance criteria

- [ ] `organize.sh` exists, executable
- [ ] `--dry-run` output pasted, plus `ls` before/after proving nothing moved
- [ ] Real run pasted, files actually organized into the right subfolders
- [ ] Run it a **second time** against files already in place — paste
      output showing conflicts are detected and skipped, not clobbered
- [ ] At least one function defined and called
- [ ] `git log` shows iteration (more than one commit)
- [ ] README explains what it does and why, in your own words

## When done

Point me at the script + `git log`, and show the paste evidence above.
Say "review my code" for a real review — I'll check the dry-run actually
does nothing, and whether the conflict check is solid or just cosmetic.
