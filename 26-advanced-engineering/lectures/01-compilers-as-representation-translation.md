> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 26.01 — A Compiler Is a Chain of Representation Translations

## Why this matters

This stage assumes Stages 1-9 are genuinely solid, and 26.1 is where
that gets tested directly: you already know assembly (Stage 7), you've
built an ISA and an assembler (Stage 4), and now you're building the
piece that sits in front of all of it. Strip away the mystique and a
compiler is nothing but a sequence of translations, each one turning a
representation that's easy for *humans* to write into one that's easier
for the *next stage* to process, ending at something a machine can
execute. Understanding it as a pipeline of representations — not one
monolithic "compile" black box — is what makes 26.1 tractable, and it's
the same mental model you'll need in 26.2 (bytecode as yet another
target representation) and when you touch LLVM directly, which is built
on exactly this front-end/back-end split at industrial scale.

## Core concepts

**Lexing turns a flat string into a flat stream of tokens, discarding
noise.** Source code as text has whitespace, comments, and arbitrary
spacing that carry no meaning — the lexer's whole job is to strip that
away and classify what's left into a sequence of typed tokens (`IDENT`,
`NUMBER`, `PLUS`, `LPAREN`, ...). This is a strictly local, one-pass
operation: the lexer doesn't need to understand `(a + b) * c` as an
expression, it just needs to correctly chop it into `LPAREN, IDENT(a),
PLUS, IDENT(b), RPAREN, STAR, IDENT(c)`. Keeping this phase dumb on
purpose is what makes the next phase possible to write cleanly.

**Parsing turns that flat stream into a tree that encodes structure.**
This is the phase that actually understands precedence and
associativity — `a + b * c` has to become a tree where `b * c` is a
subtree feeding into the `+`, not a tree read strictly left to right,
or you'll silently compute the wrong value. Recursive-descent parsing —
the natural starting approach — makes this concrete: you write one
function per grammar rule, and each function calls the functions for
the rules it's built from, so operator precedence gets encoded directly
in which function calls which (a common structure: `parseExpression`
calls `parseTerm`, which calls `parseFactor`, mirroring
lowest-to-highest precedence). The output, the AST, is the single most
important artifact in the whole pipeline — everything downstream reads
it, and it's the natural place to catch **syntax errors**: a token
sequence that doesn't match any grammar rule fails right here, before
anything is generated.

**Semantic analysis walks the AST and answers questions parsing
couldn't.** Parsing only checks "is this grammatically well-formed" —
it has no notion of whether a variable exists. Resolving names to
declarations (and rejecting undefined-variable references — the
semantic error class 26.1 explicitly requires) needs a symbol table:
a mapping from name to declaration, pushed and popped as the walk
enters and exits each scope (a new block opens a new scope layer; using
a name looks it up starting from the innermost scope outward). This is
exactly why scoping bugs are a *semantic* error class distinct from
syntax errors — the code parses fine, `x + 1` is syntactically valid
regardless of whether `x` was ever declared; only a walk with scope
tracking catches that it wasn't.

**Code generation is the mirror image of parsing: tree back to a flat
sequence, one more time.** Having built structure up (tokens → tree),
codegen walks that tree and flattens it back into a linear sequence of
instructions for the target — your own ISA via 4.3's assembler, LLVM
IR, or real machine code. A binary operation node becomes: generate code
for the left subtree, generate code for the right subtree, emit the op.
This is a textbook case of a problem solved cleanly by recursion because
the input (a tree) is itself recursively structured.

**This is exactly why "front-end" and "back-end" is a real, load-bearing
split, not just terminology — and it's the reason LLVM exists at all.**
The front end (lexer + parser + semantic analysis, all specific to
*your* source language) has no idea what CPU it'll run on. The back end
(codegen, specific to the *target*) has no idea what source language
produced the IR it's given. LLVM's actual value proposition is exactly
this: write one front end for a new language and you get every LLVM
backend (x86, ARM, RISC-V, ...) for free, or write one new backend and
every existing LLVM-based front end (Clang, Rust, Swift, ...) targets it
immediately. Choosing LLVM IR as your 26.1 target, instead of your own
ISA, is choosing to plug into that ecosystem rather than owning the
whole pipeline yourself — a real tradeoff, not just "the easy option."

## Required reading

Per `ROADMAP.md`'s Stage 26 resource table — the [LLVM official docs +
tutorial](https://llvm.org/docs/tutorial/), specifically "My First
Language Frontend with LLVM" (the Kaleidoscope tutorial). It walks
lexer → parser/AST → LLVM IR codegen for a small language end to end —
read it even if you target your own ISA instead of LLVM IR, since the
front-end structure it teaches is target-independent.

## Check yourself

1. Why does `a + b * c` need a parser (structure-aware) rather than
   being computable correctly straight from the lexer's flat token
   stream?
2. Give a concrete example of a token sequence that's syntactically
   valid (passes the parser) but semantically invalid, and explain
   which phase catches it and why that phase, not an earlier one.
3. In a recursive-descent parser with functions like `parseExpression`
   → `parseTerm` → `parseFactor`, which function should be called first
   when parsing `2 + 3 * 4`, and how does that call order guarantee `*`
   binds tighter than `+` without any explicit "precedence table" data
   structure?
4. What has to be pushed and popped from your symbol table exactly when
   the parser enters and exits a nested block — and what bug results if
   you forget to pop on exit?
5. If you target LLVM IR instead of your own ISA, what part of your
   26.1 pipeline (lexer, parser, semantic analysis, or codegen) changes,
   and what part stays identical? What does that split tell you about
   why LLVM lets languages like Rust and Swift share backends?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 26.1 — A Small Compiler**
(`projects/26.1-small-compiler/SPEC.md`). Start there — 26.2's bytecode
VM (`projects/26.2-small-vm/SPEC.md`) is the natural next step once
you've got a working codegen target.
