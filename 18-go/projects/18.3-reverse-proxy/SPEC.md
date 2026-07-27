> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 18.3 — Reverse Proxy

## Goal

The mirror image of Stage 9.2's forward HTTP proxy: a reverse proxy
sitting in front of one or more backend servers, routing incoming
requests to them. Go's standard library has real support for this
(`httputil.ReverseProxy`) — the point is understanding what it's doing
under the hood, not just calling it.

## Requirements

1. Accepts incoming HTTP requests and forwards them to a configured
   backend server, relaying the response back correctly.
2. Supports **routing to more than one backend** based on some rule
   (e.g. path prefix, or a simple round-robin across multiple instances
   of the same backend — pick one).
3. Correctly relays/rewrites headers where needed (e.g. `Host` header
   handling is a common correctness pitfall for reverse proxies).
4. Handles a backend being down (connection refused) — clear error
   response to the client (e.g. `502`), proxy itself stays up.

## Acceptance criteria

- [ ] Builds/runs cleanly
- [ ] Paste requests routed to at least two different backends (by
      path or round-robin), showing correct relay of both
- [ ] Backend-down case tested, `502`-equivalent response confirmed,
      proxy doesn't crash
- [ ] `git log` shows iteration
- [ ] README explaining the routing rule chosen

## When done

Point me at the source + `git log`. I'll check header handling (`Host`,
`X-Forwarded-For` if implemented) and the down-backend case first —
these are the parts of a reverse proxy that look fine in a happy-path
demo and break in real deployment.
