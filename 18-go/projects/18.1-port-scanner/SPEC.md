> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 18.1 — Port Scanner (Go)

## Goal

Redo Stage 9.3's port scanner in Go — the comparison is the point:
goroutines + channels for concurrency instead of manually managed
threads. Same scope-of-use rules as 9.3 apply.

## Requirements

1. Scans a target host across a port range, using goroutines for
   concurrent scanning (a worker-pool pattern via channels, not one
   unbounded goroutine per port on a huge range).
2. Configurable timeout per port/connection.
3. Same permission scope as 9.3: only scan hosts you own/control.
4. **Stretch:** benchmark against your 9.3 C version on the same target/
   port range — compare wall-clock time and code complexity/length.

## Acceptance criteria

- [ ] Builds/runs cleanly (`go build`, no vet warnings)
- [ ] Paste a scan against a host you control, cross-checked against
      `ss -tlnp`/`netstat` for agreement
- [ ] Timeout behavior demonstrated
- [ ] If benchmarked against 9.3: paste the comparison
- [ ] `git log` shows iteration
- [ ] README stating what was scanned, confirming permission

## When done

Point me at the source + `git log`. I'll check the goroutine/channel
pattern specifically — an unbounded `go func()` per port without a
worker-pool limit can misbehave badly on large ranges, which is exactly
the kind of Go-specific mistake this project should surface.
