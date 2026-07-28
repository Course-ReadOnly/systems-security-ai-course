> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 18.01 — Goroutines and Channels: A Different Answer to Concurrency

## Why this matters

Stage 5 and Stage 9 taught you concurrency the hard way: `pthread_create`,
mutexes, condition variables, and manually driving `epoll` to multiplex a
pile of sockets on one thread. That work wasn't wasted — it's what lets
you actually evaluate Go's model instead of just trusting it. Go was
designed by people who'd built concurrent systems in C and wanted a
language where "spawn a concurrent unit of work" and "coordinate between
them safely" were first-class primitives instead of something you
hand-roll with `pthread.h` and discipline. 18.1 redoes Stage 9.3's port
scanner specifically so you can compare the two approaches on the same
problem, and Go's concurrency model matters well beyond this stage — it's
why a large share of real security tooling (Nuclei, many C2 frameworks,
cloud-security scanners) is written in Go in the first place.

## Core concepts

**A goroutine is not an OS thread.** `pthread_create` asks the OS for a
real kernel thread, with a default stack around 2MB (Stage 5's `ulimit -s`
world) and real scheduling overhead. `go func()` asks the *Go runtime* for
a goroutine — starts around 2KB of stack, grows as needed, and gets
multiplexed onto a small pool of OS threads by Go's own scheduler (an M:N
model — many goroutines mapped onto few OS threads). This is why spawning
one goroutine per port on a large scan range is *plausible* in Go in a way
spawning one pthread per port never was — but "plausible" isn't "free,"
which is exactly the trap 18.1's SPEC calls out.

**Channels are the actual mechanism, and the philosophy behind them is
the real content of this lecture:** "don't communicate by sharing memory;
share memory by communicating." In Stage 5/8, two threads coordinate by
both touching the same variable, protected by a mutex you have to remember
to acquire *every single time* you touch that variable — the bug class is
someone forgetting the lock once. In Go's idiom, a goroutine that produces
a result sends it *through* a channel to whichever goroutine consumes it;
ownership of the data moves with the send. There's still a mutex under the
hood (channels are implemented with one), but you don't manage it — you
can't forget to lock what you never had to lock explicitly.

**The unbounded-goroutine footgun is precisely what 18.1 is designed to
surface.** `for port := range ports { go scan(port) }` with no limit will
happily spawn tens of thousands of goroutines against a large range. Each
one is cheap alone, but cheap × 65535, all opening a TCP connection
roughly simultaneously, is not cheap in aggregate — you'll exhaust file
descriptors or hammer the target in a burst instead of a controlled scan.
The fix is a **worker pool**: a fixed number of goroutines pulling jobs
off a channel acting as a queue, with the channel's buffer size (or a
semaphore pattern) bounding concurrency. This is the direct structural
analog of a fixed-size thread pool with a work queue in C — same idea,
except the queue and its synchronization are a language primitive instead
of something you build from a mutex, a condvar, and a linked list.

**`select` is Go's `epoll`, scoped to channels instead of file
descriptors.** Stage 9's `epoll` loop let one thread wait on many sockets
at once and react to whichever became ready first. `select` over channels
does the same job at the language level: wait on multiple channel
operations, proceed with whichever is ready. `time.After(d)` returns a
channel that fires after a duration — combine it with `select` and you get
per-connection timeouts (18.1's requirement #2) without any manual
alarm/`select()`-with-timeout plumbing.

**Memory safety doesn't mean leak safety.** Go's GC and bounds-checked
slices eliminate the classic C bug class (use-after-free, buffer
overflow) — but a goroutine blocked forever on a channel nobody will ever
write to is a *leaked goroutine*, functionally the same failure mode as a
thread that never gets joined and never exits. The GC frees unreachable
*memory*; it has no concept of an unreachable-but-still-running goroutine.
This is the Go-native version of a bug you already know how to think
about from Stage 5 — same failure shape, new syntax to cause it.

## Required reading

Per `ROADMAP.md`'s Stage 18 resource table: [A Tour of
Go](https://go.dev/tour/)'s Concurrency module (goroutines, channels,
buffered channels, `select`) is the required baseline. Then, before
writing 18.1, read [Go by Example](https://gobyexample.com/)'s "Worker
Pools" and "Select" pages specifically — that's the exact pattern the
project's acceptance criteria expects.

## Check yourself

1. Why does a 2KB starting stack (vs. a pthread's ~2MB default) make
   spawning tens of thousands of concurrent units *plausible* in Go —
   and why does "plausible" still not mean "safe to do unbounded" on a
   large port range?
2. Contrast a shared counter protected by `sync.Mutex` with the same
   result sent back over a channel. Both are valid Go — which is more
   idiomatic for collecting scan results across workers, and what bug
   does the channel version structurally rule out that the mutex version
   doesn't?
3. Concretely, how does `select { case <-resultChan: ... case
   <-time.After(timeout): ... }` implement a per-port timeout — walk
   through what happens on each branch.
4. What is a goroutine leak, precisely, and why doesn't Go's garbage
   collector protect you from it the way it protects you from a dangling
   pointer?
5. Describe the worker-pool fix for 18.1's port scanner: what are the two
   moving pieces (the job source and the workers), and what specifically
   bounds how many connections are ever attempted at once?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 18.1 — Port Scanner (Go)**
(`projects/18.1-port-scanner/SPEC.md`). Start there.
