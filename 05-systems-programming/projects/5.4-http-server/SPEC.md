> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 5.4 — An HTTP Server

## Goal

Sockets, applied to a protocol you already use daily. Parse real HTTP
requests, generate real HTTP responses, over raw TCP sockets — no
framework. Direct prep for Stage 9's networking work and a genuinely
useful thing to have built once.

## Requirements

1. Listens on a TCP port, accepts connections (`socket`/`bind`/`listen`/
   `accept`).
2. Parses a real HTTP/1.1 request: method, path, headers (at minimum
   `Host` and `Content-Length` if a body is present).
3. Handles `GET` and `POST` at minimum, responding with correct status
   lines (`200`, `404`, `400` for malformed requests) and headers.
4. Serves at least one dynamic route (e.g. `/echo` reflecting POST body,
   or `/time` returning the current time) — not just static files (that's
   5.5's job).
5. **Concurrency**: handles more than one client — either via your 5.3
   thread pool, `fork`-per-connection, or an event loop (`epoll`) — pick
   one and justify it in the README.
6. Doesn't crash on malformed/partial requests (a client that sends
   garbage or disconnects mid-request).

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Paste `curl` output against your server for `GET` and `POST` on
      your dynamic route(s), showing correct status/body
- [ ] Malformed-request case tested (e.g. `curl` with a broken request,
      or `nc` sending garbage) — server stays up, responds with `400` or
      closes cleanly, doesn't crash
- [ ] Concurrency demonstrated: multiple simultaneous clients (e.g. `curl`
      in parallel, or `ab`/`wrk` if available) handled correctly, not
      serialized or dropped
- [ ] `git log` shows iteration
- [ ] README documenting the concurrency model chosen and why

## When done

Point me at the source + `git log`. I'll check the HTTP parsing against
malformed/partial input first (real clients send weird things), then the
concurrency model's actual correctness under simultaneous load.
