> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached.

# Project 24.2 — First Smart Contract + ERC-20 Token

## Goal

Your first real Solidity contract, deployed to a real (test) network —
the standard "hello world" of smart contract development, done
properly: understand the ERC-20 interface you're implementing rather
than copy-pasting OpenZeppelin's contract and calling it done.

## Requirements

1. Work through enough of Cyfrin Updraft or CryptoZombies to be
   comfortable with Solidity syntax, state variables, functions,
   modifiers, and events before starting this project.
2. Implement an ERC-20 token contract yourself — you may reference
   OpenZeppelin's implementation to check your work, but write your
   own `transfer`, `approve`, `transferFrom`, and balance-tracking
   logic rather than inheriting it wholesale. The point is
   understanding the standard, not just deploying it.
3. Correctly implement the allowance pattern (`approve` +
   `transferFrom`) — this is the part of ERC-20 most learners get
   subtly wrong (forgetting to check/decrement allowance, or allowing
   underflow).
4. Emit the standard `Transfer` and `Approval` events on the correct
   operations.
5. Deploy to a public testnet (Sepolia or similar) using a throwaway
   test wallet and faucet ETH — **never mainnet, never a real wallet**.
6. Write basic tests (Foundry or Hardhat) covering: a normal transfer,
   a transfer that should fail (insufficient balance), an approve +
   transferFrom flow, and a transferFrom that should fail (insufficient
   allowance).

## Acceptance criteria

- [ ] Your own ERC-20 implementation (not a bare OpenZeppelin import),
      with `transfer`/`approve`/`transferFrom`/balance tracking
- [ ] Tests covering both the happy path and at least 2 failure cases
      (insufficient balance, insufficient allowance), all passing
- [ ] Deployed to a public testnet — contract address + testnet name in
      the README (no mainnet deployment)
- [ ] `Transfer`/`Approval` events emitted correctly
- [ ] `git log` shows real iteration
- [ ] No real wallet seed phrase or private key committed anywhere in
      the repo — confirm your `.gitignore` actually excludes it

## Security relevance

The allowance pattern this spec calls out as "most learners get subtly
wrong" (Requirement 3) is a real, historically-exploited ERC-20 bug
class — an unchecked or incorrectly-decremented allowance in
`transferFrom` has caused real token-draining incidents in production
contracts. This project's committed-secret warning is the same
discipline as any other credential-handling code (see
`SECURITY-CONCEPTS.md`), just with an unusually unforgiving failure
mode: a leaked key on a public chain can't be rotated after the fact
the way a leaked API key can.

## When done

Point me at the source, `git log`, test output, and the testnet
contract address. I'll check the allowance logic specifically —
`transferFrom` without a correct allowance check/decrement is the most
common real-world ERC-20 bug class.
