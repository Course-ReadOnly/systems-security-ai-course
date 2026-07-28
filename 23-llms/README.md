> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 23 — LLMs

**Time budget:** 6–8 weeks part-time / 3 weeks full-time

## Objectives

Understand transformers/attention/tokenizers from first principles
(Karpathy's build-GPT is the anchor resource here), then build practical
LLM-powered tools applied to security domains from earlier stages — the
direct rehearsal for Stage 25's deeper AI×security integration.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Build a GPT from scratch | [Karpathy — "Let's build GPT"](https://www.youtube.com/watch?v=kCc8FmEb1nY) |
| 02 | Full NLP/transformers course | [Hugging Face NLP Course](https://huggingface.co/learn/nlp-course) |
| 03 | Visual intuition for attention | [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) |

**Topics:** attention, tokenizers, embeddings, fine-tuning, RAG, agents.

**Worth knowing before building any of these:** every project below
feeds untrusted, attacker-influenceable content (samples, logs, CVE
text) into an LLM prompt — that content can itself be crafted to hijack
the model's behavior (indirect prompt injection). See
`SECURITY-CONCEPTS.md`'s "Prompt Injection" entry before you build the
first one; it changes how you should think about trusting model output.

## Projects

| # | Project | Folder |
|---|---|---|
| 23.1 | Reverse-engineering assistant | `projects/23.1-re-assistant/` |
| 23.2 | Malware report summarizer | `projects/23.2-report-summarizer/` |
| 23.3 | Threat-hunting assistant | `projects/23.3-threat-hunting-assistant/` |
| 23.4 | Vulnerability assistant | `projects/23.4-vulnerability-assistant/` |

All four are "LLM applied to a domain from an earlier stage" projects —
do Karpathy's build-GPT material first so the tools you build in 23.1-
23.4 aren't just API calls to a black box.
