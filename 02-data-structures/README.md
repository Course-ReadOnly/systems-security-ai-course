> **Generated ahead of schedule** (2026-07-27, per learner request, going as
> far as reasonably possible through the roadmap). Revisit when actually
> reached — this stage assumes Stage 1's C fluency, which doesn't exist yet.

# Stage 2 — Data Structures

**Time budget:** 6–8 weeks part-time / 3 weeks full-time

## Objectives

Implement the data structures everything else takes for granted, from
scratch, in C — no `<stdlib.h>` shortcuts. By the end you should be able to
explain the time/space tradeoffs of each one and pick the right one under
pressure, not just recite definitions. This stage is the direct foundation
for Stage 3 (Algorithms) and comes back constantly from Stage 8 (OS) onward.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Core theory & algorithms | [MIT 6.006 (OCW)](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) |
| 02 | Visualization | [VisuAlgo](https://visualgo.net/en) |
| 03 | Written reference | [CP-Algorithms](https://cp-algorithms.com/) |
| 04 | Practice problems | [freeCodeCamp DS&A](https://www.freecodecamp.org/) |

**Structures to implement yourself (in C):** vector, linked list, stack,
queue, hash map, binary tree, AVL tree, red-black tree, heap, trie, graph.

## Projects

| # | Project | Folder |
|---|---|---|
| 2.1 | STL-like generic library in C | `projects/2.1-stl-library/` |

Unlike later stages with several separate small projects, ROADMAP.md frames
this stage as **one** consolidated library project spanning all the
structures above — see `2.1`'s spec for a realistic core/stretch split
rather than treating all eleven structures as equally mandatory.
