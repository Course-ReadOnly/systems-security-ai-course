> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached.

# Project 20.1 — Perceptron / Single Neuron From Scratch

## Goal

The smallest possible neural net — one neuron — with every piece
(forward pass, loss, gradient, update) written by hand, no ML library
involved. This is where the calculus from Stage 19 stops being an
abstraction and becomes code you derived yourself. It also sets up the
single most important historical lesson in the field: why a lone
neuron hits a hard ceiling, and why that ceiling is the reason
multi-layer networks exist at all.

## Requirements

1. Implement the forward pass by hand: weighted sum of inputs plus
   bias, passed through an activation function (sigmoid is the
   standard choice here).
2. Derive the gradient of your loss function with respect to the
   weights and bias **yourself** — write the derivation down (even
   informally, in the README) before implementing it. Use MSE or
   binary cross-entropy.
3. Train with a manual gradient descent loop (your own code, not an
   optimizer class) and plot the loss decreasing over iterations.
4. Test on a toy linearly separable dataset (e.g. AND/OR-gate style
   points, or two well-separated 2D clusters) — it should converge
   cleanly.
5. Then run the same neuron against XOR and show it fails. Explain in
   the README *why*, in terms of linear separability — this is the
   historical reason the field moved to multi-layer networks.
6. No `torch`, `sklearn`, `tensorflow`, or any other library that
   provides autograd or a pre-built model. Plain Python (NumPy for
   array math is fine — the gradient math itself must be yours).

## Acceptance criteria

- [ ] Forward pass, loss, and gradient computation are all your own
      code — paste or describe your gradient derivation in the README
- [ ] Loss-over-iterations plot showing convergence on the linearly
      separable dataset
- [ ] Explicit demonstration that the same neuron fails on XOR, with a
      written explanation of why (linear separability)
- [ ] `git log` shows real iteration
- [ ] No ML-framework imports anywhere in the training code

## When done

Point me at the source, `git log`, and the loss plot. I'll ask you to
walk through your gradient derivation from the loss function down to
the weight update — that's where "copied a formula from a tutorial"
and "actually derived it" become obviously different things.
