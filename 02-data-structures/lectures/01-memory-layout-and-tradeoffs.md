> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 2.01 — Memory Layout Is the Tradeoff

## Why this matters

Every structure in Project 2.1 looks different on paper — a vector, a
linked list, a hash map, a BST — but they're all answers to the exact
same question: *where do you put the next element in memory, and what
does that decision cost you?* Once you see that, "which structure
should I use here" stops being a memorization exercise (vector = fast,
linked list = flexible) and becomes something you can derive from first
principles. That skill is the entire point of Stage 3 (choosing the
right algorithm) and comes back hard from Stage 8 (OS) onward, where
the kernel is making these exact same layout decisions about page
tables, process lists, and file system metadata.

## Core concepts

**Contiguous storage (the array/vector family) trades flexibility for
speed.** A vector is just a block of memory where element `i` lives at
`base_address + i * element_size` — no pointer chasing, one arithmetic
operation to reach anything. This is why indexing is O(1) and, just as
important, why iterating a vector is fast *in practice*, not just in
Big-O: consecutive elements sit next to each other in RAM, so the CPU's
cache pulls in a whole cache line's worth of upcoming elements on the
first access. A linked list's nodes can be scattered anywhere the
allocator put them — same O(n) traversal in theory, but dramatically
more cache misses in practice. This is the gap between asymptotic
complexity and real-world speed that a Big-O table alone never tells
you.

**The cost of contiguity shows up at insert/delete, not access.**
Insert at the front of a vector means shifting every existing element
over by one slot — O(n). A linked list just rewires two pointers —
O(1), *if* you already hold a pointer to the right spot. This is the
core tradeoff, full stop: arrays win at "get me element i," linked
structures win at "insert/remove here without moving everything else."
Every other structure in this stage is a more elaborate answer to the
same question.

**Amortized growth is how a vector fakes "dynamic size" on top of fixed-
size contiguous memory.** You can't ask the allocator to "extend this
block in place" reliably, so a vector that's full allocates a *new*,
larger block (typically 1.5x-2x) and copies everything over. That copy
is O(n) — expensive — but happens rarely enough (each doubling buys
room for as many new elements as everything that came before it
combined) that the *average* cost per push, amortized over many pushes,
is still O(1). Understanding *why* the growth factor matters (too small
and you copy too often; the exact factor is a real, debatable tuning
choice) is more valuable here than memorizing "vectors are O(1)
push_back."

**A hash map is a contiguous array wearing a trick.** The array gives
you O(1) access *if you know the index* — a hash function's entire job
is turning an arbitrary key into an index deterministically, so you get
array-speed lookup for arbitrary keys. Collisions (two keys hashing to
the same slot) are the tax you pay for compressing an infinite key space
into a finite array, and chaining vs. open addressing are just two
different strategies for paying it — chaining falls back to a linked
list per bucket (pointer-chasing again, but only among the colliding
few), open addressing stays fully contiguous by probing for the next
free slot. Neither is "correct" — it's a real tradeoff you have to
justify in Project 2.1's README, not a default to copy.

**A BST is a linked structure that encodes order in its shape, not its
address.** Where a linked list only tells you "what's next," a BST's
left/right pointers encode a comparison ("everything left of me is
smaller") — which is what turns O(n) linear search into O(log n),
*as long as the tree stays roughly balanced*. An unbalanced BST fed
sorted input degenerates into a linked list with extra steps — same
pointer-chasing, same O(n) worst case, which is exactly why AVL/red-
black trees (this stage's stretch goal) exist: the same idea, with an
explicit rule enforcing balance.

## Required reading

Per `02-data-structures/README.md`'s resource table — [MIT 6.006
(OCW)](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/),
the lectures covering arrays, linked lists, and hashing specifically.
Use [VisuAlgo](https://visualgo.net/en) alongside it to actually watch
insert/delete/collision-resolution animate — the layout argument above
is much easier to internalize visually than from a textbook diagram.

## Check yourself

1. A vector and a linked list both have O(n) worst-case search. Why is
   the vector's version almost always faster in practice, and under
   what circumstance would that stop being true?
2. If a vector grows by a *fixed* amount (e.g. +10 slots) each time it's
   full, instead of doubling, why does that make repeated push_back
   calls O(n) per call on average instead of O(1)?
3. In a chaining hash map, what happens to lookup time as the load
   factor (elements / bucket count) grows well past 1 — and why does
   resizing the bucket array fix it?
4. Why does inserting already-sorted data into a plain (unbalanced) BST
   produce the worst possible shape, and what does that shape actually
   look like?
5. Project 2.1 requires documenting who owns/frees each element. Why is
   that specifically harder to get right in a hash map with chaining
   than in a plain vector of values?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 2.1 — STL-like Generic
Library in C** (`projects/2.1-stl-library/SPEC.md`) — read its
core/stretch split before starting; this is one consolidated project
covering the whole stage, not eleven separate ones.
