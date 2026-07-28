> **Generated ahead of schedule** (2026-07-28, per learner request — see
> `STATUS.md`'s 2026-07-28 note). Revisit when actually reached.

# Stage 24 — Blockchain & Smart Contracts

**Time budget:** 6–8 weeks part-time / 3 weeks full-time

## Objectives

Placed here rather than near Stage 10 (classical Cryptography) because
it leans on tooling you don't have until now: Python/Go (17–18) to
build a chain from first principles, and the auditing/exploit mindset
from Stage 13 (Offensive Security) for the smart-contract-security
half. Two halves to this stage, deliberately in this order:

1. **Understand the mechanism** — build a minimal blockchain yourself
   (hashing, chaining, proof-of-work, validation) before touching
   Solidity, so "blockchain" stops being a buzzword and becomes code
   you wrote and can reason about.
2. **Build and break real contracts** — write actual Solidity, then
   attack intentionally-vulnerable contracts on designated practice
   platforms. This half is the web3 analogue of Stages 11–13: same
   reverse-engineering/exploitation mindset, applied to a domain where
   bugs are worth real money and get exploited within minutes of a
   live deployment.

## Topics & resources

All resources below are free and are what the field itself treats as
canonical/credible (official docs, audited-org-run wargames — not
survey-course filler). Verified live as of 2026-07-28; re-check for
staleness whenever this stage is actually reached, per this course's
usual generated-ahead caveat.

| # | Topic | Free Resource |
|---|---|---|
| 01 | Blockchain fundamentals (hashing, consensus, UTXO) | [Mastering Bitcoin — Andreas Antonopoulos (free, open-source book)](https://github.com/bitcoinbook/bitcoinbook) |
| 02 | Solidity + smart contract development, full free curriculum | [Cyfrin Updraft (free, industry-run — Solidity/web3 courses)](https://updraft.cyfrin.io/) |
| 03 | Gamified Solidity intro | [CryptoZombies (free, interactive)](https://cryptozombies.io/) |
| 04 | Official language reference | [Solidity official docs](https://docs.soliditylang.org/) |
| 05 | Official protocol/developer docs | [ethereum.org developer docs (free, official)](https://ethereum.org/en/developers/docs/) |
| 06 | Smart contract security wargame | [Ethernaut (free, built by OpenZeppelin)](https://ethernaut.openzeppelin.com/) |
| 07 | DeFi-specific exploitation challenges (advanced) | [Damn Vulnerable DeFi (free)](https://www.damnvulnerabledefi.xyz/) |

**Topics:** blocks, hashing, Merkle trees, consensus (PoW/PoS), the
Ethereum account/gas model, Solidity, the ERC-20/ERC-721 token
standards, common smart contract vulnerability classes (reentrancy,
integer overflow/underflow, access control, oracle manipulation,
flash-loan attacks), auditing methodology.

## Scope/safety note (same standard as Stages 11–14)

- **Testnets only, ever.** Every contract you write or deploy in this
  stage goes on a public testnet (Sepolia or similar) using test ETH
  from a faucet — never mainnet, never real funds. There is no
  legitimate reason for a learning project in this stage to touch real
  money.
- **Exploitation work stays on designated practice platforms.**
  Ethernaut and Damn Vulnerable DeFi are built specifically for this —
  treat them the same way this course treats ROP Emporium/PortSwigger
  in Stage 13: sanctioned targets only, same discipline as any other
  offensive-security lab, never real/live contracts you don't own or
  have explicit authorization to test.
- **Private keys/seed phrases:** use throwaway test wallets only. Never
  put a real wallet's seed phrase in code, an environment variable
  committed to git, or anywhere in this repo.

## Projects

| # | Project | Folder |
|---|---|---|
| 24.1 | Blockchain from scratch | `projects/24.1-blockchain-from-scratch/` |
| 24.2 | First smart contract + ERC-20 token | `projects/24.2-erc20-token/` |
| 24.3 | Simple DApp | `projects/24.3-simple-dapp/` |
| 24.4 | Ethernaut write-up | `projects/24.4-ethernaut-writeup/` |
| 24.5 | Stretch: Damn Vulnerable DeFi | `projects/24.5-damn-vulnerable-defi/` |

Do 24.1 before 24.2 — understanding what a chain actually is makes the
Solidity/gas-model material in 24.2 onward land as "how this specific
chain (Ethereum) does the thing you already built a toy version of,"
not a cold start.
