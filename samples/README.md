# Sample Data

Small, reusable test fixtures for exercises that need real input instead
of inventing your own each time.

- **`sample-text.txt`** — a short multi-paragraph text sample with
  repeated words, a contraction (apostrophe-handling gotcha), and one
  deliberately long line — useful for text-processing exercises (word
  frequency, longest-line detection, grep/sed/awk practice).

Stage-specific fixtures (sample C source, binaries, etc.) get added
under each stage's own project folder as that stage is actually reached,
not here — this directory is for generic, cross-stage test data only.
