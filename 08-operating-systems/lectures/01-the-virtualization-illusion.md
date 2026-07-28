> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 8.01 — The Virtualization Illusion

## Why this matters

Stages 5-7 taught you the *user-mode view* of processes, memory, and
registers — the API surface. This stage takes you underneath it: xv6 is
small enough (a few thousand lines) that you can read the actual code
that makes `fork()`, virtual addresses, and file descriptors real,
instead of trusting they work. That's not just satisfying — it's the
last piece this course needed before Stage 11 (Reverse Engineering) and
Stage 12 (Malware Analysis) start asking you to reason about kernel-mode
behavior, privilege boundaries, and syscall handling directly. If you've
never seen a trap handler, "the kernel intercepts this" stays an
abstraction; after 8.1-8.3, it's code you've read and modified.

## Core concepts

**Every process believes it owns the entire machine, and that belief is
a carefully maintained lie.** It has "its own" CPU (nothing else seems
to be running), "its own" memory starting at some fixed layout, "its
own" set of file descriptors. None of this is true at the hardware
level — there's one CPU (or a handful), one physical RAM, shared among
every process on the system. The OS's entire job is maintaining this
illusion convincingly enough that a program never has to know it's
being lied to. Everything else in this stage is a mechanism in service
of that one lie.

**The CPU illusion is maintained by time-slicing plus context
switching.** The kernel runs a *scheduler* that periodically (via a
timer interrupt) takes the CPU away from the running process, saves
every register it was using (the process's entire visible state) into
that process's kernel-managed control block, picks another process to
run, and restores *its* saved registers. From inside any single process,
this is completely invisible — the illusion of "I have had this CPU
continuously" survives because every register you could observe was
put back exactly as you left it. This is the mechanism behind
"multitasking," and it's the first thing 8.2 (write a new scheduler)
asks you to modify directly.

**The memory illusion is maintained by virtual memory / paging.** Every
address your process ever touches is a *virtual* address, translated by
hardware (with page tables the kernel maintains) into a physical
address on every single memory access. This buys three things at once:
isolation (your virtual address space maps to physical pages nothing
else can reach, so one process can't read or corrupt another's memory
by accident or, absent a bug, on purpose), a uniform address layout
(every process can believe its code starts near the same address,
regardless of what's physically resident where), and overcommit (pages
can be swapped out, mapped lazily, or shared copy-on-write, all invisible
to the process). The process never sees a physical address; it doesn't
need to.

**The privilege boundary is what makes the illusion non-optional to
respect.** User-mode code cannot touch page tables, cannot mask
interrupts, cannot execute privileged instructions — the CPU itself
enforces this, not politeness. The *only* sanctioned way from user mode
into kernel mode is a trap: a syscall instruction, a hardware interrupt,
or a fault (e.g. a page fault), each of which hands control to a fixed,
kernel-defined entry point — never to an address the user-mode code
chooses. This is the mechanism you'll extend directly in 8.3 (add
syscalls): a new syscall means adding a new, deliberate doorway through
this exact boundary, at a number the kernel recognizes, not opening a
new hole in it.

**A syscall is the trap mechanism, seen from the other side of Stage
7's convention.** You already know the *user-mode* half — syscall
number in a register, `syscall` instruction, arguments in fixed
registers. What xv6 shows you is the *other* half: the trap handler that
receives that number, an entry point that saves the interrupted user
context (so it can resume the illusion afterward), dispatches to the
right kernel function by that number, and eventually returns control —
and *that's* the code path 8.3 asks you to extend.

## Required reading

Per the Stage 8 README's resource table: OSTEP's chapters on
"Virtualization" (CPU virtualization, scheduling, address spaces, paging)
for the conceptual model, and the MIT 6.828/6.S081 xv6 book + lab
materials for the concrete implementation you'll actually be reading and
modifying in 8.1.

## Check yourself

1. During a context switch, exactly what has to be saved before the
   scheduler picks a different process to run, and where does it get
   saved to (not "somewhere" — specifically whose memory)?
2. Two processes both believe their code starts at the same virtual
   address. What makes this safe instead of a conflict?
3. Why can't user-mode code just jump directly into kernel code instead
   of going through a syscall/trap — what specifically would break (or
   become unsafe) if it could?
4. When xv6 handles a timer interrupt mid-instruction in some user
   process, what has to be true about how much of that instruction had
   already executed, for the process to be resumable afterward without
   corruption?
5. If you add a new syscall in 8.3, what are the *minimum* places in
   xv6 you'd expect to need to touch, based on the "user-mode number in
   a register, kernel dispatches by number" model above?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 8.1 — Modify xv6
(Orientation)** (`projects/8.1-xv6-modifications/SPEC.md`). Start there.
