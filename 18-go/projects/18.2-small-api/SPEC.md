> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 18.2 — Small API

## Goal

A real REST API in Go — CRUD over HTTP with a real router and JSON,
using Go's standard library (`net/http`) rather than reaching
immediately for a framework, so the underlying mechanics stay visible.

## Requirements

1. At least one resource with full CRUD (Create/Read/Update/Delete) over
   HTTP, using JSON request/response bodies.
2. Correct status codes (`200`/`201`/`404`/`400`) for each case, not
   just `200` for everything.
3. Input validation on write endpoints (malformed JSON or missing
   required fields → `400`, not a panic/500).
4. Persists data somewhere real between requests (even an in-memory
   store with a mutex for concurrent-safety is fine — a real database is
   a reasonable stretch goal, not required).
5. Concurrent-safe if using in-memory storage — multiple simultaneous
   requests must not race on the shared data.

## Acceptance criteria

- [ ] Builds/runs cleanly
- [ ] Paste `curl` sessions covering full CRUD with correct status codes
      for each
- [ ] Malformed-input case tested (bad JSON, missing field) — `400`
      returned, not a crash
- [ ] If in-memory + concurrent: run under Go's race detector
      (`go run -race`) under concurrent load, paste output showing no
      races
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log` and the race-detector output if
applicable. I'll check status-code correctness across the full CRUD
surface and the concurrent-safety of shared state specifically.
