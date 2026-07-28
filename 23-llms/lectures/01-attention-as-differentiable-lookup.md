> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 23.01 — Attention as a Learned, Differentiable Lookup

## Why this matters

Every project in this stage — the RE assistant, the report summarizer,
the threat-hunting and vulnerability assistants — is "call an API and
engineer a prompt" on the surface. Underneath, every one of them is
handing text to a stack of attention layers and trusting the model to
figure out, token by token, what in that text actually matters for the
task. If attention stays a black box, prompt engineering degenerates
into superstition — you'll tweak wording and hope. Understand the
mechanism and prompt design becomes something you can reason about: you
know *why* burying the important instruction in a wall of irrelevant
context makes the model worse, and — sharply relevant given this stage's
prompt-injection warning — you know exactly *why* an LLM can't cleanly
separate "your instructions" from "the untrusted text you handed it."

## Core concepts

**Attention answers one question per token: which other tokens matter to
me, and how much?** Every token gets three learned vectors derived from
its embedding: a query ("what am I looking for"), a key ("what do I
offer"), and a value ("what I actually contribute if picked"). A token's
query is dot-producted against *every* token's key (including its own)
to get a raw relevance score per pair, those scores are passed through
softmax to become weights that sum to 1, and the token's new
representation is the weighted sum of every token's value vector using
those weights. That's the whole mechanism. It's a lookup — "search
across all these keys for what's relevant to my query" — except every
piece of it (the Q/K/V projections, the whole pipeline) is
differentiable, so gradient descent tunes what the model considers
"relevant" directly from data, instead of anyone hand-coding a lookup
rule.

**This is why it's called *self*-attention: the tokens attending and the
tokens being attended to are the same sequence.** Every token
simultaneously plays lookup-er and lookup-ed. The result is that a
token's representation after one attention layer already incorporates
context from the entire sequence — a pronoun's representation can be
pulled toward whatever noun it refers to, purely because that
relationship raised the attention score between them, with no explicit
"resolve coreference" step anyone wrote.

**Contrast this with what came before: RNNs process sequentially and
compress everything into one fixed-size hidden state as they go.** By
the time an RNN reaches token 500, information from token 1 has been
overwritten and diluted through 499 update steps — a real bottleneck,
and the concrete cause of RNNs struggling with long-range dependencies.
Attention has no such bottleneck: token 500's query can attend directly
to token 1's key in a single step, full strength, regardless of
distance. That's the architectural reason transformers displaced RNNs
for language, not just "attention is trendier."

**Multi-head attention runs several of these lookups in parallel with
different learned Q/K/V projections, then concatenates the results.**
One head might learn to track syntactic dependencies, another
coreference, another something with no clean human name — the point is
the model isn't limited to one notion of "relevant," it learns several
simultaneously and combines them.

**A causal mask is what makes a transformer decoder autoregressive.**
For generation (what GPT does), token N's query is *not allowed* to
attend to tokens after it — the attention scores for future positions
are forced to `-infinity` before the softmax, zeroing their weight.
Without this, the model could "cheat" during training by looking ahead
at the very token it's supposed to predict. This masking is the entire
difference between an encoder (sees everything, good for
understanding/classification) and a decoder (sees only the past, good
for generation) — same attention mechanism, different mask.

**Tokenization and embeddings are the layer beneath all of this, and
worth naming precisely once:** text is split into subword tokens (not
words, not characters — a compromise that keeps vocabulary size
manageable while still handling rare/unseen words), each token maps to a
learned vector via an embedding table, and that vector is what queries,
keys, and values are computed from. "Meaning," to the model, is nothing
but position in that high-dimensional vector space.

**Why this matters directly for prompt injection, which this stage's
README already flags:** attention has no architectural notion of "this
span of tokens is a trusted instruction, this span is untrusted data I
retrieved." A system prompt, your actual prompt, and a pasted
decompiled function or log file all become tokens in the same sequence,
and every token's query can attend to every other token equally,
governed only by learned relevance — not by any hard boundary. If an
attacker's text contains something that reads, to the trained
attention patterns, like an instruction, the model has no built-in way
to know it didn't come from you. That's not a bug that gets patched;
it's a direct consequence of the mechanism above, which is exactly why
`SECURITY-CONCEPTS.md`'s Prompt Injection entry says to design around it
rather than assume it away.

## Required reading

Per `ROADMAP.md`'s Stage 23 resource table — watch Karpathy's ["Let's
build GPT"](https://www.youtube.com/watch?v=kCc8FmEb1nY) for the
mechanism implemented in actual code (he builds the Q/K/V, scaled
dot-product, and causal mask from scratch). For the visual/intuitive
pass before or alongside the video, use [The Illustrated
Transformer](https://jalammar.github.io/illustrated-transformer/) —
its diagrams of the Q/K/V computation are the clearest available for
building intuition before you read the code.

## Check yourself

1. In the Q/K/V setup, which vector belongs to the token doing the
   "asking" and which belongs to the token being "offered" — and what
   actually gets summed to produce the output?
2. Why is softmax used on the raw attention scores instead of, say,
   just normalizing them to sum to 1 by dividing by their total?
3. Concretely, what breaks (in terms of what the model could "see")
   during training if you forgot to apply the causal mask in a GPT-style
   decoder?
4. An RNN's hidden state at token 500 has been through 499 update steps
   before it can influence the output. What's the equivalent number of
   "steps" a self-attention layer needs for token 500 to be influenced
   by token 1's information — and why does that number matter for long
   documents?
5. Given that attention treats every token in the sequence uniformly
   (no built-in trusted/untrusted distinction), what's one concrete
   prompt-design choice you could make in 23.1's RE assistant to reduce
   (not eliminate) the risk of a decompiled function's contents being
   interpreted as instructions rather than data?

Answers withheld until asked.

## Project

This stage's projects are all "LLM applied to an earlier-stage domain."
Read `README.md`'s project list before picking one — the natural first
stop is **Project 23.1 — Reverse-Engineering Assistant**
(`projects/23.1-re-assistant/SPEC.md`), which uses your own Stage 11
crackme work as ground truth.
