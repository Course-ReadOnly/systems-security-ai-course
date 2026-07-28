> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 21.01 — Precision, Recall, and Why Accuracy Lies

## Why this matters

Stage 19 gave you the math; this is where it turns into a number you can
be wrong about. Every classifier you build from here on — spam, malware
in 21.2, the binary classifier in 25.4 — sits on a dataset where the
"interesting" class (spam, malicious) is a small minority of the total.
Report the wrong metric on data shaped like that and you can ship a
classifier that is simultaneously "99% accurate" and completely useless.
This isn't a niche statistics footnote; it's the single most common way
a first ML project's results turn out to be dishonest, and 21.1's
acceptance criteria is built specifically to catch it.

## Core concepts

**Start from the confusion matrix**, not accuracy. Every prediction on a
binary problem lands in one of four buckets: true positive (correctly
flagged spam), false positive (ham wrongly flagged spam), true negative
(correctly passed ham), false negative (spam wrongly passed as ham).
Every metric worth reporting is built from these four counts — memorize
the 2x2 grid before anything else.

**Accuracy is `(TP+TN)/total`, and that formula has a blind spot: it
doesn't care which class the errors land in.** If your spam dataset is
1% spam / 99% ham (a realistic split), a classifier that outputs "ham"
for *everything*, ignoring the input entirely, scores 99% accuracy. It
also has zero value — it never once catches spam. This is the trap:
accuracy looks like it's measuring "is the model good" when on
imbalanced data it's actually measuring "how imbalanced is the data."
Always state the class balance before reporting accuracy at all, per
21.1's requirements — the number is meaningless without it.

**Precision and recall each ask a different, class-aware question.**
Precision = `TP/(TP+FP)`: of everything you flagged as spam, how much
actually was? Recall = `TP/(TP+FN)`: of everything that actually was
spam, how much did you catch? A model can max out one by gutting the
other — flag *everything* as spam and recall hits 100% while precision
collapses; flag *nothing* and precision is vacuously perfect while
recall is zero. Neither extreme is a working classifier, which is why
you report both, never either alone.

**F1 is the harmonic mean of precision and recall specifically because
harmonic means punish imbalance between the two.** The arithmetic mean
of 1.0 and 0.0 is 0.5, which would make the "flag everything" classifier
above look mediocre-but-okay. The harmonic mean of the same pair is 0 —
it's dominated by whichever number is smaller, so a model can't hide a
collapsed precision or recall behind a good score on the other. That's
the entire reason F1 exists as a single number instead of just averaging.

**The precision/recall tradeoff is a real dial, not a fixed property of
the model.** Most classifiers output a probability, then threshold it
(e.g. `>0.5 = spam`) to get a hard label. Move that threshold down and
you flag more things as spam — recall goes up, precision goes down. Move
it up and the reverse happens. Where you *set* that threshold is a
domain decision, not a math one: for spam, a false positive (a real
email buried in the spam folder) is often worse to a user than a missed
spam message, so you'd bias toward precision. For malware — the theme of
21.2, and the direct subject of 25.1's triage tool — a missed detection
can be far more costly than an analyst wasting time on a false alarm, so
the bias usually flips toward recall. There's no universally "correct"
threshold; there's only a threshold that matches what an error actually
costs in that domain.

**None of this means anything if it's measured on data the model
trained on.** A held-out test set (21.1 requires this explicitly) exists
because a model can trivially memorize its training data and report
perfect precision/recall on it while generalizing to nothing. A
suspiciously perfect score is a leakage bug far more often than it's a
good model — check the split before you trust the metric.

## Required reading

Per `ROADMAP.md`'s Stage 21 resource table — [StatQuest's](
https://www.youtube.com/c/joshstarmer) videos on the confusion matrix,
sensitivity/specificity, and ROC/AUC cover exactly this material with
the clearest visual intuition of the three listed resources; watch those
before touching precision/recall in code. If you want the fuller
mathematical treatment of why logistic regression's output can be read
as a probability at all, that's in Andrew Ng's course (Coursera) or CS229's
notes on generalized linear models.

## Check yourself

1. A malware classifier trained on a dataset that's 99.5% benign
   reports 99.5% accuracy. What's the one-line sanity check that tells
   you whether that number means anything?
2. Construct a confusion matrix (made-up numbers are fine) where
   accuracy is high but F1 is low. What does that combination tell you
   about which class the model is failing on?
3. Why does moving a classification threshold that increases recall
   necessarily risk decreasing precision — walk through what happens to
   the false-positive count as the threshold drops toward 0.
4. For 21.2's malware classifier specifically, would you argue for
   optimizing toward precision or recall as the primary metric, and why
   — what does a false negative cost versus a false positive in that
   domain?
5. Your model gets 100% precision and 100% recall on the test set. Before
   celebrating, what's the first thing you should check?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 21.1 — Spam Detector**
(`projects/21.1-spam-detector/SPEC.md`). Start there.
