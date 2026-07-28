> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 16.01 — Abstraction Bottoms Out in Gates

## Why this matters

Stage 4's NAND2Tetris CPU was simulated — every gate was a function
call, every clock tick was a loop iteration, and a bug meant a wrong
number on a screen. This stage builds the same idea again, except now
a "1" is 5 volts on a real wire and a bug can mean a chip that gets hot
or a program counter that never increments. The whole software stack
you've spent this course learning — variables, functions, instructions
— is a tower of abstractions that has to bottom out somewhere in
physical reality. This stage is where you stand at that bottom and
watch the tower get built back up, gate by gate, in front of you.

## Core concepts

**A logic gate is an analog circuit that a digital abstraction is
imposed on, not a mathematical primitive that exists in nature.** A
74-series NAND chip is transistors and voltage; "0 and 1" is an
interpretation layered on top — voltage below some threshold reads as
0, above another threshold reads as 1, and the gap between those
thresholds (the "forbidden zone") exists specifically so that noise
and imperfect components don't flip your interpretation. Every layer
above this — NAND2Tetris's simulated gates, your CPU's registers, a
Python `int` — is more digital abstraction stacked on top of this one
analog-to-digital act of interpretation. It works reliably because
each layer's designer over-engineered enough margin that the layer
below almost never violates it, not because "1 and 0" are physically
real things.

**Propagation delay is why "instant" logic doesn't exist.** A NAND
gate doesn't produce a stable output the instant its inputs change —
current has to flow, transistors have to switch state, and that takes
a small but nonzero time. Chain gates together (an ALU built from many
of them) and the delays add up along the longest path through the
circuit — the "critical path." This one fact is *why clock speed is a
real physical limit* and not an arbitrary marketing number: the clock
period has to be long enough for a signal to finish propagating
through the slowest path in the circuit before the next clock edge
tells a register to latch whatever value is sitting at its input.
Clock the circuit faster than its critical path allows, and a register
latches a half-settled, garbage value — this is the physical-hardware
version of a race condition, and it's not fixable in software.

**A clock is not "time," it's a synchronization signal that turns a
pile of combinational logic into something with sequential state.**
Combinational logic (plain gates, an ALU) computes a function of its
current inputs with no memory. A register (built from gates, but
wired to *hold* its output until told otherwise) only updates on a
clock edge. The entire "fetch-decode-execute" cycle you learned as an
abstract concept in Stage 4 is, physically, just: combinational logic
computes the next state from the current state, and on each clock
edge, registers latch that computed value as the new "current state."
There's no other mechanism — a CPU is combinational logic plus
registers plus a clock, repeated.

**Setup and hold time are the fine print that makes registers
trustworthy.** A register needs its input to be *stable* for some
window of time before the clock edge (setup time) and for some window
after it (hold time) — sample it while the input is still changing and
you get an undefined, possibly metastable result: a voltage stuck
between "0" and "1" that can resolve either way, unpredictably, some
time later. This is the physical reason a breadboard build with long,
noisy jumper wires and a hand-wired clock circuit is *more* failure-
prone than the equivalent simulated circuit — real wires have
capacitance and real gates have delay that a simulator's ideal model
doesn't force you to account for.

**PCB design and FPGAs are two different answers to "how do I stop
hand-wiring this."** A PCB (Stage 16.2's territory via KiCad) fixes
the *layout* — a physical circuit gets etched into copper traces
instead of jumper wires, which drastically reduces the noise and
inconsistent-delay problems above. An FPGA (via the Yosys open-source
toolchain) fixes something different: it's a chip made of thousands of
reconfigurable logic blocks that get wired together *electrically*, at
configuration time, to implement whatever circuit you describe in an
HDL (hardware description language). You're not writing a program that
runs sequentially — you're describing a circuit's structure, and the
toolchain configures real gates to physically become that circuit.
That's a fundamentally different mental model from software, and it's
worth sitting with the discomfort of it now, briefly, even though 16.1
itself is breadboard-only.

## Required reading

Per this stage's `README.md` resource table: [NAND2Tetris](https://www.nand2tetris.org/)
for the architecture you're rebuilding physically — if you did Stage
4's software version, revisit its chapter on the CPU and clock/register
model specifically, since that's what you're about to make real.
Ben Eater's breadboard-CPU build (the de facto guide for 16.1, per the
project spec) supplements this with the physical wiring and timing
details NAND2Tetris deliberately abstracts away.

## Check yourself

1. Why is "propagation delay" a physical property of the circuit's
   longest path, not a fixed number per gate — what determines the
   maximum clock speed a given circuit can run at?
2. A register updates on a clock edge, not continuously. What would go
   wrong, concretely, if a register updated the instant its input
   changed instead — what does gating updates to a clock edge actually
   buy you in a circuit with feedback (like a counter feeding its own
   next value)?
3. If two signals reach a register at slightly different times because
   their wires are different lengths, what specific timing violation
   does that risk, and what's the observable symptom on your breadboard
   build?
4. In your own words: what's the actual difference between "an FPGA
   runs your HDL code" and "an FPGA is configured, at load time, to
   become a circuit that implements your HDL description"? Why does
   the second framing matter for how you'd debug it?
5. NAND2Tetris's simulated clock and your breadboard's real clock
   circuit both drive the same logical CPU design. Name one failure
   mode that's possible on the breadboard version that's structurally
   impossible in the simulator.

Answers withheld until asked — 16.1's build is where setup/hold time
and propagation delay stop being abstract and start being "why is my
counter reading garbage."

## Project

This lecture is the bridge into **Project 16.1 — Breadboard CPU**
(`projects/16.1-breadboard-cpu/SPEC.md`). Start there — note the
stage-level requirement that this needs real components (breadboards,
74-series ICs); flag it in STATUS.md if hardware access is a blocker.
