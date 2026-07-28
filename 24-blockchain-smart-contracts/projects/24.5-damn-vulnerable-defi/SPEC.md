> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached. Stretch project — do this after 24.4, not
> instead of it; Damn Vulnerable DeFi assumes the Ethernaut-level
> fundamentals are already solid.

# Project 24.5 — Stretch: Damn Vulnerable DeFi

## Goal

Ethernaut teaches individual vulnerability classes in isolation. Damn
Vulnerable DeFi is the next step up: realistic, composed DeFi
protocols (lending pools, flash loans, staking, DEXes) with
vulnerabilities that usually require chaining multiple contracts and
economic mechanisms together, not just one function's bug — much
closer to how real, high-value smart contract exploits actually work.
Same designated-legal-practice-platform framing as 24.4.

## Requirements

1. Complete at least 4 challenges from Damn Vulnerable DeFi.
2. For each, write up: which contracts/mechanisms are involved, the
   economic or logical assumption the protocol makes that turns out to
   be false, the exploit path (including any flash-loan or multi-step
   sequencing involved), and how you'd fix the protocol design (not
   just patch the specific line).
3. At least 2 write-ups must explicitly address the **economic**
   dimension of the exploit — e.g. what capital (if any) the attacker
   needs up front vs. what a flash loan lets them borrow-and-repay
   atomically within one transaction, and why that changes what
   "expensive to attack" even means for a naively-designed protocol.
4. Include the actual solving script/contract for every challenge you
   claim complete, not just a narrative description.

## Acceptance criteria

- [ ] At least 4 Damn Vulnerable DeFi challenges completed, each with a
      working solving script/contract in the repo
- [ ] Written report per challenge: mechanism involved, false
      assumption, exploit path, proposed fix
- [ ] At least 2 write-ups explicitly reason about the economic
      dimension (capital requirements, flash-loan atomicity)
- [ ] `git log` shows real iteration
- [ ] Cross-reference to `SECURITY-CONCEPTS.md` where a matching entry
      exists, same as 24.4

## Security relevance

Already this project's entire subject, at the most advanced level this
course reaches on the topic: these challenges are modeled on real,
high-value production exploits, and the economic-dimension requirement
(Requirement 3) is what separates this from 24.4's more contained,
single-contract bugs — flash loans mean an attacker's required capital
and a protocol's actual economic security assumptions are two
different things, which is precisely the gap real DeFi exploits have
repeatedly found.

## When done

Point me at the write-ups, solving scripts, and `git log`. I'll ask
you to explain one challenge's exploit as if walking a protocol team
through a real disclosure — what would you tell them broke, and what
would you actually recommend they change (not just "add a
reentrancy guard").
