> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached.

# Project 20.2 — Micrograd-Style Autograd Engine

## Goal

Build your own small automatic-differentiation engine — the actual
mechanism every deep learning framework (PyTorch included) is built
on. This is the "the magic isn't magic" project for this stage: once
you've built `.backward()` yourself, Stage 21's `loss.backward()`
stops being a black box. Directly follows Karpathy's micrograd build
from "Neural Networks: Zero to Hero" — use it as your primary guide,
but the implementation and understanding need to be genuinely yours.

## Requirements

1. A `Value` class wrapping a single scalar, supporting at minimum
   `+`, `*`, `-`, `/`, `**` (power), and one nonlinearity (`tanh` or
   `ReLU`).
2. Each operation records its input `Value`s and a local backward
   function (the chain-rule step for that operation) — the computation
   graph should emerge implicitly from object references, not a
   separate graph structure bolted on afterward.
3. Implement `.backward()`: a topological sort of the graph from the
   output node, then apply the chain rule in reverse order to populate
   `.grad` on every node reachable from it.
4. Use your own engine (not PyTorch) to build and train a small MLP —
   2-3 layers, a handful of neurons — on a toy binary classification
   dataset.
5. Gradient-check your engine: for at least 3 nontrivial expressions,
   compare your engine's `.grad` output against either PyTorch's
   autograd or manual numerical differentiation (finite differences)
   on the same expression. This is the actual correctness bar — a loss
   curve going down doesn't prove the gradients are right.

## Acceptance criteria

- [ ] `Value` class supports the required operations with both correct
      forward values and correct backward (gradient) computation
- [ ] `.backward()` correctly handles a graph where a single `Value` is
      reused multiple times in one expression (e.g. `x*x + x`) — this
      is the case a naive, non-topologically-sorted implementation gets
      wrong (gradients get overwritten instead of accumulated)
- [ ] Gradient-checked against PyTorch or numerical differentiation for
      at least 3 nontrivial expressions, values shown side by side
- [ ] A small MLP trained end-to-end using only this engine, with a
      loss curve shown
- [ ] `git log` shows real iteration

## When done

Point me at the source, `git log`, and the gradient-check output.
I'll specifically test the "variable reused multiple times" case —
that's the one place this project is easy to get subtly wrong while
still looking like it works.
