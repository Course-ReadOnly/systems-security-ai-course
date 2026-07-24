# Lecture 01 — Linux Terminal & CLI

## Why this matters

Nearly every resource from here through Stage 23 assumes a Linux (or
Linux-like) shell: compilers, debuggers, `man` pages, wargames, CTF
challenges, kernel source. Get fluent now and every later stage moves
faster; stay shaky here and you'll be fighting the environment instead of
the material for years.

## Core concepts

**You're on Windows — set up a real Linux environment first.** Don't try to
learn Linux CLI through Git Bash or PowerShell aliases; it'll teach you
wrong muscle memory.

1. Install **WSL2** (Windows Subsystem for Linux) with Ubuntu:
   ```
   wsl --install -d Ubuntu
   ```
   Run from an elevated PowerShell, reboot if prompted. This gives you a
   real Linux kernel, not an emulation layer — Bandit, GDB, Valgrind, GCC
   all behave exactly as they would on a native Linux box.
2. From now on, "the terminal" in this course means your WSL2 Ubuntu shell,
   not PowerShell. VS Code has a WSL extension that lets you edit files
   living in the Linux filesystem directly — install it.

**Filesystem model.** Everything is a file, rooted at `/`. No drive letters.
Key locations: `/home/<you>` (your stuff), `/etc` (system config), `/usr/bin`
and `/bin` (programs), `/var/log` (logs), `/tmp` (scratch, wiped on reboot).
`~` is shorthand for your home directory.

**Permissions.** Every file has an owner, group, and mode (`rwx` for
owner/group/others). `ls -l` shows them. `chmod` changes them. You'll hit
"permission denied" constantly until this clicks — it's not a bug, it's the
security model working.

**Processes.** Everything you run is a process with a PID. `ps`, `top`,
`kill` are how you inspect and manage them. Foreground vs background (`&`,
`jobs`, `fg`, `bg`) matters once you're running servers/scripts later.

**The core toolkit you need fluent, not just "seen once":**
`ls`, `cd`, `pwd`, `cp`, `mv`, `rm`, `mkdir`, `find`, `man`, `cat`, `less`,
`grep`, `chmod`, `chown`, `ps`, `kill`, `df`, `du`, `tar`, `ssh`, `curl`,
`wget`, `apt` (Ubuntu's package manager).

**Piping and redirection** (`|`, `>`, `>>`, `<`, `2>`) is the single most
important habit for CLI fluency — it's how Unix tools compose instead of
each needing its own built-in feature set. Spend real time here.

## Required reading

[Linux Journey](https://linuxjourney.com/) — work through the **"Grasshopper"**
track in full (filesystem, permissions, users, processes) before moving on.
It's interactive; do the exercises, don't just read.

## Check yourself

1. What's the difference between `/bin`, `/usr/bin`, and `~/bin`?
2. You run `chmod 750 script.sh`. What can the owner do? The group? Everyone
   else?
3. What does `grep -r "TODO" . | wc -l` do, piece by piece?
4. Why does `rm -rf /` (or worse, a typo'd `rm -rf /*`) matter so much on
   Linux specifically, compared to deleting files in a GUI?
5. What's the difference between killing a process with `kill <pid>` vs
   `kill -9 <pid>`?

Don't answer these to me unprompted — ask when you want to check your
understanding, or I'll fold them into the project review.

## Project spec

See `../projects/0.1-dotfiles-repo/SPEC.md` (say "start project" when ready).
