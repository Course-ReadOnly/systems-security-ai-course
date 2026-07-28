> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 10.1 — Password Manager

## Goal

Apply real crypto correctly, end to end: a master password unlocks a
store of secrets, encrypted at rest. The point of this project is
almost entirely about **not making the classic mistakes** (rolling your
own cipher, reusing a nonce, storing a password instead of a hash of it)
— using a real, established library correctly is the actual skill.

## Requirements

1. Uses an established crypto library (e.g. OpenSSL, libsodium — **do
   not implement your own AES/cipher**; that's what Cryptopals is for,
   this project is about correct *use*).
2. Master password → key derivation via a real KDF (PBKDF2, scrypt, or
   Argon2 — **not** a raw hash of the password) with a proper random
   salt stored alongside the encrypted data.
3. Secrets encrypted at rest using authenticated encryption (e.g.
   AES-GCM) — a fresh, random nonce/IV per encryption, **never reused**.
4. Add/retrieve/list secrets via a CLI, unlocked by the master password
   each session.
5. Wrong master password is rejected cleanly (authentication tag
   verification failure, not silent garbage decryption).

## Acceptance criteria

- [ ] Builds/runs cleanly
- [ ] Paste a session: unlock with master password, add a secret,
      retrieve it correctly
- [ ] Wrong-password case pasted, showing clean rejection (not garbled
      output)
- [ ] **Explicitly confirm and paste evidence** that nonces/IVs are
      never reused across encryptions (e.g. log/inspect the nonces used
      across several add operations, show they're all different)
- [ ] `git log` shows iteration
- [ ] README stating exactly which library, KDF, and cipher mode were
      used, and why

## Security relevance

This entire project *is* the security relevance — see
`SECURITY-CONCEPTS.md`'s "Cryptographic Misuse" entry for the general
pattern this project is built to avoid. Nonce reuse under AES-GCM
specifically doesn't just weaken security, it can fully break
confidentiality and authenticity for the affected messages (the
keystream reuse reduces to the same two-time-pad math XOR-based
schemes fail on, plus a forgeable authentication tag) — which is why
"never reused" is an acceptance-criteria requirement with pasted
evidence, not a suggestion.

## When done

Point me at the source + `git log`. I will check nonce/IV reuse and KDF
choice hardest — those are the two mistakes that turn "using real
crypto" into "using real crypto insecurely," which is worse than no
crypto in some ways because it looks safe.
