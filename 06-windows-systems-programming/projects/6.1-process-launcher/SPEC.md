> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 6.1 — Win32 Process Launcher

## Goal

The Windows-native version of Stage 5's `fork`/`exec`/`wait`: spawn a
process, wait for it, capture its exit code — but via `CreateProcess`
and the `HANDLE` model instead of POSIX primitives. The point is feeling
the difference: Windows makes you manage handles explicitly where POSIX
gives you integer file descriptors/PIDs.

## Requirements

1. Spawns a child process via `CreateProcess` (not `system()` — that's
   cheating the point of this project).
2. Waits for it to finish via `WaitForSingleObject` on its process
   `HANDLE`.
3. Retrieves and prints the child's exit code (`GetExitCodeProcess`).
4. Correctly closes every `HANDLE` it opens (process and thread handles
   from `CreateProcess` are **two separate handles** — both need
   closing) — no handle leaks.
5. Handles a launch failure (bad executable path) with a clear error
   using `GetLastError`/`FormatMessage`, not a silent failure.

## Acceptance criteria

- [ ] Builds cleanly (MSVC or MinGW, your choice — document which)
- [ ] Paste output launching a real program and printing its correct
      exit code (test with a program you control the exit code of)
- [ ] Handle-leak check: use Task Manager's handle-count column (or
      Process Explorer) before/after running your launcher many times in
      a loop — paste evidence handle count returns to baseline, not
      climbing
- [ ] Launch-failure case pasted, with a real, readable error message
      (not just a raw error code)
- [ ] `git log` shows iteration

## Security relevance

`CreateProcess`'s path handling is where the real-world **"unquoted
service path"** vulnerability class comes from: if a path containing
spaces (`C:\Program Files\App\app.exe`) is ever passed unquoted, and an
attacker has write access to any parent directory in that chain
(`C:\Program.exe`, `C:\Program Files\App.exe`), Windows will try each
space-delimited segment as a candidate executable before reaching the
real one — a real, commonly-exploited local privilege-escalation
pattern. Always quote the full path, and never build it by
concatenating untrusted input. Handle leaks matter here too, beyond
tidiness: a process that leaks handles under attacker-controlled load
is a real (if unglamorous) denial-of-service vector once the handle
table fills up.

## When done

Point me at the source + `git log` plus your handle-count evidence.
I'll check that both the process and thread handles from `CreateProcess`
are actually closed — forgetting the thread handle specifically is the
most common mistake here.
