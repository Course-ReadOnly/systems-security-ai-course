> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached.

# Project 24.1 — Blockchain From Scratch

## Goal

Before touching Solidity or Ethereum, build the actual mechanism a
blockchain is: a chain of blocks, each cryptographically linked to the
one before it, with a consensus rule that makes tampering expensive.
Done in Python or Go (reusing Stage 17/18), this turns "blockchain"
from a buzzword into code you wrote and can reason about — which is
what makes the rest of this stage make sense instead of feeling like
memorized vocabulary.

## Requirements

1. A `Block` structure containing: an index, a timestamp, transaction
   data (can be arbitrary strings/simple structs — this isn't about
   transaction semantics yet), the previous block's hash, and its own
   hash.
2. Each block's hash is a real cryptographic hash (SHA-256 is fine) of
   its own contents **including** the previous block's hash — this is
   what makes the chain a chain, not just a list.
3. A simple proof-of-work: mining a block requires finding a nonce such
   that the block's hash meets a difficulty target (e.g. starts with N
   zero bits). Implement the mining loop yourself.
4. A chain validation function that walks the whole chain and verifies:
   every block's stored `previous_hash` actually matches the previous
   block's real hash, and every block's own hash is still valid given
   its contents (i.e., nobody edited a block's data after mining it).
5. Demonstrate tampering detection: modify a transaction in an
   already-mined block (without re-mining) and show your validator
   correctly flags the chain as invalid — then show what re-mining
   that block and every block after it would require (you don't have
   to actually re-mine the whole chain, just explain/demonstrate the
   cost scales with chain length).

## Acceptance criteria

- [ ] Real SHA-256 (or equivalent) hashing, chained through
      `previous_hash` correctly
- [ ] Working proof-of-work mining loop with an adjustable difficulty
      target
- [ ] Chain validator that correctly accepts an untampered chain and
      rejects a tampered one
- [ ] Demonstrated tampering-detection run (paste the before/after
      validator output)
- [ ] `git log` shows real iteration
- [ ] README explains, in your own words, why an attacker would need
      to re-mine every subsequent block to make a tampered chain
      validate again — and why that's the actual security property a
      blockchain provides

## Security relevance

Already this project's entire point: the hash-chain is a tamper-evidence
mechanism, not tamper-*prevention* — anyone can still edit a block, the
protocol just makes that edit immediately detectable and expensive to
hide. This is the load-bearing security property everything in the
rest of Stage 24 builds on top of; 24.4/24.5's exploits never attack
the chain mechanics themselves, they attack application logic (smart
contracts) built on top of an already-sound foundation.

## When done

Point me at the source, `git log`, and the tampering-detection output.
I'll ask you to explain what would happen to your validator's output
if two blocks were mined with the same `previous_hash` (a fork) —
that's the concept this toy version doesn't need to fully solve, but
you should be able to reason about it.
