> **Generated ahead of schedule** (2026-07-27, per learner request) —
> written before 0.3/0.4 are done. Revisit and adjust when actually reached
> if it no longer fits your pace/gaps at that point.

# Project 05 — Backup Utility Script

## Goal

A real backup script: archive a directory, verify the archive isn't
corrupt, and optionally prune old backups — safely. The retention/pruning
step is deliberately the centerpiece here, since it's a real `rm`-adjacent
operation and this session's dotfiles incident is the direct reason it
needs to be done carefully, not the reason to skip it.

## Environment

Same WSL2 Ubuntu shell. New repo, own `git init`, at
`~/00-foundations-project/0.5-backup-utility/`.

## Requirements

1. **`backup.sh`** — takes a source directory and a destination directory
   as arguments.
2. Creates a timestamped compressed archive of the source in the
   destination (`tar`/`gzip`), e.g. `backup-YYYYMMDD-HHMMSS.tar.gz`.
3. **Verifies the archive** after creation (e.g. `tar -tzf` to confirm it
   lists contents without error) before reporting success — don't just
   trust that `tar` exited 0.
4. **Retention**: keep only the N most recent backups in the destination,
   deleting older ones. The deletion **must** be scoped to files matching
   the exact backup naming pattern this script creates (a specific glob,
   e.g. `backup-*.tar.gz`) — never a blanket `rm -rf "$DEST"/*`. This is
   the concrete, load-bearing safety requirement of this project.
5. `set -e`, and a real failure test (e.g. a nonexistent source directory)
   confirming the script stops rather than continuing.
6. README.

## Acceptance criteria

- [ ] `backup.sh` exists, executable, produces a real `.tar.gz` archive
- [ ] Archive integrity check output pasted (proof it verified, not just
      assumed, the archive is good)
- [ ] Retention logic tested with more than N backups present — paste
      `ls` before/after showing only old *matching-pattern* backups were
      removed, nothing else in the destination touched
- [ ] Deliberately-broken run (bad source path) — paste output showing
      non-zero exit and no partial/corrupt archive left behind
- [ ] `git log` shows iteration (more than one commit)
- [ ] README explains what it does and why, in your own words

## When done

Point me at the script + `git log`, and show the paste evidence above.
Say "review my code" — I'll scrutinize the retention/deletion logic
hardest, since that's the part with real blast radius if it's wrong.
