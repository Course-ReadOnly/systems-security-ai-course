> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 4.3 — Simple Assembler

## Goal

Write an assembler targeting **your own 4.1 CPU simulator's instruction
set** — turning human-readable mnemonics (`ADD R1, R2`) into the raw
encoding your simulator executes. This is where an ISA stops being an
abstract idea and becomes something you can actually target as a
compiler-adjacent tool — direct prep for Stage 26's compiler project.

## Requirements

1. Reads a text source file using your 4.1 ISA's mnemonics (e.g. `LOAD`,
   `ADD`, `JMP`, `HALT`).
2. Two-pass assembly: first pass resolves labels/jump targets to
   addresses, second pass emits the actual encoded instructions — labels
   used before they're defined (forward references) must work correctly.
3. Outputs a binary/byte format your 4.1 simulator can load and execute
   directly.
4. Reports clear errors for invalid mnemonics or malformed operands
   (line number + what's wrong), not silent garbage output.
5. Round-trip proof: assemble a real program, run it on your 4.1
   simulator, confirm correct execution.

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] A real assembly-source program (using at least one forward-
      referenced label/jump) assembled and pasted alongside its encoded
      output
- [ ] That output actually run on your 4.1 simulator, with correct
      register-state results pasted (this is the real proof it works,
      not just "it assembled without error")
- [ ] At least one malformed-input case pasted, showing a clear error
      with line number
- [ ] `git log` shows iteration

## Security relevance

An assembler turning mnemonics into raw bytes is the same operation
(in reverse) as a disassembler turning bytes back into mnemonics —
Stage 11's entire premise. Understanding encoding from the authoring
side makes it much easier to spot when a disassembler's output doesn't
add up later (a real anti-analysis technique: crafting bytes that
disassemble misleadingly, exploiting exactly the ambiguity you'll have
resolved cleanly here on your own simple ISA).

## When done

Point me at the source + `git log` and the round-trip evidence. I'll
check the forward-reference/label-resolution logic hardest — that's
where two-pass assemblers most often have an off-by-one or ordering bug.
