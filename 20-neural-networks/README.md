> **Generated ahead of schedule** (2026-07-28, per learner request — see
> `STATUS.md`'s 2026-07-28 note). Revisit when actually reached.

# Stage 20 — Neural Networks Foundations

**Time budget:** 4–6 weeks part-time / 2 weeks full-time

## Objectives

Stage 19 gives you the math (gradients, matrix multiplication,
probability). Stage 21 hands you PyTorch, which does backpropagation
for you. This stage sits deliberately between the two: build a neuron,
an autograd engine, and a trained network **from scratch, in code you
wrote**, so that when Stage 21 introduces `loss.backward()` you know
exactly what that call is doing instead of trusting it as magic. This
is the single most effective way to actually understand deep learning
rather than just operate a framework — every later stage's neural-net
work (Stage 22's CNNs, Stage 23's transformers) rests on the same
mechanism you'll build here by hand.

Narrower in scope than Stage 21/22 on purpose: one mechanism
(backpropagation via the chain rule), understood cold, not a survey of
architectures.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | From-scratch build, autograd + backprop, code-first | [Andrej Karpathy — "Neural Networks: Zero to Hero" (free YouTube series)](https://karpathy.ai/zero-to-hero.html) |
| 02 | Free full textbook, rigorous but accessible | [Neural Networks and Deep Learning — Michael Nielsen (free online book)](http://neuralnetworksanddeeplearning.com/) |
| 03 | Visual intuition for gradient descent/backprop | [3Blue1Brown — Neural Networks series (free YouTube)](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) |
| 04 | Pure-NumPy walkthrough, layer by layer | [Sentdex — "Neural Networks from Scratch in Python" (free YouTube series)](https://www.youtube.com/watch?v=Wo5dMEP_BbI) |

**Topics:** the perceptron, activation functions, forward pass, loss
functions, the chain rule applied to a computation graph,
backpropagation derived by hand, gradient descent, a minimal autograd
engine, vectorized forward/backward passes, why a single neuron can't
solve XOR (and why depth fixes that).

**Primary path through this stage:** Karpathy's "Zero to Hero" series
(specifically the micrograd and makemore-intro videos) is the spine —
it builds exactly what 20.1 and 20.2 below ask for, live, in code.
Nielsen's book is the reference to fall back on when you want the math
written out more formally than the videos have time for.

## Projects

| # | Project | Folder |
|---|---|---|
| 20.1 | Perceptron / single neuron from scratch | `projects/20.1-perceptron/` |
| 20.2 | Micrograd-style autograd engine | `projects/20.2-micrograd/` |
| 20.3 | MLP from scratch on MNIST (NumPy only) | `projects/20.3-mlp-mnist-numpy/` |
| 20.4 | Stretch: same MLP ported to C | `projects/20.4-mlp-in-c/` |

Do these in order — each one removes a crutch the previous one still
had (20.1 has no autograd at all, 20.2 builds one but only at scalar
granularity, 20.3 vectorizes it, 20.4 removes NumPy itself).
