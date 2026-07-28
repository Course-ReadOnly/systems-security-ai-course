> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 10.01 — Encrypted vs. Secure: XOR to AES

## Why this matters

Cryptopals' entire pedagogy is built on one move: hand you a broken
construction, let you break it yourself, and only then hand you the real
thing. That order matters. If you learn "use AES" first, "secure" stays
a label you trust because you were told to. Break XOR-based encryption
with your own hands in Set 1 first, and "secure" becomes something you
can actually reason about — a claim backed by decades of public
cryptanalysis finding no practical attack, not a property you can see by
looking at ciphertext. That instinct — asking *why* a construction
resists attack, not just accepting that it's labeled AES — is exactly
what Stage 13's crypto-adjacent exploitation and Stage 14's detection
work both lean on later.

## Core concepts

**"Encrypted" means "transformed by a reversible, keyed function."**
That's all it means. It says nothing about whether the transform
resists an attacker who can see the ciphertext, or knows some plaintext,
or can even choose plaintext and watch what comes out. XOR is the
cleanest possible demonstration of this gap, because XOR-with-a-key
*is* technically encryption — reversible, keyed — and is also trivially
broken, which is exactly why Cryptopals Set 1 opens with it.

**Single-byte XOR falls to frequency analysis.** English text has a
known, stable letter-frequency distribution. XOR every possible
single-byte key (all 256) against the ciphertext, score each result
against that distribution, and the highest-scoring result is
overwhelmingly likely to be the real key — no plaintext knowledge
required, just statistics about the *language*, not the message.

**Repeating-key XOR (Vigenère wearing modern clothes) falls the same
way, one level removed.** First recover the key *length* — the
Hamming distance (bit differences) between successive key-length-sized
chunks of ciphertext is minimized at the true key length, because XORing
two chunks encrypted under the identical repeating key cancels the key
out and leaves you comparing plaintext to plaintext, which is far more
similar than random noise. Once you know the length, the ciphertext
splits into N interleaved single-byte-XOR streams, each breakable
exactly as above.

**Reusing a key is the fatal sin, and it generalizes past XOR.** XOR two
ciphertexts encrypted under the *same* key and the key cancels out
entirely: `C1 ⊕ C2 = P1 ⊕ P2`. You now have the XOR of two plaintexts
with zero knowledge of the key — and crib-dragging (guessing a likely
word in one plaintext and sliding it across) recovers both messages.
This is precisely why a *one-time pad* is only secure if the key is used
exactly once; "one-time" isn't a name, it's a load-bearing
requirement. Keep this failure mode in mind — it resurfaces below in a
place that looks nothing like XOR on the surface.

**AES resists this class of attack by design, not by luck.** Where XOR
is one linear operation, AES is many rounds of two things working
together: confusion (a nonlinear S-box substitution, so output bits
don't relate simply to input bits) and diffusion (operations like
ShiftRows/MixColumns that spread each input bit's influence across the
whole block). The "secure" claim rests on this construction having
survived decades of the best public cryptanalysis — differential and
linear attacks specifically — finding nothing better than brute force.
That track record, not "it looks random," is what "secure" means in
practice.

**A block cipher only encrypts one fixed-size block — the mode of
operation is what handles real, arbitrary-length data, and the mode
choice is itself a security decision.** ECB (encrypt each block
independently) leaks structure: identical plaintext blocks produce
identical ciphertext blocks, so patterns in the input survive into the
output (the classic demonstration: encrypt an image in ECB and its
outline is still visible in the ciphertext). CBC and CTR both fix this
by chaining each block's encryption to something that changes block to
block. CTR is the sharper case to understand: it turns AES into a
*stream* cipher by encrypting a counter and XORing the result with your
plaintext — which means CTR mode's security depends entirely on that
counter/nonce never repeating under the same key. Reuse a nonce in CTR
and you've reconstructed the exact two-time-pad vulnerability above,
just with an AES-generated keystream standing in for the XOR key. "AES"
alone is not a complete security claim — mode and nonce handling are
part of it.

**Round-tripping is not correctness; a test vector is.** Encrypt-then-
decrypt returning your original input only proves your encrypt and
decrypt functions are mutual inverses of *something* — a bug present in
both directions cancels itself out and passes that test every time.
Matching a NIST Known-Answer Test vector proves your implementation
computes the *specified* algorithm, not merely a self-consistent one.

## Required reading

Per Stage 10's resource table: [Cryptopals](https://cryptopals.com/)
Set 1, challenges 1–6 (fixed XOR through breaking repeating-key XOR) —
do these yourself before touching 10.2's AES implementation.
[Crypto101](https://www.crypto101.io/)'s block cipher chapter is the
right companion for the confusion/diffusion and modes-of-operation
material above, in more depth than this lecture gives it.

## Check yourself

1. Given only a ciphertext you're told was single-byte XORed, how would
   you programmatically recover the key without knowing the plaintext —
   what exactly are you scoring?
2. Two messages were encrypted under the same repeating-key XOR key.
   What single operation on the two ciphertexts gets you information
   about both plaintexts with *zero* knowledge of the key, and why does
   that operation cancel the key out?
3. Why is ECB mode's "identical plaintext blocks → identical ciphertext
   blocks" a real vulnerability rather than a cosmetic curiosity — what
   could an attacker learn from an image encrypted in ECB?
4. What specific implementation mistake in CTR mode recreates the exact
   two-time-pad vulnerability from question 2 — and why does that mean
   "we use AES" is not, by itself, a meaningful security claim?
5. Why doesn't "my code encrypts then decrypts back to the original
   string" prove your AES implementation is correct, and what does
   matching a NIST test vector prove that a round-trip test can't?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 10.2 — Small Encryption
Library** (`projects/10.2-encryption-library/SPEC.md`). Set 1 of
Cryptopals first, then start there.
