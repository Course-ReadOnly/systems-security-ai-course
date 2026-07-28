> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 26.1 — A Small Compiler

## Goal

A real compiler for a small language of your own design, targeting
either your Stage 4.1 toy ISA, LLVM IR, or real machine code — the
culmination of Stage 4 (ISA design), Stage 7 (assembly), and Stage
4.3's assembler all at once.

## Requirements

1. Define a small source language (arithmetic expressions, variables,
   at least one control-flow construct like `if`/`while` — doesn't need
   to be large, needs to be real).
2. A real pipeline: lexer → parser (producing an AST) → code generation
   targeting your chosen backend (your own ISA + 4.3's assembler, or
   LLVM IR, or direct machine code).
3. Correct handling of variable scoping if your language has blocks/
   functions.
4. Meaningful error reporting for both syntax errors (parse failures)
   and at least one class of semantic error (e.g. undefined variable).

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] Paste a real, non-trivial source program (using variables and
      control flow) compiled and actually run, showing correct output
- [ ] Both a syntax-error and a semantic-error case pasted, with clear
      error messages (line numbers if reasonable)
- [ ] `git log` shows iteration
- [ ] README documenting the language grammar and the compilation
      pipeline/target chosen

## When done

Point me at the source + `git log`. I'll check the parser handles
genuinely ambiguous-looking grammar correctly (operator precedence is
the classic place small compilers get subtly wrong) before looking at
codegen.
