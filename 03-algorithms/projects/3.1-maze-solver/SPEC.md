> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 3.1 — Maze Solver

## Goal

BFS/DFS applied to something visual and checkable — a grid maze. This is
deliberately the easier of the two Stage 3 projects: unweighted graph
search (every move costs the same), building toward 3.2's weighted
version.

## Requirements

1. Reads a maze from a text file (e.g. `#` for wall, `.` for open, `S`/`E`
   for start/end) — represent it internally as a graph (grid cells as
   nodes, adjacency = non-wall neighbors).
2. Implements **both** BFS and DFS as separate, selectable solvers —
   comparing them is the point, not just picking one.
3. Outputs whether a path exists, and if so, the path itself (e.g.
   printed as coordinates or an overlay on the maze).
4. Reports path length (BFS) — and can demonstrate BFS finds the
   *shortest* path while DFS doesn't necessarily.
5. Handles a maze with no solution (correctly reports "no path," doesn't
   hang or crash).
6. Language: C (continuing Stage 1/2's track) unless there's a specific
   reason to use something else — note that reason in the README if so.

## Acceptance criteria

- [ ] Builds cleanly (or runs cleanly, if not C), no warnings
- [ ] Paste output solving a real maze with both BFS and DFS, showing
      both find *a* path but potentially different ones
- [ ] Demonstrate BFS's shortest-path guarantee concretely — a maze where
      DFS's path is provably longer than BFS's
- [ ] No-solution maze tested, handled cleanly
- [ ] `valgrind` clean (if C)
- [ ] `git log` shows iteration

## When done

Point me at the source + `git log`. I'll check that BFS is actually
breadth-first (not accidentally degenerating into DFS due to using the
wrong data structure — a stack instead of a queue is the classic mistake
here).
