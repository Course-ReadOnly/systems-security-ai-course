> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 9.2 — HTTP Proxy

## Goal

Sit in the middle: accept a client's HTTP request, forward it to the
real destination server, relay the response back. This is the
plumbing behind tools you'll rely on constantly from Stage 13 onward
(Burp Suite and similar are, at their core, exactly this).

## Requirements

1. Accepts an HTTP request from a client, parses the target host from
   it, opens a **new** connection to that real destination server, and
   forwards the request.
2. Relays the destination's response back to the original client
   correctly (status line, headers, body).
3. Handles `Connection: keep-alive` behavior sensibly (or explicitly
   documents choosing `Connection: close` for simplicity — a real,
   stated tradeoff either way).
4. Handles the destination server being unreachable (connection refused/
   timeout) — clear error surfaced to the client, proxy doesn't hang or
   crash.
5. **Stretch:** log/print each proxied request (method + host + path) —
   the "visibility" feature that makes a proxy useful for the security
   work coming in Stage 13.

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] Paste a real browser or `curl` request routed through your proxy to
      a real website, showing correct end-to-end relay of the response
- [ ] Unreachable-destination case tested and handled cleanly
- [ ] `git log` shows iteration
- [ ] README documenting the keep-alive decision made

## When done

Point me at the source + `git log`. I'll check header-relay correctness
first (a proxy that mangles `Content-Length` or drops headers silently
breaks things in ways that are easy to miss on a quick test).
