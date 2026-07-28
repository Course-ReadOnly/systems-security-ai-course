> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 21.1 — Spam Detector

## Goal

The classic first-ML-project, done properly: a real classifier
evaluated with real metrics, not just "accuracy looked fine." This is
where the difference between accuracy and precision/recall stops being
a lecture slide — spam datasets are exactly the kind of class-imbalanced
problem where accuracy alone lies to you.

## Requirements

1. Train a classifier (logistic regression or Naive Bayes are the
   standard, appropriate choices here — a full neural net is
   overkill and belongs in Stage 22) on a real, public spam/ham email
   dataset.
2. A real train/test split (**not** evaluating on the same data trained
   on) — and ideally cross-validation, not just one split.
3. Report **precision, recall, and F1**, not just accuracy — and explain
   in the README why accuracy alone is misleading for this dataset
   specifically (check the class balance and say what it is).
4. Basic feature engineering from raw email text (e.g. bag-of-words/
   TF-IDF) — understand what your features actually represent, not just
   call a library function blindly.
5. Inspect at least a few misclassified examples (false positives and
   false negatives) and reason about *why* the model got them wrong.

## Acceptance criteria

- [ ] Trains successfully on a real public dataset (cite which one)
- [ ] Paste precision/recall/F1 (and accuracy, for comparison) on a
      genuine held-out test set
- [ ] Class balance of the dataset stated, with a sentence on why
      accuracy alone would be misleading given that balance
- [ ] At least 2 misclassified examples (one false positive, one false
      negative) shown with your reasoning about why
- [ ] `git log` shows iteration
- [ ] README explaining the feature representation used

## Security relevance

Spam filtering is adversarial ML in its original, oldest form — spammers
actively adapt their content specifically to evade whatever filter is
currently deployed, which is why a static model's accuracy degrades
over time in production even with no code changes. The precision/recall
tradeoff you're forced to reason about here (Requirement 3) is the same
tradeoff 12.3's YARA rules and 14.1's Sigma rules face: a false positive
(blocking real mail) has a different cost than a false negative (spam
getting through), and the "right" threshold depends on which cost
matters more to whoever's using the tool.

## When done

Point me at the source + `git log`. I'll check the train/test split is
genuinely held-out (no leakage) and that the metrics reported actually
match what the confusion matrix would show — a suspiciously perfect
score is usually a leakage bug, not a good model.
