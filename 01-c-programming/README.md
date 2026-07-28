# Stage 1 — C Programming (Core)

**Time budget:** 6–9 weeks part-time / 3 weeks full-time

## Objectives

By the end of this stage you should be comfortable writing and debugging
real C programs end to end: variables and control flow through pointers,
manual memory management, and structuring a program across multiple files
with `make`/`cmake`. This is the language everything from Stage 2 (data
structures) through Stage 8 (OS) and Stage 11 (reverse engineering) is
built on top of — gaps here compound later.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Full language (variables → pointers → memory) | [Beej's Guide to C](https://beej.us/guide/bgc/) |
| 02 | Deeper / modern semantics | [Modern C by Jens Gustedt](https://upload.wikimedia.org/wikipedia/commons/0/0a/Modern_C.pdf) |
| 03 | Structured course w/ problem sets | [CS50 (Harvard)](https://cs50.harvard.edu/x/) |
| 04 | Interactive drills | [learn-c.org](https://www.learn-c.org/) |
| 05 | Reference | [C Reference (cppreference.com)](https://en.cppreference.com/w/c) |

## Projects

Unlike Stage 0, ROADMAP.md presents this stage's projects as a graded
menu (easy → hard) rather than a fixed must-do-all list. Provisional
numbering below for folder consistency — **which ones we actually do, and
in what order, gets decided when we're actually here**, based on your pace
and where gaps show up in Stage 0. Treat this table as a menu, not a
checklist.

| # | Project | Difficulty | Folder |
|---|---|---|---|
| 1.1 | Calculator | Easy | `projects/1.1-calculator/` |
| 1.2 | Todo app | Easy | `projects/1.2-todo-app/` |
| 1.3 | File copier | Easy | `projects/1.3-file-copier/` |
| 1.4 | Text statistics tool | Easy | `projects/1.4-text-statistics/` |
| 1.5 | Hex editor | Medium | `projects/1.5-hex-editor/` |
| 1.6 | Config parser | Medium | `projects/1.6-config-parser/` |
| 1.7 | INI parser | Medium | `projects/1.7-ini-parser/` |
| 1.8 | JSON parser | Medium | `projects/1.8-json-parser/` |
| 1.9 | Text editor | Hard | `projects/1.9-text-editor/` |
| 1.10 | Terminal UI | Hard | `projects/1.10-terminal-ui/` |
| 1.11 | CSV library | Hard | `projects/1.11-csv-library/` |

> **Generated ahead of schedule** (2026-07-27, per learner request). All 11
> `SPEC.md` files above exist and are fully written — revisit when this
> stage is actually reached, per this course's usual generated-ahead
> caveat.

## Note on environment

Same WSL2 Ubuntu shell as Stage 0. `gcc`/`make`/`cmake`/`gdb`/`valgrind`
should already be installed via 0.2's `setup.sh` by the time you get here.
