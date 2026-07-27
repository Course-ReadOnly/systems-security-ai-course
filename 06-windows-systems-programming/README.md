> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 6 — Windows Systems Programming

**Time budget:** 4–6 weeks part-time / 2 weeks full-time

## Objectives

Everything through Stage 5 is Linux/POSIX. This is the Windows
equivalent — same process/thread/IPC concepts, but the actual Win32 API
you'll need to read when reversing Windows binaries or analyzing Windows
malware later (Stages 12, 24). This stage was inserted specifically to
give Windows internals dedicated coverage rather than leaving it as a
bare mention elsewhere.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Win32 API fundamentals | [theForger's Win32 API Tutorial](http://winprog.org/tutorial/) |
| 02 | Official API reference | [Win32 API reference (Microsoft Learn)](https://learn.microsoft.com/en-us/windows/win32/api/) |
| 03 | Full systems tutorial | [tenouk Win32 Programming Tutorial](https://www.tenouk.com/ModuleC.html) |
| 04 | Kernel internals | [OpenSecurityTraining2 — Windows Kernel Internals](https://p.ost2.fyi/courses) |
| 05 | Kernel debugging | OpenSecurityTraining2 WinDbg mini-course |

**Topics:** the `HANDLE` model, `CreateProcess`/`CreateThread`,
synchronization primitives (mutexes, events, critical sections), DLLs and
the import/export table, the Windows Registry, named pipes, an intro to
kernel-mode internals (objects, syscalls, IRQL).

## Projects

| # | Project | Folder |
|---|---|---|
| 6.1 | Win32 process launcher | `projects/6.1-process-launcher/` |
| 6.2 | Custom DLL (build + load) | `projects/6.2-custom-dll/` |
| 6.3 | Process/module enumerator | `projects/6.3-process-enumerator/` |
