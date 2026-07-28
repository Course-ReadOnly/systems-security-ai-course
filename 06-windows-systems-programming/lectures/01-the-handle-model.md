> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 6.01 — The HANDLE Model

## Why this matters

Stage 5 taught you that a Unix file descriptor is a small integer
indexing into a per-process table that ultimately points at a kernel
object. Windows solves the *identical* problem — user-mode code needs a
safe way to refer to a kernel-managed resource — with `HANDLE`, and the
differences between the two designs aren't cosmetic. They're the reason
Windows malware analysis (Stage 12) and Windows internals work look and
feel so different from the Linux equivalent: opaque handles instead of
transparent integers, explicit per-handle reference counting instead of
invisible refcounting hidden behind a bare integer, and a kernel object
namespace that's far richer than "file."
Get this model straight now and every later Win32 API call — `CreateFile`,
`CreateThread`, `CreateEvent`, `OpenProcess` — reads as "yet another
`Create*`/`Open*` returning a `HANDLE` into the same table," instead of
a wall of unrelated-looking functions to memorize.

## Core concepts

**A `HANDLE` is Windows' answer to "how does user-mode code safely refer
to a kernel object" — same problem as a fd, deliberately opaque
solution.** Under the hood it's still an index into a per-process handle
table the kernel maintains, but Win32 treats the *value* as meaningless
to you — you never do arithmetic on a `HANDLE` or assume `0`/`1`/`2`
mean anything, the way you would with stdin/stdout/stderr on POSIX.
Every kernel object — a process, a thread, a file, a mutex, an event, a
registry key — gets referred to the same way: open or create it, get a
`HANDLE` back, operate on the object through that handle, close the
handle when done. This uniformity is why the Win32 API, despite its
sprawl, has a repeating shape once you notice it.

**Kernel objects are reference-counted, and a `HANDLE` is one reference.**
This is the sharpest divergence from POSIX. A Unix fd table entry is
just a pointer-ish reference with no count attached to the underlying
file *object* in the same way — closing the last fd to a file just
closes it. A Windows kernel object stays alive as long as *anything*
holds a reference to it, and a `HANDLE` in your process's handle table
is exactly one such reference. This is precisely why `CreateProcess`
handing you back *two* handles (one for the new process, one for its
initial thread) isn't redundant API design — they're two independent
references to two different kernel objects, and each has to be closed
independently, or each object's refcount never drops to zero and the
object survives leaked in the kernel long after you stop caring about it.
This is the exact mistake 6.1's grading callout warns about: forgetting
the thread handle specifically.

**A handle leak is a kernel resource leak, and it's directly
observable.** Every open handle costs kernel memory and shows up, per
process, in Task Manager's handle-count column (or Process Explorer).
This is what makes 6.1's acceptance criteria — loop your launcher many
times, watch the handle count — a real test and not busywork: a
correctly-written launcher's handle count returns to baseline after each
run; a leaking one climbs monotonically, and given enough iterations, a
process can genuinely exhaust its handle capacity.

**Failure is reported differently, and that difference matters more
than it looks.** POSIX syscalls return `-1` and set `errno`, a single
global(ish) integer with a small, well-known set of values you learn
once. Win32 calls typically signal failure via their return value
(`NULL`, `FALSE`, `INVALID_HANDLE_VALUE` depending on the function) and
you separately call `GetLastError()` to find out *why* — and that error
code is only meaningful immediately after the failing call, since the
next successful API call can overwrite it. `FormatMessage` turns the
numeric code into readable text. Skipping this and printing a bare error
number is the difference 6.1 is checking for when it asks for a "real,
readable error message."

## Required reading

Per the Stage 6 README's resource table: theForger's Win32 API Tutorial
for the hands-on process/handle basics, cross-referencing
`CreateProcess`, `WaitForSingleObject`, `GetExitCodeProcess`, and
`CloseHandle` in the official Microsoft Learn API reference as you use
each one — the tutorial gets you moving, the reference tells you exactly
what each parameter and return value means.

## Check yourself

1. `CreateProcess` returns handles to both the new process and its
   initial thread. Name the kernel object each one refers to, and
   explain why closing only one of them still leaves a leak.
2. Why doesn't closing a `HANDLE` necessarily destroy the kernel object
   it refers to? What has to be true for the object to actually go away?
3. If `CreateProcess` fails because the executable path is wrong, what's
   the correct sequence of calls to get a human-readable reason instead
   of just a numeric code — and why does the timing of that call (right
   after the failure, not later) matter?
4. Contrast a POSIX fd with a Windows `HANDLE`: name one thing that's
   valid to do with a fd's integer value that you should never rely on
   with a `HANDLE`'s value.
5. If your launcher runs in a loop and the handle count in Task Manager
   climbs by exactly 2 per iteration, what does that number specifically
   (as opposed to 1, or some other count) tell you about which handles
   you're forgetting to close?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 6.1 — Win32 Process Launcher**
(`projects/6.1-process-launcher/SPEC.md`). Start there.
