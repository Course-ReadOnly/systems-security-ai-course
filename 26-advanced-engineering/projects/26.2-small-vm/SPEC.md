> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 26.2 — A Small VM

## Goal

A bytecode virtual machine — the natural compilation target for 26.1's
compiler, and a step beyond Stage 4.1's simple CPU simulator: a stack-
based (or register-based) VM with a richer instruction set, closer to
what CPython/the JVM/Lua actually are under the hood.

## Requirements

1. Define a bytecode instruction set (stack-based is the more common,
   simpler starting choice) with at minimum: arithmetic, comparisons,
   conditional/unconditional jumps, and function calls with a real call
   stack.
2. Correct call-stack handling: function calls push a new frame,
   returns pop it correctly, including passing arguments and returning
   values.
3. **Integrate with 26.1**: your compiler should be able to target this
   VM's bytecode directly (or close to it) — this is what makes the two
   projects a real pipeline rather than two disconnected exercises.
4. Basic error handling: an invalid opcode or stack underflow is
   detected and reported, not undefined behavior.

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] Paste a hand-assembled (or 26.1-compiled) bytecode program with
      at least one function call, run correctly with the right result
- [ ] Stack-underflow/invalid-opcode case tested and handled cleanly
- [ ] If integrated with 26.1: paste a full pipeline run — source →
      compiled → executed on this VM
- [ ] `git log` shows iteration
- [ ] README documenting the bytecode format and call-stack layout

## When done

Point me at the source + `git log`. I'll check call-frame handling
hardest — incorrect stack-frame bookkeeping across nested/recursive
calls is where VMs like this most often break in subtle ways.
