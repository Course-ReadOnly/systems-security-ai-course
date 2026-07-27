# Project 03 — Small Bash Automation Scripts

## Goal

0.1 and 0.2 were both "loop over a fixed array" shaped. This project is
smaller, separate reps targeting bash skills neither of those exercised:
argument/flag parsing, functions, and text processing. Last stop before
0.4/0.5, which are each one bigger single-purpose automation script.

## Environment

Same WSL2 Ubuntu shell. New repo, own `git init`, at
`~/00-foundations-project/0.3-bash-automation/`.

## Requirements

Three small, separate scripts in the repo:

1. **`args-demo.sh`** — accepts command-line flags via `getopts` (e.g. `-n
   NAME` for a required name, `-v` for a verbose flag, `-h` for help).
   Must handle: a missing required flag (error + usage message, non-zero
   exit), an unknown flag (error + usage), and `-h` (prints usage, exits
   0).
2. **`word-count.sh`** — takes a file path as an argument and reports
   something non-trivial about it using `grep`/`sed`/`awk` (e.g. word
   frequency, longest line, count of lines matching a pattern) — not just
   a thin wrapper around `wc`.
3. **`confirm-rm.sh`** — a safety-focused script: takes a path, checks
   what it actually is (`-L`/`-d`/`-f` tests) before touching it, and
   requires an explicit typed confirmation (not a bare `-y` flag) before
   deleting anything. This is the "check before you `rm -rf`" habit from
   this session's dotfiles incident, made concrete. Must define and call
   at least one bash **function**.

## Acceptance criteria

- [ ] All three scripts exist, are executable, and each does what its
      section above describes
- [ ] `args-demo.sh`: paste output for a valid call, a missing-required-
      flag call, and `-h`
- [ ] `word-count.sh`: paste output run against a real file
- [ ] `confirm-rm.sh`: paste output for both a confirmed delete and a
      declined one — a decline must leave the target untouched, proven
      with `ls`/`cat` before and after, not just claimed
- [ ] At least one bash function defined and called (not just inline loop
      bodies copy-pasted between scripts)
- [ ] `git log` shows iteration (more than one commit)

## When done

Point me at the three scripts + `git log`, and show the paste evidence
above. Say "review my code" and I'll check argument handling, quoting,
and whether `confirm-rm.sh`'s safety check is actually solid or just
cosmetic.
