> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 9.4 — Packet Sniffer

## Goal

Capture and parse real network packets off the wire (raw sockets or
`libpcap`), down to the Ethernet/IP/TCP header level. This is where the
protocol stack you've read about (Beej's Guide, CS144) becomes bytes you
personally parsed — the same skill Stage 14's network-monitoring tools
(Zeek/Suricata) are built on top of, at a much larger scale.

## Requirements

1. Captures live packets on a network interface (raw sockets with
   `CAP_NET_RAW`, or `libpcap`/`pcap.h` — either is fine, document which).
2. Parses at minimum: Ethernet header (MACs, ethertype), IP header
   (src/dst, protocol), and TCP **or** UDP header (ports).
3. Prints a readable summary per packet (source/dest IP:port, protocol,
   size) — not raw hex dumps as the primary output.
4. Correctly handles non-IP or non-TCP/UDP traffic (doesn't crash trying
   to parse a TCP header out of a UDP or ARP packet).
5. Only capture on your own machine/network you control — same
   permission boundary as 9.3.

## Acceptance criteria

- [ ] Builds/runs cleanly (likely needs elevated privileges to open raw
      sockets — note this in the README)
- [ ] Paste output capturing real traffic you generated yourself (e.g.
      `curl` or `ping` while the sniffer runs), showing correctly parsed
      addresses/ports/protocol
- [ ] Cross-check a captured session against `tcpdump`/`wireshark`
      output for the same traffic, confirming your parse agrees
- [ ] Mixed-protocol traffic tested (some TCP, some UDP, some other) —
      handled without crashing on the ones you don't fully parse
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log` and the `tcpdump` cross-check — that
comparison is the actual proof your header parsing is byte-correct, not
just "prints something plausible."
