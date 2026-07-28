> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 22.01 — Convolution as Inductive Bias

## Why this matters

Stage 20 taught you that a neural network is layers of weighted sums plus
nonlinearities, trained by backprop — true, but architecture-agnostic.
This stage is about the fact that *architecture* is not a detail; it's
an assumption baked into the model about the structure of its input, and
getting that assumption right is why CNNs beat plain fully-connected
networks on images by a wide margin, not just a little. Understanding
*why* convolution is the right assumption for images — not just how to
call `nn.Conv2d` — is what lets you reason about whether a given
architecture fits a given problem, instead of cargo-culting
"CNN for images, RNN for sequences" without knowing why.

## Core concepts

**A fully-connected layer treats every input as an independent, unordered
feature.** Feed it a flattened image and it learns a separate weight for
every pixel position, with no built-in notion that pixel (10,10) and
pixel (10,11) are neighbors. Two consequences follow: the parameter count
explodes (a 224x224x3 image is ~150,000 inputs, so even one hidden layer
of modest size is millions of weights), and the network has to
*re-learn* the same pattern separately for every position it might
appear at — a cat detector trained only on centered cats won't
recognize one in the corner, because that's a different set of weights
entirely.

**Convolution fixes both problems with one idea: a small filter, shared
across every position.** A kernel (e.g. 3x3) slides across the image,
computing a dot product with the pixels under it at every position, and
the *same* kernel weights are reused everywhere. This is parameter
sharing, and it has a direct consequence worth naming precisely:
**translation invariance** — if the kernel learns to detect a vertical
edge, it detects that edge wherever it appears in the image, because
it's literally the same weights being applied at every location. This
is the inductive bias: you're telling the network, before it's seen a
single example, "whatever pattern matters, it can occur anywhere in the
image and should be recognized the same way regardless." For images,
that assumption is almost always true (a cat is a cat whether it's in
the top-left or center), which is exactly why it works so well — it's
not a generic trick, it's a correct prior for this specific data type.

**Stacking conv layers builds a feature hierarchy, replacing hand
engineering.** In 21.1 you hand-built features (TF-IDF, bag-of-words)
because you understood the domain well enough to know what mattered.
Images don't offer an equivalent obvious feature set — "pixel 4,782 is
bright" means nothing on its own. Early conv layers learn low-level
features like edges and color blobs; layers built on top of those
combine them into textures and simple shapes; layers on top of *that*
combine shapes into object parts. The network is learning its own
feature engineering, layer by layer, driven by nothing but the gradient
of the loss — this is the actual meaning of "deep" learning.

**Pooling (typically max pooling) downsamples between conv layers**,
keeping the strongest activation in each small region and discarding the
rest. This does two things: it shrinks the spatial size (less
computation, fewer parameters downstream), and it adds a small amount of
additional positional slack — a feature detected slightly off from
where pooling expects it still survives, because pooling only cares
about the max in a neighborhood, not the exact position within it.

**Depth increases the effective receptive field.** A single 3x3 kernel
only "sees" a 3x3 patch of the input. But a second 3x3 conv layer stacked
on top of the first sees a 3x3 patch *of the first layer's output* —
which itself each depended on a 3x3 patch of the original image. Stack
enough layers and a neuron deep in the network is effectively influenced
by a large region of the original input, without ever using a large,
expensive kernel directly. This is why deep stacks of small kernels
generally outperform a single shallow layer of large kernels — more
nonlinearity, fewer parameters, same effective coverage.

**Loss curves are how you'll actually catch this going wrong.** Once
training starts, watch train and validation loss together: both
dropping together means the network is learning something general;
train loss still dropping while validation loss climbs back up is the
concrete signature of overfitting — the network has started memorizing
training examples rather than learning the translation-invariant
features above. 22.1's acceptance criteria requires you to show and
explain this curve for exactly this reason.

## Required reading

Per `ROADMAP.md`'s Stage 22 resource table — Stanford
[CS231n](http://cs231n.stanford.edu/)'s lecture and notes on
convolutional neural networks are the deep-dive on everything above
(receptive fields, parameter sharing, pooling math). For the
practical, code-first path straight into PyTorch, pair it with
[fast.ai's Practical Deep Learning](https://course.fast.ai/) course,
lesson 1.

## Check yourself

1. A fully-connected network and a CNN are both trained on centered,
   32x32 images and both reach 95% accuracy. The CNN keeps that accuracy
   when test images are shifted 5 pixels off-center; the fully-connected
   network's accuracy collapses. Explain why, in terms of what each
   architecture actually learned.
2. Why does parameter sharing reduce the parameter count *and* improve
   generalization simultaneously, rather than trading one for the other?
3. If you stack three 3x3 conv layers with no pooling in between, what's
   the effective receptive field (in original-image pixels) of a single
   output neuron at the top, and why isn't it just 3x3?
4. Your training loss keeps dropping smoothly across 50 epochs while
   your validation loss bottoms out at epoch 12 and then rises. What's
   happening, and what does it have to do with the "translation
   invariance is a correct prior for images" argument above — is the
   model's *architecture* the problem here, or something else?
5. Why would applying the exact same convolutional inductive bias
   (translation invariance) to something like tabular financial data
   likely be a *wrong* assumption, unlike with images?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 22.1 — Image Classifier**
(`projects/22.1-image-classifier/SPEC.md`). Start there.
