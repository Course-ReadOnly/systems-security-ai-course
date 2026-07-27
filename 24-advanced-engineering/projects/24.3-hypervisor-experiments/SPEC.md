> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 24.3 — Hypervisor Experiments

## Goal

Get hands-on with hardware virtualization (Intel VT-x/AMD-V) at a level
below what QEMU/KVM normally show you — write minimal code that enters
guest mode and executes a trivial guest payload. This is explicitly
framed as "experiments," not a production hypervisor — depth of
understanding matters more than feature completeness here.

## Requirements

1. Using Linux's KVM API (`/dev/kvm`) directly (not through libvirt/
   QEMU as a black box), write a minimal host program that: creates a
   VM, allocates guest memory, loads a tiny guest payload (raw machine
   code, no OS), creates a vCPU, and runs it.
2. The guest payload should do something observably verifiable — e.g.
   write a value to a specific memory address or port that the host can
   read after a VM exit.
3. Correctly handle at least one VM exit reason (e.g. an I/O port
   write from the guest, or `HLT`) and read state back from the vCPU.
4. Document, in your own words, what a VM exit actually is and why the
   CPU needs hardware support (VT-x/AMD-V) for this rather than pure
   software emulation.

## Acceptance criteria

- [ ] Host program builds and runs, successfully creates and runs a
      guest via `/dev/kvm`
- [ ] Paste output showing the guest's observable effect (memory write,
      port I/O) correctly read back by the host after a VM exit
- [ ] `git log` shows iteration
- [ ] README explaining VM exits and hardware virtualization support in
      your own words

## When done

Point me at the source + `git log` and the VM-exit evidence. Given this
project touches genuinely low-level, easy-to-get-subtly-wrong territory,
I'll ask follow-up questions about what's actually happening at each
step to confirm real understanding, not just working code copied from a
tutorial.
