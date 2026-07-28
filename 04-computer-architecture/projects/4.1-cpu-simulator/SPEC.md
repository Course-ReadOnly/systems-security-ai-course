> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 4.1 — CPU Simulator

## Goal

Design a tiny toy instruction set and simulate it — registers, memory,
the fetch/decode/execute loop, made concrete in code instead of just
diagrams. This is the conceptual base 4.2 (CHIP-8) and 4.3 (assembler)
build on.

## Requirements

1. Define your own minimal instruction set (this is part of the
   assignment, not given): at minimum, load/store, add/sub, a
   conditional jump, and a halt instruction.
2. A fixed set of registers (e.g. 4–8) and a flat memory array.
3. Implements fetch → decode → execute as an explicit loop, one
   instruction per iteration, updating a program counter.
4. Loads a program (array of instruction bytes/words) into memory before
   running.
5. A way to inspect state (dump registers + relevant memory) after each
   step or at the end, for debugging/verification.
6. Handles a halt instruction cleanly (program stops, doesn't loop
   forever) and an invalid opcode (clear error, not undefined behavior).

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] A real hand-written program in your instruction set (e.g. compute
      a small sum or factorial using a loop) — paste it plus the
      register-state output proving it computed the right answer
- [ ] Invalid-opcode case tested and handled cleanly
- [ ] Infinite-loop protection or explicit halt tested (a program that
      halts vs. one you deliberately let run to a step limit)
- [ ] `git log` shows iteration
- [ ] README documenting your instruction set (opcode encoding, what
      each instruction does) — this doubles as the ISA reference you'll
      need for 4.3's assembler

## Security relevance

Every sandbox/VM/emulator-based security tool (Stage 12's malware
sandboxing, Stage 26's hypervisor work) is built on exactly this
fetch-decode-execute loop, with the added job of also containing
whatever's running inside it. Building one yourself, even a toy one,
makes "sandbox escape" a concrete idea later instead of an abstract
term — it's a bug in code shaped just like this.

## When done

Point me at the source + `git log`. I'll check the fetch/decode/execute
loop structure is genuinely general (not special-cased per instruction
in a way that wouldn't scale) and that the ISA documentation is complete
enough that someone else could write a program against it.
