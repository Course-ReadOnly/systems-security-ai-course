> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 7.01 — Calling Conventions as Social Contract

## Why this matters

Stage 4 had you simulate a CPU; this stage puts you in front of a real
one, with nothing between you and it. That absence is the whole point of
7.1 — you'll feel, by hand, everything C normally does silently: setting
up a stack frame, deciding which register holds what, converting a
string to a number one digit at a time. It's also non-negotiable
preparation for Stage 11 (Reverse Engineering): a disassembler shows you
raw instructions and register names, and reading them fluently means
already knowing, without looking it up, what `rdi` almost certainly
holds at the top of a function and why `rbp` gets pushed before anything
else happens.

## Core concepts

**The CPU has no concept of "function," "argument," or "return value" —
only registers, memory, and a small set of instructions that move data
between them.** A "function call" is a *convention*: an agreement about
which registers hold the first few arguments, where the rest go, which
register holds the return value, and which registers a callee is
allowed to clobber versus must restore before returning. On x86-64
System V (Linux), that agreement is: integer/pointer args in `rdi`,
`rsi`, `rdx`, `rcx`, `r8`, `r9` in order, return value in `rax`, and
`rbx`/`rbp`/`r12`-`r15` are callee-saved (if you use them, you restore
them) while the rest are caller-saved (assume they're garbage after any
`call`). None of this is enforced by the hardware. The CPU will execute
`call` and `ret` regardless of whether you honored a single bit of it —
which is exactly why violating the convention doesn't produce an error,
it produces a program that's subtly wrong in a way that's miserable to
debug. This is the single most common way 7.1 breaks, per its own
grading note: clobbering a register the kernel (or a function you called)
expected untouched.

**`call` and `ret` are just `push`+`jmp` and `pop`+`jmp` with a name.**
`call` pushes the return address onto the stack and jumps; `ret` pops an
address off the stack and jumps to it. This is precisely why a stack
corruption bug (writing past a buffer, or unbalancing `push`/`pop`)
can hijack control flow: `ret` doesn't know or care whether the value it
pops is the address `call` actually pushed, or something an attacker
overwrote it with. The entire "stack smashing" vulnerability class you'll
meet properly in Stage 11-13 is this one fact, weaponized.

**The stack frame is a convention on top of a convention.** `push rbp` /
`mov rbp, rsp` at function entry establishes a fixed reference point
(the frame pointer) so local variables and saved registers can be
addressed at consistent offsets even as `rsp` moves around during the
function body (e.g. from further pushes, or `call`s to other functions).
Nothing requires you to maintain a frame pointer at all — some optimized
code omits it entirely and addresses everything relative to `rsp` — but
when you're hand-writing assembly, keeping one is what makes your own
code (and, later, a disassembler's output) legible instead of an
unlabeled maze of stack-relative offsets.

**A syscall is a *different* contract from a function call — same idea,
harder boundary.** Calling into the kernel (`read`, `write`, `exit`) uses
its own register convention (on Linux x86-64: syscall number in `rax`,
arguments in `rdi`, `rsi`, `rdx`, `r10`, `r8`, `r9` — note `r10` instead
of `rcx`, because `syscall` itself clobbers `rcx` and `r11` as part of
the mode switch into the kernel) and its own instruction (`syscall`,
not `call`). Get a register wrong here and you're not miscommunicating
with a function you wrote — you're miscommunicating with the kernel,
which will happily read garbage as a buffer pointer or length if you let
it. `strace` (which 7.1 asks you to use) exists precisely to show you
whether the syscalls you *think* you're making match what the kernel
actually received.

## Required reading

Per the Stage 7 README's resource table: the NASM Tutorial for syntax
and the mechanics of assembling/linking with `nasm`+`ld`, and
OpenSecurityTraining2's x86/x64 training for the calling convention and
register discipline in depth. Keep the Linux x86-64 syscall table
(syscall numbers, e.g. `read`=0, `write`=1, `exit`=60 — search "x86-64
Linux syscall table") open as a reference while you write 7.1.

## Check yourself

1. If you call a function without honoring the System V calling
   convention (e.g. you clobber a callee-saved register you were
   supposed to restore), what specifically breaks, and in whose code
   does the bug actually manifest — yours, or the caller's?
2. `ret` pops a value off the stack and jumps to it unconditionally. What
   has to be true about everything you pushed/popped between the
   function's `call` and its `ret` for that popped value to still be the
   correct return address?
3. Why does the Linux syscall convention use `r10` instead of `rcx` for
   the fourth argument, when the regular function-call convention uses
   `rcx` as its fourth argument register?
4. What does `strace` actually show you that reading your own assembly
   source can't confirm on its own?
5. Concretely, what would `rbp` and `rsp` point to right after your
   function's `push rbp` / `mov rbp, rsp` prologue, before any locals are
   allocated?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 7.1 — Assembly Calculator**
(`projects/7.1-asm-calculator/SPEC.md`). Start there.
