> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached — this assumes C fluency from Stage 1.

# Project 2.1 — STL-like Generic Library in C

## Goal

A reusable, generic data-structure library — the kind of thing you'd
actually link against in later C projects instead of rewriting a linked
list every time. "Generic" in C means `void*`-based storage (or a macro-
generated approach) — deciding how to handle arbitrary element types safely
is itself a core part of this project, not incidental.

Eleven structures is a lot for one project — split into **core**
(required) and **stretch** (optional, do if time allows) so this stays
realistic rather than an unbounded mega-project.

## Requirements — Core (required)

1. **Vector** (dynamic array): push/pop/get/set, grows automatically.
2. **Linked list** (singly or doubly, your choice): insert/remove/traverse.
3. **Stack** and **Queue**: can be thin wrappers over vector/linked list —
   the point is the interface, not reinventing storage.
4. **Hash map**: insert/lookup/delete, your own hash function, collision
   handling (chaining or open addressing — pick one and justify it).
5. **Binary search tree** (unbalanced is fine here): insert/lookup/delete/
   in-order traversal.
6. Consistent, documented ownership rules for every structure: who
   allocates elements, who's responsible for freeing them. This is the
   single most common source of bugs in a project like this.
7. **Zero memory leaks** across all core structures — `valgrind`-clean.
8. A `Makefile` building the library and a test/demo executable.

## Requirements — Stretch (optional)

Pick any of these if the core is solid and you want more:

- **Heap** (binary heap, for a priority queue)
- **Trie** (prefix tree, string-keyed)
- **Graph** (adjacency list, plus BFS/DFS traversal)
- **AVL or red-black tree** (a self-balancing BST — significantly harder
  than the plain BST above; don't attempt until the plain BST is solid)

## Acceptance criteria

- [ ] All five core structures implemented, each with a small test/demo
      showing correct behavior (paste output)
- [ ] `valgrind` clean across every structure's test — paste output
- [ ] Memory ownership documented (in code comments or README) — who
      frees what
- [ ] At least one deliberately-broken case tested per structure where
      relevant (e.g. removing from an empty stack, looking up a missing
      hash key) — confirm it fails safely, not with a crash/UB
- [ ] `git log` shows real iteration
- [ ] README explaining the design choices (why chaining vs. open
      addressing, why this hash function, etc.) in your own words
- [ ] Any stretch structures attempted, same rigor as core

## When done

Point me at the source + `git log`. Say "review my code" — I'll check
ownership/free correctness hardest (this is where generic C data
structures usually go wrong), and whether the "generic" mechanism
(`void*` or macros) is actually type-safe in practice, not just in theory.
