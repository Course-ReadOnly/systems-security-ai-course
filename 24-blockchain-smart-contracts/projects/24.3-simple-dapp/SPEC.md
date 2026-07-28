> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached.

# Project 24.3 — Simple DApp

## Goal

Connect 24.2's contract to something a user actually interacts with —
a small decentralized application, closing the loop from "I deployed a
contract" to "something can actually call it." A CLI is enough; a web
frontend is a reasonable stretch if you want it.

## Requirements

1. A client (CLI or minimal web frontend) that connects to your 24.2
   ERC-20 contract on the testnet via a web3 library (`ethers.js`,
   `web3.py`, or equivalent).
2. Support at minimum: checking a wallet's token balance, sending a
   transfer, and approving/executing a `transferFrom` — i.e., exercise
   every function you tested in 24.2, but from a real client instead of
   a test harness.
3. Handle the asynchronous, sometimes-slow nature of blockchain
   transactions correctly: don't report "success" until the transaction
   is actually confirmed (has a receipt), and handle a reverted
   transaction (e.g. insufficient balance) as a distinct, clearly
   reported outcome rather than a generic error.
4. Read contract state (balances, allowances) via a read-only call, not
   by re-deriving it from watching every past transaction yourself.

## Acceptance criteria

- [ ] Client successfully reads balance and executes a transfer against
      your live testnet contract (paste the transaction hash and a
      link to the testnet explorer showing it confirmed)
- [ ] A deliberately-failed transaction (e.g. transfer more than the
      balance) is caught and reported clearly, not left as a raw
      exception/stack trace
- [ ] `approve` + `transferFrom` flow demonstrated end-to-end from the
      client
- [ ] `git log` shows real iteration
- [ ] README explains the difference between a transaction being
      "sent" and being "confirmed," and how your client distinguishes
      the two

## Security relevance

The sent-vs-confirmed distinction this spec requires you to handle
correctly is a real, exploited category of bug in production DApps —
a client (or worse, another smart contract) that acts on an
unconfirmed transaction can be misled by a transaction that later
reverts, gets replaced, or lands in a different order than expected.
Getting this right here is direct preparation for reasoning about
transaction-ordering attacks (front-running, sandwich attacks) that
Damn Vulnerable DeFi (24.5) explores from the attacker's side.

## When done

Point me at the source, `git log`, and the testnet explorer links for
at least 2 real transactions (one success, one deliberate failure).
I'll check that you're actually waiting for a transaction receipt
before reporting success — a client that reports "done" the moment a
transaction is submitted (before it's mined) is a real, common bug in
this domain.
