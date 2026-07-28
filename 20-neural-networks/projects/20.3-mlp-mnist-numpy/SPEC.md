> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached.

# Project 20.3 — MLP From Scratch on MNIST (NumPy Only)

## Goal

The bridge from "I understand one neuron" (20.1) and "I understand a
tiny scalar-level graph" (20.2) to "I understand a real, vectorized
network" — a multi-layer perceptron for handwritten digit
classification, with forward and backward passes implemented as matrix
operations in raw NumPy. This is the last stop before Stage 21 lets a
framework do this for you; the vectorization itself (batching neurons
and samples into matrix operations instead of Python loops) is as much
the point as the network architecture.

## Requirements

1. At least one hidden layer, a softmax output layer, and
   cross-entropy loss.
2. Both the forward and backward pass implemented as vectorized NumPy
   matrix operations — no per-neuron Python loops in the training hot
   path.
3. Trained on real MNIST (or Fashion-MNIST, if you want more
   difficulty), with a genuine train/test split.
4. Report held-out test accuracy. A correctly-implemented bare-minimum
   MLP should comfortably clear 90%+ on MNIST — if it doesn't, treat
   that as a signal the backward pass has a bug, not "needs more
   epochs."
5. Before trusting the training results, gradient-check your backward
   pass: compare the analytical gradient (from your backward pass) to
   a numerical gradient (finite differences) for at least one weight
   matrix.

## Acceptance criteria

- [ ] Forward and backward pass in vectorized NumPy, no autograd
      library involved
- [ ] Trained on real MNIST/Fashion-MNIST with held-out test accuracy
      reported (≥90% on MNIST, or a reasoned explanation if lower)
- [ ] Gradient check (numerical vs. analytical) shown for at least one
      layer's weights
- [ ] `git log` shows real iteration
- [ ] README explains the matrix shapes flowing through each layer —
      what each dimension actually represents (batch size, features,
      hidden units, classes)

## Security relevance

A trained classifier's confidence output is only as trustworthy as your
understanding of how it was produced — this project is where you build
that understanding from raw matrix operations rather than a framework's
`.fit()` call. That groundwork pays off directly in Stage 21's
precision/recall work (a model can be accurate and still miscalibrated)
and Stage 25's "when to trust a model" question, both of which assume
you understand what's actually happening between input and output.

## When done

Point me at the source, `git log`, the gradient-check output, and the
test accuracy. I'll ask you to explain the shape of your weight
gradient matrix from first principles (why that shape, derived from
which two other matrices) — that's usually where "copied the formula"
and "understands it" become visibly different.
