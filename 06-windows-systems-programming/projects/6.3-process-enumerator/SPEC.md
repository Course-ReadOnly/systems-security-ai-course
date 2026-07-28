> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 6.3 — Process/Module Enumerator

## Goal

Read-only system introspection using `CreateToolhelp32Snapshot` — the
same *shape* of tool (list running processes, list loaded modules per
process) you'll build again, more seriously, in Stage 12 for malware
triage. This version is deliberately just informational, no
injection/manipulation.

## Requirements

1. Enumerates all running processes (`CreateToolhelp32Snapshot` +
   `Process32First`/`Process32Next`) — prints PID, parent PID, and image
   name for each.
2. For at least one target process, enumerates its **loaded modules**
   (DLLs) via a module snapshot — prints module name and base address.
3. Handles processes you don't have permission to inspect (e.g. system
   processes) gracefully — skip with a note, don't crash the whole
   enumeration.
4. Correctly closes every snapshot handle.

## Acceptance criteria

- [ ] Builds cleanly
- [ ] Paste output of a full process listing from a real run of your
      machine, cross-checked against Task Manager's process list for
      agreement (at least spot-check a few PIDs/names match)
- [ ] Paste module-enumeration output for a real process (e.g. your own
      shell or a browser), showing several real DLLs with base addresses
- [ ] Permission-denied case handled and demonstrated (a system process
      you can't open)
- [ ] `git log` shows iteration

## Security relevance

This read-only enumeration is the exact reconnaissance step that
precedes process injection: an attacker (or a legitimate EDR tool
doing the same thing defensively) has to enumerate processes and their
loaded modules *before* picking a target to inject into or hook — you
can't inject into a process you haven't first identified. Building the
"list what's running" half yourself here is what makes Stage 12's more
serious malware-analysis tooling, and eventually the injection
techniques Stage 13 covers from the offensive side, feel like natural
extensions rather than opaque API calls.

## When done

Point me at the source + `git log`. I'll check that snapshot handles are
actually released (`CloseHandle`) in every code path, including error
paths — a snapshot handle leak in a loop-based enumerator adds up fast.
