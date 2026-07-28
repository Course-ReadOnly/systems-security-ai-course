> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 3.01 — Graph Search Is One Algorithm

## Why this matters

BFS, DFS, Dijkstra, and A* look like four separate algorithms you have
to memorize, each with its own pseudocode block. They aren't. They're
one algorithm — explore a frontier, expand it, repeat — with one thing
swapped out each time: the data structure that decides *which* frontier
node you expand next. Seeing that unifies this whole stage's graph
content into a single mental model instead of four memorized
procedures, and it's the exact model Stage 11 reuses for walking binary
control-flow graphs and Stage 26 reuses for compiler dataflow analysis.
Project 3.1 makes you build the "BFS vs DFS" half of this yourself, on
a maze, where the difference is directly visible.

## Core concepts

**The skeleton, stripped to its bones:** maintain a *frontier* (nodes
discovered but not yet expanded) and a *visited* set (nodes already
expanded, so you don't redo work or loop forever). Loop: pull one node
out of the frontier, mark it visited, look at its neighbors, add any
unvisited ones to the frontier. Stop when the frontier's empty or you
find your target. Every algorithm in this stage's graph section is this
loop, verbatim — the *only* thing that changes between them is what
kind of container the frontier is and, for Dijkstra/A*, how you decide
which item to pull out.

**BFS uses a queue (FIFO), and that single choice is why it finds
shortest paths.** Pulling the *oldest*-added node first means you fully
explore everything at distance 1 from the start before touching
anything at distance 2, everything at distance 2 before distance 3, and
so on — the frontier expands in concentric rings. The first time you
reach the target, you've necessarily reached it by the shortest number
of steps, because nothing farther could have been dequeued first. This
is a structural guarantee, not a happy coincidence, and it's exactly
what Project 3.1's acceptance criteria asks you to demonstrate
concretely.

**DFS uses a stack (LIFO, often literally the call stack via
recursion), and that's why it gives up the shortest-path guarantee.**
Pulling the *newest*-added node first means you commit to one branch
and follow it as deep as it goes before backing up — you might stumble
onto the target immediately, or only after wandering down a much longer
branch first. DFS still *finds* a path (if one exists) and does less
bookkeeping per step than BFS, which is why it's still useful — just
not for "shortest," ever. This is why Project 3.1 makes you implement
both from the same graph representation: the only code that should
differ between your BFS and DFS solvers is which container backs the
frontier. If you find yourself writing substantially different logic
for each, that's a sign the abstraction (frontier + visited set) hasn't
clicked yet.

**Dijkstra generalizes BFS to weighted edges by swapping the queue for
a priority queue keyed on distance-so-far.** BFS's "oldest added first"
is only a correct proxy for "closest first" when every edge costs the
same (1 step). The moment edges have different weights (Project 3.2's
route planner: real road distances), you need to explicitly track and
compare accumulated distance rather than insertion order — a priority
queue does exactly that. Same skeleton, different frontier structure,
same core guarantee (shortest path first out), now correct for weighted
graphs too.

**A* is Dijkstra with a heuristic added to the priority, and the
heuristic is a bet about which unexplored nodes are worth looking at
first.** Instead of ordering purely by "distance traveled so far"
(Dijkstra), A* orders by "distance so far + estimated distance
remaining" (e.g. straight-line distance to the goal). A good admissible
heuristic (never overestimates) still guarantees the shortest path
while exploring far fewer nodes than Dijkstra — it's Dijkstra with a
sense of direction instead of expanding equally in every direction.

## Required reading

Per `03-algorithms/README.md`'s resource table — [MIT 6.006
(OCW)](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/),
the graph search lectures (BFS/DFS, then Dijkstra) specifically. [CP-
Algorithms](https://cp-algorithms.com/) is the faster reference once
you've seen the lecture version once and just need the pseudocode again
while coding Project 3.1.

## Check yourself

1. If you implemented BFS but accidentally used a stack instead of a
   queue for the frontier, what would you actually observe — a crash,
   wrong output, or something else entirely?
2. Why can't DFS guarantee a shortest path even on an unweighted graph,
   concretely — describe a small graph where DFS's path is longer than
   BFS's.
3. Why does plain BFS break on a weighted graph — what specifically
   goes wrong if you run BFS's exact algorithm (queue, no priority) on
   a graph where edges have different costs?
4. What makes a heuristic "admissible," and what would go wrong with
   A*'s shortest-path guarantee if you used a heuristic that sometimes
   *overestimates* the remaining distance?
5. In terms of the frontier/visited-set skeleton, what's the one line
   of pseudocode that's genuinely different between Dijkstra and A*?

Answers withheld until asked.

## Project

This lecture is the bridge into **Project 3.1 — Maze Solver**
(`projects/3.1-maze-solver/SPEC.md`) — build BFS and DFS from the same
graph representation before moving to 3.2's weighted route planner.
