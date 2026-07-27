> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 5.1 — A Shell

## Goal

Build a real (if minimal) Unix shell: read a command line, `fork`/`exec`
it, wait for it, repeat. This is the canonical systems-programming
project — it's where `fork`/`exec`/`wait`, process groups, and signal
handling stop being lecture concepts and become things you debug at 2am.

## Requirements

1. REPL: read a command line, parse it, execute it, print any output,
   loop.
2. Supports built-in commands that must run in the shell's own process
   (not forked) — at minimum `cd` and `exit`.
3. Supports external commands via `fork` + `exec` + `waitpid` — the
   parent shell must not exit or hang while the child runs, and must
   correctly reap it.
4. **I/O redirection**: `>` and `<` at minimum.
5. **Pipes**: `cmd1 | cmd2` — a real pipeline, not string-substitution
   trickery.
6. Handles a command that doesn't exist (clear error, shell doesn't
   crash or hang) and `Ctrl-C` during a running child (interrupts the
   child, not the shell itself).

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Paste a session: a built-in (`cd`), an external command, output
      redirection, input redirection, and a real pipe (`ls | grep`-style)
      all working
- [ ] Nonexistent-command case pasted, handled cleanly
- [ ] `Ctrl-C` behavior demonstrated: interrupts a running child without
      killing the shell itself
- [ ] `valgrind` clean
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log` plus a session transcript. I'll check
zombie-process handling first (are children actually reaped via
`waitpid`, or do they pile up as zombies) and whether signal handling is
installed correctly for the parent vs. inherited by children as intended.
