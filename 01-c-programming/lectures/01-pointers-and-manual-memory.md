> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 1.01 — Pointers and Manual Memory

## Why this matters

Every stage from here forward assumes you actually understand what a
pointer *is*, not just how to spell `*` and `&`. Stage 2's data
structures are pointer-chained nodes with no garbage collector to save
you. Stage 5 (Systems Programming) and Stage 8 (OS) hand you raw
syscalls that traffic in addresses, not objects. Stage 11-13
(reverse engineering, exploitation) are, almost entirely, about what
happens when someone else's manual-memory discipline breaks — a
use-after-free, a buffer overflow, a double-free. You cannot understand
the attack until you've felt the discipline it violates from the inside,
by managing memory yourself and watching what happens when you get it
wrong.

## Core concepts

**A pointer is a number.** Specifically, it's an integer that names a
byte address in your process's memory space. `int *p` doesn't mean
"a magic box containing an int somewhere" — it means "a variable
holding an address, which I've promised the compiler points at an
`int`." Every operation on pointers — `*p` (dereference: go read/write
the byte(s) at that address), `p + 1` (pointer arithmetic: advance by
`sizeof(*p)` bytes, not one byte), `&x` (address-of: get `x`'s
location) — is just address math with a type attached so the compiler
knows how far to step and how many bytes to read.

**The stack and the heap are two different lifetime strategies for the
same memory space.** A local variable (`int x;`) lives on the stack:
its address is valid only until the function returns — the moment the
stack frame pops, that memory is fair game for the *next* function
call, and reading it is undefined behavior even though nothing crashes
immediately (this is exactly what makes "return a pointer to a local
variable" such an insidious bug — it often *appears* to work).
`malloc`/`free` give you heap memory instead: it survives until you
explicitly say you're done with it, which is powerful and is the entire
source of the danger. Nothing enforces the contract for you.

**Ownership is a discipline you invent, not a language feature.**
C has no concept of "who owns this pointer." *You* decide, by
convention, which piece of code is responsible for calling `free()` on
a given allocation — and every memory bug in this stage's projects
traces back to that convention breaking down: **use-after-free** (you
kept using a pointer after something freed it — the memory might now
belong to a totally different allocation), **double-free** (two code
paths both think they own the free, and both call it), and **leak**
(nobody ever thought they owned the free, so it never happens). This is
exactly why Project 2.1 (Stage 2) makes you write down ownership rules
explicitly for every structure — "who allocates, who frees" isn't
paperwork, it's the actual engineering problem C forces you to solve
yourself that most modern languages solve for you.

**`valgrind` is how you get a safety net back.** It can't stop you from
writing the bug, but it instruments every allocation and access so you
find out *after the fact*, in a controlled setting, instead of an
attacker finding out for you in production. Treat a clean `valgrind`
run as a hard requirement, not a nice-to-have — it's in this stage's
acceptance criteria for exactly that reason.

**`argv`/stdin parsing is your first real exposure to untrusted input**
in this course. Every token from the command line or stdin is
attacker-controlled the instant this program ever runs somewhere you
don't control — "did I validate this before I computed with it"
(Project 1.1's calculator: division by zero, malformed tokens) is the
same question Stage 13's buffer-overflow work asks about a memory
offset instead of a number.

## Required reading

Per `01-c-programming/README.md`'s resource table — [Beej's Guide to
C](https://beej.us/guide/bgc/), the pointers and dynamic memory
allocation chapters specifically. If a section moves too fast, cross-
reference the same topic in [Modern C by Jens
Gustedt](https://upload.wikimedia.org/wikipedia/commons/0/0a/Modern_C.pdf),
which spells out the memory model in more formal detail.

## Check yourself

1. Why does returning `&local_var` from a function compile without a
   crash, and yet still be a real bug? What has to happen for the bug
   to actually manifest as visible wrong behavior?
2. Given `int *p = malloc(sizeof(int) * 5);` and `p + 2`, what address
   does that expression actually compute, and why does the compiler
   need to know `p`'s type to compute it?
3. Name one concrete rule you could adopt for "who frees this pointer"
   in a function that allocates memory and returns it to its caller —
   and one way that rule could still be violated by a careless caller.
4. What's the actual difference between a memory leak and a
   use-after-free, in terms of which one is "the memory still exists
   but nobody can reach it" vs. "the memory is reachable but no longer
   means what you think it means"?
5. `valgrind` reports a leak but your program still produced the
   correct output. Why is that not good enough to ship?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 1.1 — Calculator**
(`projects/1.1-calculator/SPEC.md`) — the menu's easiest entry, and
where to start per the README's stage note. Start there; which of the
remaining ten projects come next gets decided based on pace, per the
README.
