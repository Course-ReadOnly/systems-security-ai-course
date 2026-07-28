> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 20.01 — Backpropagation From Scratch

## Why this matters

Every later "AI" stage in this course — Stage 21's classifiers, Stage
22's CNNs, Stage 23's transformers, Stage 25's AI-assisted security
tooling — is a neural network trained by the same one mechanism:
backpropagation, a repeated application of the chain rule across a
computation graph. Frameworks hide this behind `.backward()`. If you
learn the frameworks first, that call stays a black box forever — it
works, until it doesn't (a vanishing gradient, a shape mismatch, a
NaN loss), and debugging a black box you don't understand is guesswork.
Build it by hand once, here, while the network is small enough to trace
on paper, and every later framework call becomes something you can
reason about instead of something you trust.

## Core concepts

**The forward pass** is nothing more than repeated weighted sums plus a
nonlinearity: `z = w·x + b`, `a = activation(z)`. Stack layers of this
and you get a network. Without the nonlinearity, stacking layers is
pointless — any composition of purely linear functions collapses back
into one linear function, so depth would buy you nothing.

**The loss function** turns "how wrong was this prediction" into a
single number you can take a derivative of. MSE for regression,
cross-entropy for classification — the choice matters less right now
than understanding that the whole point of training is minimizing this
one number.

**The chain rule is the entire mechanism.** If `L` depends on `a`,
`a` depends on `z`, and `z` depends on `w`, then `dL/dw = dL/da · da/dz
· dz/dw`. That's it — backpropagation is applying this repeatedly,
layer by layer, from the output back to the inputs, reusing each
layer's computed gradient for the layer before it (this reuse — not
recomputing from scratch at every layer — is *why* backprop is
efficient instead of exponentially expensive).

**A computation graph** is what makes this automatic instead of
something you re-derive by hand for every new architecture. Every
operation (`+`, `*`, an activation function) is a node that knows two
things: how to compute its output from its inputs (the forward pass),
and how to route a gradient backward to each of its inputs given the
gradient flowing into it (the backward pass). Chain enough of these
together and `.backward()` is just: walk the graph in reverse
topological order, and at each node, apply its local backward rule.
This is genuinely the entire idea behind PyTorch's autograd — you're
about to build a tiny, real version of it in 20.2.

**Gradient descent** uses these gradients to actually improve the
network: `w ← w - lr · dL/dw`. The gradient points in the direction of
steepest *increase*; you step opposite it. The learning rate (`lr`) is
the one hyperparameter you cannot avoid reasoning about — too large and
training diverges (loss explodes or oscillates), too small and it
crawls.

**Why XOR breaks a single neuron.** A single neuron computes a linear
decision boundary — one straight line (or hyperplane) separating
"yes" from "no." XOR's four points aren't linearly separable — no
single straight line separates them. This isn't a bug or a training
failure; it's a hard mathematical ceiling. It's *the* historical reason
the field moved from single perceptrons (1950s-60s) to multi-layer
networks: stacking layers lets the network learn a *combination* of
linear boundaries, which can approximate arbitrarily complex
(nonlinear) decision surfaces. You'll prove this to yourself directly
in 20.1.

## Required reading

Per `ROADMAP.md`'s Stage 20 resource table — start with Karpathy's
["Neural Networks: Zero to Hero"](https://karpathy.ai/zero-to-hero.html),
specifically the first video (building micrograd). Watch it *actively*
— pause and predict what the next line of code does before he writes
it. If the pace is too fast anywhere, [Michael Nielsen's free
book](http://neuralnetworksanddeeplearning.com/) covers the same
material more slowly, with the math written out in full — chapter 1-2
covers everything in this lecture.

## Check yourself

1. Why does stacking two *linear* layers with no activation function
   between them accomplish nothing that one linear layer couldn't?
2. In `dL/dw = dL/da · da/dz · dz/dw`, which of these three factors
   would be zero (or near-zero) if the neuron's activation function had
   "saturated" (e.g. a sigmoid far out in its flat tails)? What does
   that imply about training a network that gets stuck this way?
3. If a `Value` node in a computation graph is used as an input to two
   different downstream operations, what has to happen to the
   gradients flowing back from each of them when they reach that node?
   (This is the exact case 20.2's acceptance criteria calls out.)
4. Why is a learning rate that's too large actually *worse* than one
   that's merely slow — what does "training diverges" look like
   concretely, in terms of the loss value over iterations?
5. Concretely, what does it mean for two points to *not* be linearly
   separable, and why does adding a hidden layer fix it for XOR
   specifically?

Answers withheld until asked — work through 20.1 first; the answers
become obvious once you've implemented and watched it fail on XOR
yourself.

## Project

This lecture is the bridge into **Project 20.1 — Perceptron / Single
Neuron From Scratch** (`projects/20.1-perceptron/SPEC.md`). Start
there.
