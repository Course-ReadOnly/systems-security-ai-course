> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 11 — Reverse Engineering

**Time budget:** 6–8 weeks part-time / 3 weeks full-time

## Objectives

Read compiled binaries you don't have the source for — the direct
payoff of Stage 7 (Assembly) and Stage 6/8's ELF/Windows internals work.
This stage is the hard prerequisite for Stage 12 (Malware Analysis):
you can't triage malware you can't disassemble.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Structured RE training | [OpenSecurityTraining2](https://opensecuritytraining.info/) |
| 02 | Beginner-friendly RE course | [Malware Unicorn RE101 & RE102](https://malwareunicorn.org/#/workshops) |
| 03 | Tools | [Ghidra](https://ghidra-sre.org/) · [Radare2](https://rada.re/n/) |
| 04 | Practice binaries | [crackmes.one](https://crackmes.one/) |

## Projects

| # | Project | Folder |
|---|---|---|
| 11.1 | Solve crackmes (write-ups) | `projects/11.1-crackmes/` |
| 11.2 | ELF parser | `projects/11.2-elf-parser/` |
| 11.3 | PE parser | `projects/11.3-pe-parser/` |
| 11.4 | Binary patcher | `projects/11.4-binary-patcher/` |

`11.2` goes further than Stage 7's ELF loader (section headers, symbol
tables, dynamic linking info — not just program headers).
