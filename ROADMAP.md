# Systems → Security → AI Roadmap (100% Free / Open Resources)

A self-study path from Linux basics through C, systems programming, security,
and AI/LLMs. Every resource listed is free (open courseware, open-source
books, free YouTube series, or free-tier interactive platforms). Time
estimates assume **~10–15 hrs/week** (part-time, working/studying alongside).
A **full-time (~35–40 hrs/week)** estimate is given alongside where useful.
Total path: roughly **3–3.5 years part-time**, or **~13–17 months
full-time**, if done end-to-end — but you can stop anywhere and already have
a real skillset.

---

## How to use this

- **Don't skip projects.** Reading without building is the #1 way this kind
  of roadmap stalls out.
- **Stages 17–18 (Python/Go) can be pulled earlier** if you want a scripting
  tool while still in the C-heavy stages — many people learn basic Python in
  parallel with Stage 1.
- Time ranges are cumulative *per stage*, not including review/buffer. Add
  ~15% buffer overall.

---

## Stage 0 — Foundations

**Time: 2–3 weeks part-time / 1 week full-time**

| Topic | Free Resource |
|---|---|
| Linux terminal & CLI | [Linux Journey](https://linuxjourney.com/) — free, interactive |
| Shell fundamentals | [MIT Missing Semester](https://missing.csail.mit.edu/) — free, full video+notes |
| Bash scripting | [Bash Guide (Greg's Wiki)](https://mywiki.wooledge.org/BashGuide) |
| Git | [Pro Git book](https://git-scm.com/book/en/v2) — free, official |
| Editors (Vim/Neovim/VS Code) | [Vim Adventures free tier](https://vim-adventures.com/) + [Neovim docs](https://neovim.io/doc/) |
| GCC/Clang, Make | [GNU Make Manual](https://www.gnu.org/software/make/manual/make.html) |
| CMake | [CMake official tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html) |
| GDB | [Beej's GDB Quick Start](https://beej.us/guide/bggdb/) |
| Valgrind | [Valgrind Quick Start](https://valgrind.org/docs/manual/quick-start.html) |
| Docker | [Docker Official Docs — Get Started](https://docs.docker.com/get-started/) |
| SSH | [SSH Essentials (DigitalOcean, free)](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys) |
| Practice environment | [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — free wargame for terminal fluency |

**Projects:** dotfiles repo, Linux workstation setup script, small bash
automation scripts, a file organizer script, a backup utility script.

---

## Stage 1 — C Programming (Core)

**Time: 6–9 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Full language (variables → pointers → memory) | [Beej's Guide to C](https://beej.us/guide/bgc/) — free, excellent |
| Deeper / modern semantics | [Modern C by Jens Gustedt](https://hal.inria.fr/hal-02383654/document) — free PDF |
| Structured course w/ problem sets | [CS50 (Harvard, free via edX/YouTube)](https://cs50.harvard.edu/x/) |
| Interactive drills | [learn-c.org](https://www.learn-c.org/) |
| Reference | [C Reference (cppreference.com)](https://en.cppreference.com/w/c) |

**Projects (easy → hard):**
- Easy: calculator, todo app, file copier, text statistics tool
- Medium: hex editor, config parser, INI parser, JSON parser
- Hard: text editor, terminal UI, CSV library

---

## Stage 2 — Data Structures

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Core theory & algorithms | [MIT 6.006 (OCW, full free course)](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) |
| Visualization | [VisuAlgo](https://visualgo.net/en) — free interactive visualizations |
| Written references | [CP-Algorithms](https://cp-algorithms.com/) — free, thorough |
| Practice problems | [freeCodeCamp DS&A curriculum](https://www.freecodecamp.org/) |

**Learn & implement yourself (in C):** vector, linked list, stack, queue,
hash map, binary tree, AVL tree, red-black tree, heap, trie, graph.

**Project:** an STL-like generic library in C.

---

## Stage 3 — Algorithms

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Core course (same as Stage 2) | [MIT 6.006](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) |
| Structured practice roadmap | [NeetCode Roadmap](https://neetcode.io/roadmap) — free tier covers most patterns |
| Reference/theory | [CP-Algorithms](https://cp-algorithms.com/) |
| Practice | [LeetCode free tier](https://leetcode.com/) |

**Topics:** sorting, searching, BFS/DFS, dynamic programming, Dijkstra, A*,
topological sort.

**Projects:** maze solver, route planner.

---

## Stage 4 — Computer Architecture

**Time: 4–6 weeks part-time / 2 weeks full-time**

| Topic | Free Resource |
|---|---|
| Full course | [Berkeley CS61C (free, all materials online)](https://cs61c.org/) |
| Hardware-up, hands-on approach | [Ben Eater — Build an 8-bit computer (YouTube)](https://www.youtube.com/c/BenEater) |
| Build a CPU from NAND gates | [NAND2Tetris (free course + free book)](https://www.nand2tetris.org/) |

**Topics:** binary, logic gates, CPU, registers, ALU, pipelines, cache,
memory, interrupts, MMU.

**Projects:** CPU simulator, CHIP-8 emulator, simple assembler.

---

## Stage 5 — Systems Programming

**Time: 8–10 weeks part-time / 4 weeks full-time**

| Topic | Free Resource |
|---|---|
| Canonical course (CS:APP) | [CMU 15-213 (free lectures + free labs)](https://www.cs.cmu.edu/~213/) |
| Alternative full course | [Stanford CS107 (materials free online)](https://web.stanford.edu/class/cs107/) |
| Reference book (free chapters/notes available) | [CS:APP course site materials](https://csapp.cs.cmu.edu/) |

**Topics:** processes, threads, fork, pipes, signals, mmap, epoll, memory
management.

**Projects:** a shell, a malloc implementation, a thread pool, an HTTP
server, a static web server.

---

## Stage 6 — Windows Systems Programming

**Time: 4–6 weeks part-time / 2 weeks full-time**

Everything through Stage 5 is Linux/POSIX. This stage is the Windows
equivalent — the same process/thread/IPC concepts, but the actual API you'll
need to read when reversing Windows binaries or analyzing Windows malware
later in the course (Stages 12, 24).

| Topic | Free Resource |
|---|---|
| Win32 API fundamentals (handles, windows, messages) | [theForger's Win32 API Tutorial](http://winprog.org/tutorial/) — free, classic |
| Official API reference | [Win32 API reference (Microsoft Learn)](https://learn.microsoft.com/en-us/windows/win32/api/) |
| Full Win32 systems tutorial (data types, handles, processes) | [tenouk Win32 Programming Tutorial](https://www.tenouk.com/ModuleC.html) — free |
| Windows kernel internals (objects, handles, syscalls, IRQL) | [OpenSecurityTraining2 — Windows Kernel Internals](https://p.ost2.fyi/courses) — free |
| Kernel debugging | OpenSecurityTraining2 WinDbg mini-course — free |

**Topics:** the `HANDLE` model, `CreateProcess`/`CreateThread`,
synchronization primitives (mutexes, events, critical sections), DLLs and
the import/export table, the Windows Registry, named pipes, an intro to
kernel-mode internals (objects, syscalls, IRQL) as prep for RE/malware work.

**Projects:** a native Win32 process launcher (spawn + wait + capture exit
code — the Windows-native version of Stage 5's `fork`/`exec`), a DLL you
build and load yourself via `LoadLibrary` (understand imports/exports before
you're reading them in a disassembler), a process/module enumerator using
`CreateToolhelp32Snapshot` (read-only system introspection — the same shape
of tooling you'll build again, more seriously, in Stage 12).

---

## Stage 7 — Assembly

**Time: 3–4 weeks part-time / 1.5 weeks full-time**

| Topic | Free Resource |
|---|---|
| x86/x64/ARM64, full training | [OpenSecurityTraining2 — free courses](https://opensecuritytraining.info/) |
| x86-64 assembly reference | [NASM Tutorial (free)](https://cs.lmu.edu/~ray/notes/nasmtutorial/) |
| ARM64 | [ARM Developer — free documentation](https://developer.arm.com/documentation) |

**Topics:** calling conventions, stack, registers, syscalls.

**Projects:** assembly calculator, ELF loader.

---

## Stage 8 — Operating Systems

**Time: 8–10 weeks part-time / 4 weeks full-time**

| Topic | Free Resource |
|---|---|
| Full free textbook | [OSTEP (Operating Systems: Three Easy Pieces)](https://pages.cs.wisc.edu/~remzi/OSTEP/) — completely free |
| Build a real OS with an MIT course | [MIT 6.828/6.S081 + xv6](https://pdos.csail.mit.edu/6.828/) |

**Topics:** scheduling, virtual memory, filesystems, drivers, paging,
context switching.

**Projects:** modify xv6, write a new scheduler, add system calls.

---

## Stage 9 — Networking

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Sockets programming | [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/) — free |
| Full TCP/IP course | [Stanford CS144 (free, self-paced)](https://cs144.github.io/) |
| Deep networking internals | [High Performance Browser Networking (free online book)](https://hpbn.co/) |

**Topics:** Ethernet, IP, TCP, UDP, HTTP, DNS, TLS.

**Projects:** chat server, HTTP proxy, port scanner, packet sniffer.

---

## Stage 10 — Cryptography

**Time: 4–6 weeks part-time / 2 weeks full-time**

| Topic | Free Resource |
|---|---|
| Hands-on crypto challenges | [Cryptopals](https://cryptopals.com/) — free, the gold standard |
| Free crypto book | [Crypto101](https://www.crypto101.io/) |
| University course | [Dan Boneh's Stanford Crypto I (Coursera, free audit)](https://www.coursera.org/learn/crypto) |

**Topics:** XOR, AES, RSA, ECC, Diffie-Hellman, TLS.

**Projects:** password manager, small encryption library.

---

## Stage 11 — Reverse Engineering

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Structured RE training | [OpenSecurityTraining2](https://opensecuritytraining.info/) |
| Beginner-friendly RE course | [MalwareTech / Malware Unicorn RE101 & RE102 (free)](https://malwareunicorn.org/#/workshops) |
| Tools | [Ghidra (free, NSA open-source)](https://ghidra-sre.org/) · [Radare2 (free/open-source)](https://rada.re/n/) |
| Practice binaries | [crackmes.one](https://crackmes.one/) — free |

**Projects:** solve crackmes, write an ELF parser, write a PE parser, write a
binary patcher.

---

## Stage 12 — Malware Analysis

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Sandboxed analysis (free tier) | [ANY.RUN free tier](https://any.run/) |
| Free sample repository | [theZoo (open-source malware repo, for lab use)](https://github.com/ytisf/theZoo) |
| YARA | [YARA official docs (free, open-source)](https://yara.readthedocs.io/) |
| Community write-ups | [MalwareTech blog (free)](https://www.malwaretech.com/) |

**Topics:** packers, obfuscation, Windows internals (builds on Stage 6),
Linux internals.

**Projects:** IOC extractor, write malware analysis reports on public
samples, build a YARA rule set.

---

## Stage 13 — Offensive Security

**Time: 8–10 weeks part-time / 4 weeks full-time**

| Topic | Free Resource |
|---|---|
| Web security, hands-on labs | [PortSwigger Web Security Academy](https://portswigger.net/web-security) — completely free |
| Binary exploitation (ROP) | [ROP Emporium](https://ropemporium.com/) — free challenges |
| Guided hacking labs, free rooms | [TryHackMe free tier](https://tryhackme.com/) |
| Free CTF/pwn practice with real infra | [pwn.college](https://pwn.college/) — free, ASU-run |
| Reference | [OWASP (free, open)](https://owasp.org/) |

**Topics:** web exploitation, Active Directory, buffer overflow, ROP, format
strings.

**Projects:** exploit labs (self-hosted), custom fuzzer.

---

## Stage 14 — Defensive Security

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Framework | [MITRE ATT&CK](https://attack.mitre.org/) — free, industry standard |
| Detection rule format | [Sigma project (open-source)](https://github.com/SigmaHQ/sigma) |
| Signature engine | [YARA docs](https://yara.readthedocs.io/) |
| Network monitoring | [Zeek docs (open-source)](https://docs.zeek.org/) · [Suricata docs (open-source)](https://docs.suricata.io/) |
| SIEM / threat hunting practice | [LetsDefend free tier](https://letsdefend.io/) |

**Projects:** write detection rules, run threat-hunting exercises against
sample logs, build a log parser.

---

## Stage 15 — Embedded Systems

**Time: 4–6 weeks part-time / 2 weeks full-time**

| Topic | Free Resource |
|---|---|
| ARM embedded fundamentals | [ARM Developer docs (free)](https://developer.arm.com/documentation) |
| Practical embedded community resources | [embedded.fm (free podcast/notes)](https://embedded.fm/) |
| STM32 ecosystem (free toolchain) | [STM32CubeIDE (free)](https://www.st.com/en/development-tools/stm32cubeide.html) |

**Topics:** ARM, UART, SPI, I2C, DMA.

**Projects:** bootloader, small firmware project, UART driver.

---

## Stage 16 — Hardware Engineering

**Time: 4–6 weeks part-time / 2 weeks full-time**

| Topic | Free Resource |
|---|---|
| Digital logic, build a CPU from gates | [NAND2Tetris (free)](https://www.nand2tetris.org/) |
| PCB design (free/open-source tool) | [KiCad](https://www.kicad.org/) |
| FPGA basics (free toolchains) | [Yosys/open-source FPGA toolchain docs](https://yosyshq.net/yosys/) |

**Topics:** PCB basics, FPGA basics, digital logic, signals.

**Projects:** breadboard CPU, EEPROM programmer.

---

## Stage 17 — Python

**Time: 3–4 weeks part-time / 1.5 weeks full-time**

| Topic | Free Resource |
|---|---|
| Structured intro course | [CS50P (Harvard, free)](https://cs50.harvard.edu/python/) |
| Practical, project-based book | [Automate the Boring Stuff (free online)](https://automatetheboringstuff.com/) |
| Reference | [Official Python docs](https://docs.python.org/3/) |

**Projects:** malware analysis automation script, IOC parser, Ghidra
scripting, threat-intel collector.

---

## Stage 18 — Go

**Time: 3–4 weeks part-time / 1.5 weeks full-time**

| Topic | Free Resource |
|---|---|
| Official interactive tour | [A Tour of Go](https://go.dev/tour/) |
| Example-driven learning | [Go by Example](https://gobyexample.com/) |

**Projects:** port scanner, small API, reverse proxy, CLI toolkit.

---

## Stage 19 — AI Mathematics

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Linear algebra (intuition) | [3Blue1Brown — Essence of Linear Algebra (free YouTube)](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) |
| Linear algebra (rigor) | [MIT 18.06 (OCW, free)](https://ocw.mit.edu/courses/18-06-linear-algebra-spring-2010/) |
| Calculus intuition | [3Blue1Brown — Essence of Calculus (free)](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) |
| Discrete math / probability for CS | [MIT 6.042 Mathematics for Computer Science (OCW, free)](https://ocw.mit.edu/courses/6-042j-mathematics-for-computer-science-spring-2015/) |
| General math refresher | [Khan Academy (free)](https://www.khanacademy.org/) |

**Topics:** linear algebra, probability, statistics, calculus, optimization.

---

## Stage 20 — Machine Learning

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Classic foundational course | [Andrew Ng's Machine Learning (Coursera, free audit)](https://www.coursera.org/learn/machine-learning) |
| Stanford's advanced version (free notes+videos) | [CS229 (free course materials)](https://cs229.stanford.edu/) |
| Intuitive explainer series | [StatQuest with Josh Starmer (free YouTube)](https://www.youtube.com/c/joshstarmer) |

**Topics:** regression, decision trees, clustering, neural networks.

**Projects:** spam detector, malware classifier.

---

## Stage 21 — Deep Learning

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Practical, top-down course | [fast.ai — Practical Deep Learning (free)](https://course.fast.ai/) |
| Framework | [PyTorch official tutorials (free)](https://pytorch.org/tutorials/) |
| CNN/vision deep-dive | [Stanford CS231n (free notes + free lecture videos)](http://cs231n.stanford.edu/) |

**Topics:** PyTorch, CNNs, RNNs, Transformers.

**Projects:** image classifier, log anomaly detector.

---

## Stage 22 — LLMs

**Time: 6–8 weeks part-time / 3 weeks full-time**

| Topic | Free Resource |
|---|---|
| Build a GPT from scratch, line by line | [Andrej Karpathy — "Let's build GPT" (free YouTube)](https://www.youtube.com/watch?v=kCc8FmEb1nY) |
| Full NLP/transformers course | [Hugging Face NLP Course (free)](https://huggingface.co/learn/nlp-course) |
| Visual intuition for attention | [The Illustrated Transformer (free blog, Jay Alammar)](https://jalammar.github.io/illustrated-transformer/) |

**Topics:** attention, tokenizers, embeddings, fine-tuning, RAG, agents.

**Projects:** reverse-engineering assistant, malware report summarizer,
threat-hunting assistant, vulnerability assistant.

---

## Stage 23 — AI × Cybersecurity

**Time: 6–8 weeks part-time / 3 weeks full-time**

Draws on Stages 6, 11–14, 20–22 together. No single course covers this —
this is an integration stage where you combine Windows/RE/malware/detection
knowledge with the ML/LLM tooling you just built.

**Projects:** AI malware triage tool, AI IOC extractor, AI log analyzer, AI
binary classifier, AI decompiler helper (e.g., a Ghidra script that queries
an LLM), AI-powered fuzzing assistant, AI CTF assistant (for your own lab).

---

## Stage 24 — Advanced Engineering

**Time: 10–12 weeks part-time / 5 weeks full-time**

| Topic | Free Resource |
|---|---|
| Compilers | [LLVM official docs + tutorial (free)](https://llvm.org/docs/tutorial/) |
| OS/kernel internals reference | [OSDev Wiki (free, community-maintained)](https://wiki.osdev.org/) |
| Kernel modules & eBPF | [eBPF.io (free, official learning hub)](https://ebpf.io/) |
| Kernel deep-dive (reuse Stage 8 course) | [MIT 6.S081](https://pdos.csail.mit.edu/6.828/) |
| GPU programming | [NVIDIA CUDA free docs + samples](https://docs.nvidia.com/cuda/) |
| Rust | [The Rust Book (free, official)](https://doc.rust-lang.org/book/) |

**Topics:** LLVM, compilers, hypervisors, UEFI, eBPF, Linux kernel, Windows
internals (deep dive, building on Stage 6), GPU programming, CUDA, Rust.

**Projects:** a small compiler, a small VM, hypervisor experiments, a kernel
module, an eBPF monitor.

---

## Stage 25 — Portfolio (Ongoing)

Target **25–30 substantial projects** by the end. A balanced spread:

**Core Systems (C):** hex editor, text editor, shell, memory allocator, HTTP
server, thread pool, JSON parser, ELF parser, PE parser, packet sniffer.

**Windows:** Win32 process launcher, custom DLL loader, process/module
enumerator.

**Security:** port scanner, HTTP proxy, binary patcher, crackme write-ups,
custom fuzzer, malware triage tool, YARA rule pack, Sigma rule pack.

**Hardware:** CHIP-8 emulator, bootloader, embedded firmware, CPU simulator.

**AI:** malware classifier, AI log analyzer, AI reverse-engineering
assistant, AI threat-hunting assistant.

Put all of it on GitHub with real READMEs — this portfolio *is* the resume
for systems/security/AI roles.

---

## Suggested Cumulative Timeline (part-time, 10–15 hrs/week)

| Phase | Stages | Duration | Running Total |
|---|---|---|---|
| Foundations & C | 0–3 | ~5–6 months | 6 months |
| Systems Depth (incl. Windows) | 4–8 | ~8–9 months | ~15 months |
| Networking, Crypto, Assembly | 7, 9–10 | ~4 months | ~19 months |
| Security Track | 11–14 | ~7 months | ~26 months |
| Embedded/Hardware (optional branch) | 15–16 | ~2 months | ~28 months |
| Scripting Languages | 17–18 | ~2 months | ~30 months |
| AI Foundations | 19–21 | ~5.5 months | ~35.5 months |
| LLMs & AI×Security | 22–23 | ~3.5 months | ~39 months |
| Advanced Engineering | 24 | ~3 months | ~42 months |
| Portfolio polish | 25 | ongoing | — |

**~3–3.5 years part-time**, or roughly **13–17 months if done full-time**.
Stages 15–16 (embedded/hardware) are optional if your goal is purely
software/AI/security — cutting them saves ~2 months.
