> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 22.1 — Image Classifier

## Goal

The canonical first deep-learning project: a CNN in PyTorch, trained
end to end, evaluated properly. This is where Stage 19's calculus
(gradients, backprop) and Stage 21's train/test discipline both get
applied to a model that actually learns its own features.

## Requirements

1. A CNN built in PyTorch (not a pretrained model used as a black box —
   build and train your own architecture, even if simple, so you
   understand the pieces).
2. Trained on a real, standard image dataset (e.g. CIFAR-10 or
   Fashion-MNIST — something with enough real difficulty to be
   meaningful, MNIST digits alone is too easy to prove much).
3. Proper train/validation/test split — **validation set used for
   tuning, test set touched only once at the end** (this discipline
   matters more here than in 21.1, since it's easier to overfit to a
   test set by iterating against it repeatedly).
4. Track and plot training/validation loss over epochs — able to show
   (and explain) whether/when overfitting starts.
5. Report final test accuracy, plus a confusion matrix to see which
   classes get confused with which.

## Acceptance criteria

- [ ] Trains successfully in PyTorch, GPU or CPU (note which)
- [ ] Loss curves (train + validation) pasted/plotted, with a sentence
      on what they show (converging cleanly? overfitting after epoch N?)
- [ ] Final test-set accuracy reported, confusion matrix included
- [ ] Confirm the test set was used only once, at the end — describe
      your train/val/test discipline in the README
- [ ] `git log` shows iteration
- [ ] README explaining the architecture (layers, why this shape)

## When done

Point me at the source + `git log` and the loss curves/confusion matrix.
I'll check for test-set leakage first (tuning against test accuracy
repeatedly is the most common way this project's results end up
dishonest) before looking at the architecture itself.
