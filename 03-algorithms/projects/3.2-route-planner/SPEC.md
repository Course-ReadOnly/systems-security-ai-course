> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 3.2 — Route Planner

## Goal

The weighted-graph follow-up to 3.1: Dijkstra's algorithm (and optionally
A* on top of it), applied to something recognizable — shortest route
between points on a weighted graph (think: a simplified road network,
not real-world map data).

## Requirements

1. Reads a weighted graph from a file (nodes + edges with weights/costs
   — e.g. representing distances between "cities").
2. Implements **Dijkstra's algorithm** to find shortest path between two
   given nodes, reporting both the path and total cost.
3. **Stretch:** implement A* on the same graph with a real heuristic
   (e.g. straight-line distance if nodes have coordinates), and compare
   node-visit counts against plain Dijkstra to show A* actually explores
   less.
4. Handles disconnected graphs (no path between the requested nodes)
   correctly — clear "no route" result, not a crash or infinite loop.
5. Uses a real priority queue (from your Stage 2 library if it's ready,
   or a simple one built here) — not a linear scan pretending to be one,
   which defeats the point of Dijkstra's complexity guarantees.

## Acceptance criteria

- [ ] Builds/runs cleanly, no warnings
- [ ] Paste output finding shortest path + cost on a real weighted graph
      (at least ~10 nodes, enough that the "shortest" path isn't obvious
      by inspection)
- [ ] Disconnected-graph case tested and handled
- [ ] If A* attempted: paste a comparison showing fewer nodes visited
      than plain Dijkstra for the same query
- [ ] `valgrind` clean (if C)
- [ ] `git log` shows iteration

## Security relevance

Same complexity-attack concern as 3.1, plus a new one: Dijkstra's
correctness depends on non-negative edge weights — if this were ever
fed attacker-controlled weights, that assumption becoming false is
exactly the kind of subtle precondition violation that breaks security-
critical algorithms in production (cache-poisoning and routing-protocol
attacks are real-world instances of "the algorithm's assumptions no
longer hold, and nobody checked").

## When done

Point me at the source + `git log`. I'll check the priority-queue choice
first (is it actually giving you the complexity Dijkstra is supposed to
have, or just working by coincidence on small inputs), then correctness
on the disconnected case.
