> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 9.1 — Chat Server

## Goal

A multi-client TCP chat server — the canonical "many simultaneous
connections, broadcast to all of them" networking project. Builds
directly on Stage 5's concurrency-model decision (thread pool vs.
`epoll`), now applied to persistent, long-lived connections instead of
request/response HTTP.

## Requirements

1. TCP server accepting multiple simultaneous client connections.
2. Broadcasts each client's message to all other connected clients.
3. Handles clients connecting/disconnecting at arbitrary times without
   crashing or corrupting state for remaining clients.
4. A real concurrency model (thread-per-client, thread pool, or
   `epoll`/`select` event loop) — document the choice and why.
5. A minimal client (can be as simple as using `nc`, or a small purpose-
   built client) to actually demonstrate multi-party chat.

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] Paste/describe a session with **3+ simultaneous clients**, showing
      messages from each reaching all others
- [ ] A client disconnecting mid-session tested — server continues
      operating correctly for remaining clients
- [ ] Resource cleanup confirmed on disconnect (no leaked sockets/threads
      accumulating — demonstrate with repeated connect/disconnect cycles)
- [ ] `git log` shows iteration
- [ ] README documenting the concurrency model and why

## Security relevance

A shared client list mutated concurrently from multiple connection
threads is a textbook data race (see `SECURITY-CONCEPTS.md`'s "Race
Conditions" entry) — the same class of bug as a TOCTOU, just with
"iterate the list" and "a client disconnects" as the two racing
operations instead of a file check and a file use. This project also
has zero authentication by design (anyone who can reach the port can
join and broadcast) — worth noticing explicitly as a real design
tradeoff, not an oversight, since Stage 13 will spend real time on
exactly what happens once you add auth to something like this.

## When done

Point me at the source + `git log` and the multi-client session
evidence. I'll check the broadcast logic's thread-safety first (a shared
client list being iterated while modified is the classic bug here).
