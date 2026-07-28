# Sample Data

Small, reusable test fixtures for exercises that need real input instead
of inventing your own each time.

- **`sample-text.txt`** — a short multi-paragraph text sample with
  repeated words, a contraction (apostrophe-handling gotcha), and one
  deliberately long line — useful for text-processing exercises (word
  frequency, longest-line detection, grep/sed/awk practice).

This directory is for generic, cross-stage test data only. Stage-
specific fixtures (sample config/INI/JSON/CSV files, log samples,
IOC feeds, etc.) live under each project's own folder, at
`{project}/samples/`, so they stay next to the `SPEC.md` that
references them. As of 2026-07-28 (per explicit learner request —
"samples for where it's needed," same bulk-generation exception as the
rest of the roadmap, see `STATUS.md`) several of these were added ahead
of schedule rather than waiting for the stage to be reached:

- `01-c-programming/projects/1.6-config-parser/samples/`
- `01-c-programming/projects/1.7-ini-parser/samples/`
- `01-c-programming/projects/1.8-json-parser/samples/`
- `01-c-programming/projects/1.11-csv-library/samples/`
- `14-defensive-security/projects/14.3-log-parser/samples/`
- `17-python/projects/17.2-ioc-parser/samples/`

Not every project gets one, and that's deliberate, not an oversight —
skipped where a real external source is the actual point (Stage 12's
malware samples, Stage 14.2's LetsDefend exercises, Stage 20-22's
real ML/DL datasets — faking those would undermine what the project's
acceptance criteria actually test) or where the input format doesn't
exist yet (Stage 4's toy ISA, designed by the learner when reached).
All values in the provided fixtures are synthetic (RFC 5737
documentation IP ranges, `.test` domains, made-up hashes) — never real
infrastructure or actual malware artifacts.
