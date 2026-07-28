> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached. Stretch project — do this after 20.3, not
> instead of it.

# Project 20.4 — Stretch: Port the MLP to C

## Goal

Take 20.3's MLP (or a smaller version of it) and implement the same
forward and backward pass in C, with your own matrix multiplication —
no BLAS, no linear algebra library. NumPy hides a lot of what's
actually happening in a matrix multiply and a gradient update; writing
it in C forces every one of those operations to be explicit. This also
ties directly back to Stage 1's C fundamentals and Stage 1's Valgrind
standard, applied to a completely different domain.

## Requirements

1. Forward pass and backward pass implemented in C, including your own
   matrix multiply.
2. Trained on a small subset of MNIST (or a smaller synthetic dataset)
   — a naive C matmul on the full dataset may be genuinely slow; that's
   an acceptable, expected tradeoff. Document the runtime and why it's
   what it is (compare against 20.3's NumPy version if you want a
   concrete number).
3. Demonstrates real learning: loss decreasing or accuracy improving
   over training, shown with actual numbers/output, not just "it ran."
4. Valgrind-clean — same standard as every Stage 1 project.

## Acceptance criteria

- [ ] Compiles cleanly, runs, and is Valgrind-clean (paste the summary
      line showing zero leaks/errors)
- [ ] Matrix multiplication is your own implementation, no external
      linear algebra library
- [ ] Training curve (loss or accuracy over epochs) shown with real
      numbers
- [ ] `git log` shows real iteration

## When done

Point me at the source, `git log`, and the Valgrind output. I'll
compare your C matmul's memory access pattern against what you'd
expect from the matrix shapes in 20.3 — this is a good place to catch
row-major/column-major mixups that NumPy silently protected you from.
