> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 24 — Advanced Engineering

**Time budget:** 10–12 weeks part-time / 5 weeks full-time

## Objectives

The deepest systems stage: compilers, hypervisors, kernel modules, eBPF,
GPU programming, and Rust. Everything here assumes Stages 1-9 are
genuinely solid — this is where gaps from earlier stages surface hardest,
not a good place to be catching up on C fundamentals.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Compilers | [LLVM official docs + tutorial](https://llvm.org/docs/tutorial/) |
| 02 | OS/kernel internals reference | [OSDev Wiki](https://wiki.osdev.org/) |
| 03 | Kernel modules & eBPF | [eBPF.io](https://ebpf.io/) |
| 04 | Kernel deep-dive | [MIT 6.S081](https://pdos.csail.mit.edu/6.828/) |
| 05 | GPU programming | [NVIDIA CUDA docs + samples](https://docs.nvidia.com/cuda/) |
| 06 | Rust | [The Rust Book](https://doc.rust-lang.org/book/) |

**Topics:** LLVM, compilers, hypervisors, UEFI, eBPF, Linux kernel,
Windows internals (deep dive), GPU programming, CUDA, Rust.

**Worth knowing while you're here:** the kernel/user and guest/host
boundaries this stage works in (24.3's hypervisor, 24.4's kernel module)
are exactly where real mitigations for Stage 4's side-channel concerns
live — e.g. KPTI (kernel page-table isolation), added kernel-wide after
Meltdown specifically to stop user-space from using cache timing to
infer kernel memory contents. See `SECURITY-CONCEPTS.md`.

## Projects

| # | Project | Folder |
|---|---|---|
| 24.1 | A small compiler | `projects/24.1-small-compiler/` |
| 24.2 | A small VM | `projects/24.2-small-vm/` |
| 24.3 | Hypervisor experiments | `projects/24.3-hypervisor-experiments/` |
| 24.4 | A kernel module | `projects/24.4-kernel-module/` |
| 24.5 | An eBPF monitor | `projects/24.5-ebpf-monitor/` |
