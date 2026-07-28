> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 24.01 — Blockchains and Smart Contract Security

## Why this matters

"Blockchain" gets thrown around as a buzzword precisely because most
people who use the word have never built one — it stays magic. This
stage exists to remove that: by the end of 24.1 you'll have written the
actual mechanism yourself, and by the end of 24.4 you'll have exploited
real vulnerability classes in real (if intentionally broken) contracts.
That second half is the point of placing this stage where it is —
smart contracts are the one domain in software engineering where a bug
is a direct, immediate, and often irreversible transfer of real money
to whoever finds it first. The reverse-engineering and exploitation
mindset from Stages 11-13 applies here almost unchanged; only the
target has changed.

## Core concepts

**A blockchain is a hash-chained, append-only log with an expensive
consensus rule.** Strip away the hype and that's the whole thing. Each
block contains data plus the *hash of the previous block*. Change
anything in block N, and block N's hash changes, which invalidates
block N+1's stored reference to it, and so on for every block after —
tampering with history requires redoing the "expensive" part (mining/
proof-of-work, or in modern systems, proof-of-stake) for every
subsequent block, which is what makes the history practically
immutable once enough blocks have been added on top. You'll build
this exact mechanism in 24.1 before touching anything Ethereum-specific.

**Ethereum adds a virtual machine on top of that log.** A "smart
contract" is just a program — bytecode, compiled from Solidity — whose
storage lives on-chain and whose functions execute inside every node's
copy of the EVM (Ethereum Virtual Machine) when someone sends a
transaction that calls them. There's no server; the contract's code
*is* the server, replicated across every node, and once deployed it
generally can't be changed. This is the core reason smart contract
bugs are so much higher-stakes than a typical web app's: you usually
can't just ship a patch.

**Gas is what stops an infinite loop from crashing every node in the
world.** Every EVM operation costs gas; a transaction specifies a gas
limit and runs out of it (reverting all state changes) if it exceeds
that limit. This isn't incidental — it's the whole reason Ethereum-as-
a-shared-computer is possible at all.

**Reentrancy — the canonical smart contract vulnerability — is a
race condition you already understand from Stage 5/8, wearing a
different costume.** The classic pattern: a contract sends funds to an
address (an external call) *before* updating its own internal
bookkeeping (e.g. zeroing that address's balance). If the recipient is
itself a contract, its code runs *during* that external call — and can
call back into the original function before the balance was ever
zeroed, withdrawing again. And again. This is the same class of bug as
a TOCTOU race (check happens, then time passes before the corresponding
update, and an attacker acts in that gap) — see `SECURITY-CONCEPTS.md`'s
Race Conditions entry. The fix generalizes the same way any TOCTOU fix
does: update state *before* the external call ("checks-effects-
interactions" pattern), not after.

**Flash loans change what "capital required to attack" means.** A
flash loan lets you borrow an arbitrary amount — no collateral — for
the duration of a *single transaction*, as long as you repay it (plus a
fee) before that transaction ends, or the entire transaction reverts as
if it never happened. This means an attacker doesn't need to be rich to
manipulate a price oracle, drain a liquidity pool, or exploit an
economic assumption at massive scale — they need the loan to be
*profitable within one transaction*, which is a completely different
bar. This is the mechanism behind most of the largest real-world DeFi
exploits, and it's what 24.5 (Damn Vulnerable DeFi) is really testing
your understanding of.

**Testnets exist so none of this practice touches real money.** Same
chain mechanics, same EVM, same Solidity — just worthless test ETH from
a faucet instead of real funds. There is no version of this stage's
projects that legitimately needs mainnet. See the Stage 24 README's
scope/safety note before writing a single line of Solidity.

## Required reading

Per `ROADMAP.md`'s Stage 24 resource table: start with [Mastering
Bitcoin](https://github.com/bitcoinbook/bitcoinbook) chapters 1-2 for
the blockchain-fundamentals half (you don't need the rest of the book
for this stage), then move to [Cyfrin
Updraft](https://updraft.cyfrin.io/)'s Solidity course for the
smart-contract half. Don't attempt 24.4 (Ethernaut) before you're
comfortable with basic Solidity syntax and the reentrancy pattern
above — Ethernaut assumes it.

## Check yourself

1. If you tampered with block 5 of a 10-block chain and re-mined *only*
   block 5 (not 6-10), would your chain validator from 24.1 accept it?
   Why or why not?
2. Concretely, what two lines would you swap in a vulnerable
   `withdraw()` function to fix a reentrancy bug using
   checks-effects-interactions — and why does the order matter given
   how the EVM actually executes an external call?
3. Why can't a flash-loan attacker be stopped by simply requiring "a
   minimum balance held for N blocks before acting" — what about a
   flash loan's structure makes that specific defense meaningless?
4. In the ERC-20 standard, what's the actual security-relevant
   difference between `transfer` and `transferFrom` + `approve` — why
   does the standard need both instead of just one?
5. Your 24.1 blockchain and a real Ethereum node both reject a chain
   with an invalid `previous_hash` link. What does a real Ethereum node
   check that your toy version from 24.1 doesn't need to (think about
   what makes a *transaction*, as opposed to a block, valid)?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 24.1 — Blockchain From
Scratch** (`projects/24.1-blockchain-from-scratch/SPEC.md`). Start
there before touching Solidity.
