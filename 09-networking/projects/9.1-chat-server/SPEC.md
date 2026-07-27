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

## When done

Point me at the source + `git log` and the multi-client session
evidence. I'll check the broadcast logic's thread-safety first (a shared
client list being iterated while modified is the classic bug here).
