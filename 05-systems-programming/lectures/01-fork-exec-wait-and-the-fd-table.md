> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 5.01 — fork/exec/wait and the FD Table

## Why this matters

Almost every project in this stage — the shell (5.1), the thread pool
(5.3), the HTTP server (5.4/5.5) — is really the same handful of
primitives recombined: a process gets created, its file descriptors get
rearranged, it runs, someone waits for it. Get comfortable with that
combination here and Stage 8's kernel-side view of the same mechanism
(how `fork` is actually implemented, what a context switch does to make
it possible) will read as "oh, I already know what this does, now I get
to see how" instead of new material. It's also the direct ancestor of
Stage 6's Win32 process model — same problem, deliberately different
API shape, and the contrast is the point of that stage.

## Core concepts

**`fork()` doesn't start a new program — it clones the current one.**
The child is a near-exact copy of the parent's memory, registers, and
open file descriptor table, differing only in return value (`0` in the
child, the child's PID in the parent) and PID. This is the part people
find weird: nothing has "started running" yet in any new-program sense —
you now just have two processes executing the same code from the same
point, diverging based on that one return value.

**`exec()` doesn't create a process — it replaces one.** It swaps out
the calling process's code, data, and stack for a different program's,
*in place*, keeping the same PID. The `fork()` + `exec()` split (instead
of one "spawn a new program" call) is what makes Unix flexible: because
they're separate steps, you get to do arbitrary setup *in the child*,
after the clone but before the replacement — which is exactly how
redirection works (see below). Windows collapses this into a single
`CreateProcess` call instead, which is a large part of why Stage 6 feels
so different even though it's solving the same problem.

**The file descriptor table is what fork() copies and exec() (mostly)
doesn't touch.** A file descriptor is just a small integer, an index
into a per-process table of open files/pipes/sockets — fd 0, 1, 2 are
stdin/stdout/stderr *by convention only*, not by anything the kernel
enforces. `fork()` copies this table (both processes now have their own
fd 1, both pointing at the same underlying open file description).
`exec()` normally *preserves* open fds across the program swap — this
one fact is the entire mechanism behind shell redirection: to make a
child's stdout go to a file, you `close(1)` (or `dup2()` onto fd 1) in
the child *after forking, before exec'ing*. The child's fd 1 now points
somewhere else; the new program, once exec'd, writes to fd 1 exactly
like it always would, having no idea it's not talking to a terminal. A
pipe (`cmd1 | cmd2`) is the identical trick done twice: `pipe()` creates
a connected read/write fd pair, and you `dup2` the write end onto
`cmd1`'s stdout and the read end onto `cmd2`'s stdin, in each respective
child, before each `exec`.

**`wait()`/`waitpid()` is not optional — it's how the kernel frees a
dead process's last resources.** When a child exits, it doesn't fully
disappear; it becomes a *zombie*, keeping its exit status around until
the parent reaps it with `wait()`. A parent that forks and never waits
leaks zombie entries in the process table — a real, observable resource
leak, not a theoretical one. This is the first thing worth checking in
any shell you write: does every forked child eventually get `waitpid`'d?

**Signals are asynchronous and inherited, which is why `Ctrl-C` in a
shell is subtle.** `SIGINT` goes to the foreground process group, which
by default includes children — so if you do nothing, both your shell
and the child it launched receive it. A shell that wants to survive
`Ctrl-C` while its child dies from it has to deliberately manage this
(e.g. via process groups and/or ignoring `SIGINT` in the parent while
leaving the child's disposition alone). This is exactly what 5.1's
acceptance criteria is checking for.

## Required reading

Per the Stage 5 README's resource table: work through CS:APP (CMU
15-213) — specifically the chapters covering "Exceptional Control Flow"
(processes, `fork`, `exec`, signals) and "System-Level I/O" (file
descriptors, `dup2`). If CS:APP's pace doesn't click, Stanford CS107
covers the same ground as an alternative full course.

## Check yourself

1. Right after `fork()` returns, name one thing that is now *shared*
   between parent and child, and one thing that looks identical but is
   now independently owned by each.
2. Why does redirection have to happen *between* `fork()` and `exec()`
   specifically — what would go wrong if you tried to redirect stdout
   before forking, or after exec'ing?
3. If a parent forks ten children and calls `wait()` only three times
   before exiting, what happens to the other seven? Is this actually a
   memory leak in the traditional sense?
4. In a real pipe (`ls | grep foo`), which process's fd table has the
   pipe's *write* end wired to stdout, and which has the *read* end
   wired to stdin — and why must the unused end of the pipe be closed in
   each child?
5. Concretely, what has to be different about how your shell handles
   `SIGINT` for itself versus for a running child, for `Ctrl-C` to kill
   the child without killing the shell?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 5.1 — A Shell**
(`projects/5.1-shell/SPEC.md`). Start there.
