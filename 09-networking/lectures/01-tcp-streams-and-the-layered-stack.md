> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 9.01 — TCP Streams and the Layered Stack

## Why this matters

Stage 5's HTTP server already opened a raw socket and spoke a text
protocol over it, but it stayed narrow — accept one connection, handle
one request, close. This stage generalizes that into the full picture:
what a socket actually is, what promise TCP makes that IP doesn't, and
exactly where that promise leaks once you're holding *many* long-lived
connections open at once instead of one short-lived request/response.
Stage 13 (Offensive Security) assumes this is second nature — you can't
scan, spoof, or sit in the middle of traffic you don't understand the
layering of — and you can't write a correct chat server (9.1) without
understanding the one fact this lecture is about: TCP delivers bytes,
not messages.

## Core concepts

**Each layer is a promise, and the promise is only as good as the layer
making it.** Ethernet promises to get a frame to another machine on the
same physical segment, nothing more. IP stacks on top and promises to
route a packet across *any* number of networks to reach a distant host —
but explicitly makes no promise about whether it arrives, arrives once,
or arrives in order. It's "best-effort" by design: routers drop packets
under congestion, links flap, packets take different paths and can
arrive out of sequence. Every layer above IP exists to either accept
that unreliability (UDP) or paper over it (TCP).

**TCP's entire job is manufacturing a reliable, ordered byte stream on
top of IP's unreliable, unordered packets.** It does this with
mechanics you should be able to name, not just wave at: sequence numbers
(so the receiver can detect gaps and reorder), acknowledgments (so the
sender knows what actually arrived), retransmission on timeout (so lost
packets get resent), and a sliding window (so the sender doesn't
overwhelm the receiver or the network). This machinery is *why* TCP has
a three-way handshake and connection state at all, where UDP just fires
packets — TCP is tracking a stream's worth of bookkeeping that IP itself
knows nothing about.

**The promise TCP makes is "a stream of bytes, reliably and in order" —
explicitly not "your messages, intact."** This is the single fact that
breaks more chat-server implementations than anything else. A `send()`
call handing 40 bytes to the kernel does not mean the corresponding
`recv()` on the other end returns those same 40 bytes in one call.
TCP is free to coalesce two back-to-back sends into one `recv()`, or to
hand back only 12 of your 40 bytes now and the rest on a later call —
both are correct, promise-honoring TCP behavior, not bugs. If your
protocol has no way to tell where one message ends and the next begins,
you cannot reliably parse what you receive. This is why every real
line-oriented protocol (SMTP, HTTP's headers, your 9.1 chat protocol)
picks an explicit framing scheme — a delimiter like `\n` you scan for,
or a length prefix you read first — and buffers partial reads until a
full frame is available. Framing isn't an advanced feature; it's the
minimum tax for using a byte-stream transport for anything message-
shaped at all.

**A port is a transport-layer concept, not a network-layer one.** IP
addresses a machine; a port disambiguates *which process on that
machine* a given stream or datagram belongs to. This only exists because
TCP and UDP headers carry a source and destination port field — IP
itself has no notion of "port," which is why NAT and firewalls that
filter by port are doing transport-layer inspection, not routing.

**Handling many simultaneous connections is a concurrency problem TCP
does not solve for you.** The socket API hands you one file descriptor
per connection; deciding how to service N of them concurrently —
thread-per-client, a thread pool, or a single-threaded `epoll`/`select`
event loop — is the exact decision Stage 5 already forced you to
justify, now under a harder constraint: connections are long-lived, not
one-shot, so a shared list of "currently connected clients" is being
read and mutated concurrently, and getting that wrong (iterating the
list on one thread while another thread is adding or removing from it)
is the classic chat-server bug.

## Required reading

Per Stage 9's resource table: [Beej's Guide to Network
Programming](https://beej.us/guide/bgnet/), the "System Calls or Bust!"
section covering `socket()`, `bind()`, `listen()`, `accept()`, and
especially `send()`/`recv()` — read the note there about partial sends
carefully, it's the section that directly explains the framing problem
above.

## Check yourself

1. Why can a single `recv()` call on a TCP socket return only part of a
   message that was written in one `send()` call, with the rest arriving
   on a *later* `recv()` — and what does that force you to build at the
   application layer?
2. If you rewrote 9.1's chat server over UDP instead of TCP, name two
   failure modes that become possible in a 3-client conversation that
   TCP rules out by design.
3. Two clients send messages to your chat server at nearly the same
   instant. What actually determines the order your server processes
   them in — the network, the OS, or your concurrency model?
4. Why does a client disconnecting *cleanly* versus dying mid-write
   matter to the other connected clients' `recv()` calls?
5. A port number identifies a process endpoint. At which layer does a
   port number actually exist, and why does that make "IP addresses the
   machine, the port addresses the app" more precise than a hand-wave?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 9.1 — Chat Server**
(`projects/9.1-chat-server/SPEC.md`). Start there.
