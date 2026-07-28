> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 4.01 — Fetch, Decode, Execute

## Why this matters

Every C program you wrote in Stage 1, every data structure you built in
Stage 2, eventually gets compiled down to a sequence of numbers sitting
in memory. This stage is where you stop treating "the computer runs my
program" as a black box and build the actual mechanism that makes a
number in memory *become* a register change or a memory write. That
mechanism — fetch, decode, execute, repeat — is the single loop Stage 7
(Assembly) writes instructions *for*, Stage 8 (OS) interrupts and
context-switches *around*, and Stage 12/26 (sandboxing, hypervisors)
build isolation *on top of*. Project 4.1 makes you build it yourself,
for an instruction set you invent, before touching a real one.

## Core concepts

**An instruction is just a number, and "decoding" is looking up what
that number means.** There's no special hardware type called
"instruction" distinct from "data" — memory is bytes, full stop. What
turns a byte into an *instruction* is purely that the CPU's program
counter is currently pointing at it and about to interpret its bits
according to a fixed encoding scheme you (or Intel, or ARM) defined in
advance — e.g. "the top 4 bits select the opcode, the next 4 select a
register." This is also *why* self-modifying code and code-injection
exploits work at all: memory doesn't enforce a boundary between "data"
and "code," only convention and (on modern hardware) explicit
protections like the NX/DEP bit do.

**Fetch, decode, execute is a loop over one register: the program
counter (PC).** Fetch: read the instruction at the address the PC
holds. Decode: split that instruction's bits into opcode + operands,
i.e. figure out *which* operation this is and what it operates on.
Execute: actually perform it — add two registers, write to memory,
whatever the opcode says — and update the PC (usually +1 instruction,
unless this was a jump, in which case the PC gets set explicitly to the
jump target instead). Then loop. This is the entire "brain" of a CPU
simulator; everything else (more registers, more opcodes, a fancier
memory model) is elaboration on this one loop, not a different
mechanism.

**Designing the instruction set *is* designing the interface between
hardware and software.** Every opcode you add is a promise: "if you put
these exact bits in memory, I will perform this exact operation."
Project 4.1 has you invent this from scratch — how many bits for the
opcode vs. the operands, how many registers you can address, what a
"conditional jump" actually checks — and that design directly becomes
the ISA reference Project 4.3's assembler has to target. A sloppy or
inconsistent encoding here (e.g. an opcode that sometimes takes one
operand and sometimes two, without something in the bits themselves
distinguishing which) makes decoding ambiguous, which is a real bug
category, not just an inconvenience.

**A conditional jump is how a fixed loop of instructions produces
actual branching behavior**, and it's worth being precise about the
mechanism: execute doesn't just perform an operation, it *decides what
the PC becomes next*. Every other instruction sets PC = PC + 1
(implicitly, "keep going in order"); a jump instruction sets PC to
some other address instead, based on a condition it just evaluated
(e.g. "was the last result zero"). Loops and `if` statements in every
language you've used compile down to exactly this: ordinary
instructions, plus PC manipulation.

**Halt and invalid-opcode handling are the two edges of "what happens
when the promise breaks."** A halt instruction is a deliberate,
well-defined way to stop the fetch/execute loop. An invalid opcode is
the *undefined* case — bits that don't correspond to any instruction
you decoded for, which real hardware has to do *something* well-defined
about (trap to an exception handler) rather than silently doing
something arbitrary. Project 4.1 requires both handled cleanly for
exactly this reason: a "toy" CPU that behaves unpredictably on bad
input teaches the wrong lesson about what real hardware guarantees.

## Required reading

Per `04-computer-architecture/README.md`'s resource table — [NAND2Tetris](https://www.nand2tetris.org/),
the Hack CPU chapter (building fetch/decode/execute from logic gates
up) specifically, since that's the most concrete match for what
Project 4.1 asks you to simulate in software. [Berkeley
CS61C](https://cs61c.org/)'s early lectures cover the same loop from
the "real ISA" (RISC-V) angle if you want the second framing alongside
it.

## Check yourself

1. If you copied a chunk of "data" bytes into the middle of your
   instruction memory and pointed the PC at them, what would your
   simulator actually do — and what does that tell you about where the
   data/code boundary really lives?
2. Walk through exactly what changes (which registers, which memory
   locations, and the PC) for one execution of an `ADD` instruction
   versus one execution of a conditional jump that's taken.
3. Why does an inconsistent instruction encoding (e.g. operand count
   not determinable from the opcode bits alone) make decoding
   ambiguous — what would your decoder actually have to do to handle
   it, and why is that fragile?
4. What's the concrete difference in what the CPU does for a `HALT`
   instruction versus an opcode value that doesn't match anything in
   your instruction set?
5. Project 4.3's assembler will need your ISA documentation to generate
   correct machine code. What, specifically, does that documentation
   have to specify about each instruction for that to actually work?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 4.1 — CPU Simulator**
(`projects/4.1-cpu-simulator/SPEC.md`) — the conceptual base for 4.3
(assembler) and 4.2 (CHIP-8), per the README's suggested order.
