> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 15.01 — No OS Safety Net

## Why this matters

Every stage before this one, even the lowest-level ones (Stage 5's
processes, Stage 7's assembly), still ran on top of an operating
system — something else owned the memory map, isolated your process
from every other one, and cleaned up after you when you wrote to a bad
address. On the board you'll flash in 15.1, none of that exists until
*you* write it. There is no kernel to catch a bad pointer and kill your
process — a bad pointer here can hang the chip, jump into garbage, or
silently corrupt the exact memory your own code depends on next. This
is the closest this course gets to "no safety net," and it's why the
bootloader project puts so much weight on the memory map and an
integrity check before jumping to anything.

## Core concepts

**Virtual memory is a service the OS provides, not a property of the
hardware itself.** On your laptop, address `0x1000` in your process is
a fiction — the MMU translates it to some real physical address the OS
chose, and every other process gets its own equally fictional
`0x1000`, invisibly isolated from yours. A microcontroller like an
STM32 (outside its optional MPU, which is a much smaller and *opt-in*
protection mechanism, not full virtual memory) has none of this.
Address `0x08000000` is *the actual flash chip*. Address `0x20000000`
is *the actual SRAM*. When you write code, you're placing bytes at
real, physical, singular locations — there's exactly one of each, and
you're the only thing that will ever occupy it.

**This is why the memory layout isn't documentation, it's a contract
with the CPU itself.** In an OS process, the linker mostly picks
addresses for you and it doesn't matter much where things land — the
OS's virtual memory makes every process's layout look the same from
the inside. Here, *you* decide, via the linker script, where the
bootloader lives, where flash ends and the application region begins,
where the stack starts and grows downward from. Get this wrong — say,
let the bootloader's own code region overlap where the application
expects to be flashed — and there's no page fault to tell you; you get
silent corruption or a jump into the middle of an unrelated
instruction stream. That's exactly why 15.1 requires you to document
this layout: it's load-bearing for every later project that flashes
anything onto this board.

**There is no process isolation, so "your program" and "the whole
system" are the same thing.** On a desktop OS, a segfault kills one
process and the system carries on. Here, a bad write to an arbitrary
address might corrupt a peripheral's memory-mapped control register
(these chips expose hardware — UART, timers, GPIO — as regular memory
addresses you read/write like any variable), scribble over your own
stack, or hang waiting on hardware that will now never respond. "My
program crashed" and "the board is bricked until I re-flash it" are
much closer together than you're used to.

**The vector table is the one piece of structure the CPU still gives
you for free, and it's why the bootloader's integrity check matters so
much.** At reset, an ARM Cortex-M reads the initial stack pointer and
the reset handler's address from two fixed words at the start of
flash, then jumps there — no OS loader, no ELF parsing, no checks.
That's the entire mechanism a bootloader stands on: it's just code
placed at a known address that itself, deliberately, reads *another*
address (where it expects the application to start), optionally
verifies a checksum against it, and jumps. If you skip that check and
jump to a corrupted or half-written application image, the CPU will
happily start executing whatever garbage bytes are sitting there as if
they were valid instructions — there's no OS underneath to notice
anything went wrong.

**DMA is the sharpest version of "you are the memory map."** A
DMA-capable peripheral can read or write SRAM directly, without the CPU
executing a single instruction to move that data — which is exactly
why it's fast. It also means a misconfigured DMA transfer can stomp
memory *while your code is doing something else entirely*, with no
stack trace pointing at the write that caused it. You won't need DMA
for 15.1's bootloader, but keep this in mind for 15.3's UART driver:
"nothing else touches memory unless the code makes it happen" stops
being fully true the moment DMA is configured.

## Required reading

Per this stage's `README.md` resource table: [ARM Developer
docs](https://developer.arm.com/documentation) — specifically the
Cortex-M reset/boot sequence and memory model sections (search for
"vector table" and "reset behavior") — and your board's reference
manual via [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)'s
bundled documentation for the actual flash/SRAM address ranges on your
specific chip.

## Check yourself

1. On your laptop, two different processes can both use address
   `0x1000` without conflict. Why is that meaningless on an STM32 — what
   specifically is missing that made it work on the laptop?
2. What are the two fixed values the Cortex-M reads out of the start of
   flash at reset, and what does it do with each?
3. If your bootloader's checksum check is missing (or buggy) and the
   application image is corrupted mid-flash, what actually happens when
   the CPU jumps to it — walk through it at the instruction level, not
   just "it crashes"?
4. Why does a memory-mapped peripheral register (e.g. a UART's data
   register) behave differently from an ordinary SRAM address when you
   write to it — what's actually watching that address that isn't
   watching a normal variable's?
5. Your bootloader and application both need to agree, in advance, on
   where in flash the application starts. Where does that agreement
   actually live — what breaks if the bootloader's linker script and
   the application's linker script disagree about it?

Answers withheld until asked — the memory-layout documentation
requirement in 15.1 is where most of these get concrete.

## Project

This lecture is the bridge into **Project 15.1 — Bootloader**
(`projects/15.1-bootloader/SPEC.md`). Start there — note the
stage-level requirement that this needs real hardware; flag it in
STATUS.md rather than skipping silently if you don't have a board yet.
