> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 9.3 — Port Scanner

## Goal

A real TCP port scanner — direct, hands-on prep for Stage 13
(Offensive Security) recon work. **This must only ever be run against
hosts/networks you own or have explicit permission to scan** — scanning
systems you don't control is a real legal/ethical line, not a formality.

## Requirements

1. Scans a target host across a range of ports, reporting open/closed
   (a basic TCP connect scan is sufficient — SYN scanning requires raw
   sockets and is a reasonable stretch goal, not required).
2. Concurrent scanning (a scan doing one port at a time serially over a
   large range is impractically slow) — use threads or async I/O.
3. Configurable timeout per port (a host that silently drops packets
   shouldn't hang the whole scan).
4. Clear, readable output: which ports are open, on which host.
5. **Only test against `localhost`/a VM/container you control**, or a
   host explicitly set up for this purpose (e.g. a deliberately
   vulnerable local lab VM) — document what you tested against.

## Acceptance criteria

- [ ] Builds/runs cleanly, no warnings
- [ ] Paste a scan against a host you control (e.g. your own machine)
      with known open ports, showing correct detection — cross-check
      against `ss -tlnp`/`netstat` on that same host for agreement
- [ ] Timeout behavior demonstrated (a filtered/unresponsive port
      doesn't stall the whole scan)
- [ ] `git log` shows iteration
- [ ] README stating explicitly what was scanned and confirming it was
      systems you own/control

## Security relevance

Already the load-bearing point of this project (Requirement 5 and the
Goal's opening line): this is literally the reconnaissance tool Stage
13's exploitation work depends on, and the same tool that makes
unauthorized scanning a real legal exposure, not just bad manners. The
scope discipline you build here (own systems only, stated explicitly
in every README) is the exact habit this course expects to carry
forward unprompted into every later offensive-security project.

## When done

Point me at the source + `git log` and the cross-check against `ss`/
`netstat`. I'll check the concurrency approach doesn't silently drop or
miscount ports under load, and confirm the scope-of-use note is present
and accurate.
