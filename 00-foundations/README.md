# Stage 0 — Foundations

**Time budget:** 2–3 weeks part-time / 1 week full-time

## Objectives

By the end of this stage you should be able to live comfortably in a Linux
terminal, write small Bash scripts, use Git for real version control, build
C code with GCC/Make/CMake, debug with GDB, catch memory bugs with Valgrind,
and be functional with Docker and SSH. This stage is tooling — it exists so
nothing in Stage 1 onward is blocked by "how do I even run this."

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | Linux terminal & CLI | [Linux Journey](https://linuxjourney.com/) |
| 02 | Shell fundamentals | [MIT Missing Semester](https://missing.csail.mit.edu/) |
| 03 | Bash scripting | [Bash Guide (Greg's Wiki)](https://mywiki.wooledge.org/BashGuide) |
| 04 | Git | [Pro Git book](https://git-scm.com/book/en/v2) |
| 05 | Editors (Vim/Neovim/VS Code) | [OpenVim](https://www.openvim.com/) (fully free) + [Vim Adventures](https://vim-adventures.com/) (early levels free, full game paid) + [Neovim docs](https://neovim.io/doc/) |
| 06 | GCC/Clang, Make | [GNU Make Manual](https://www.gnu.org/software/make/manual/make.html) |
| 07 | CMake | [CMake official tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html) |
| 08 | GDB | [Beej's GDB Quick Start](https://beej.us/guide/bggdb/) |
| 09 | Valgrind | [Valgrind Quick Start](https://valgrind.org/docs/manual/quick-start.html) |
| 10 | Docker | [Docker Official Docs](https://docs.docker.com/get-started/) |
| 11 | SSH | [SSH Essentials (DigitalOcean)](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys) |
| 12 | Practice | [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) |

## Projects

| # | Project | Folder |
|---|---|---|
| 0.1 | Dotfiles repo | `projects/0.1-dotfiles-repo/` |
| 0.2 | Linux workstation setup script | `projects/0.2-workstation-setup/` |
| 0.3 | Small bash automation scripts | `projects/0.3-bash-automation/` |
| 0.4 | File organizer script | `projects/0.4-file-organizer/` |
| 0.5 | Backup utility script | `projects/0.5-backup-utility/` |
| 0.6 | Capstone: tie 0.1-0.5 together | `projects/0.6-capstone/` |

Folders are numbered `{stage}.{project}` so it stays unambiguous once later
stages have projects of their own. All six `SPEC.md` files above
(0.1-0.6) were generated ahead of schedule (2026-07-27, per learner
request — see `STATUS.md`) rather than strictly on-demand; treat 0.3
onward as drafts to revise once actually reached, not contracts.

**0.6 (added 2026-07-26, not in the original ROADMAP.md project list):** a
capstone combining the dotfiles repo, workstation setup script, bash
automation scripts, file organizer, and backup utility into one coherent
setup — likely a single entry-point script that calls into the others,
mirroring how `0.2`'s `setup.sh` already calls into `0.1`'s `install.sh`.
Its `SPEC.md` exists and is written, but is explicitly flagged in-file as
the most likely of the six to need real revision, since it depends on
the exact shape 0.3-0.5 end up taking.

On the learner's WSL machine, each numbered project lives as its own git
repo under `~/00-foundations-project/{n.n-name}/` (e.g.
`~/00-foundations-project/0.1-dotfiles-repo/`) — separate repos, not one
monorepo, so each project's `git log` stays scoped to that project.

## Note on environment

You're on Windows. For a Linux-native feel (needed for Bandit, real Bash,
POSIX tools), you'll want either WSL2 (Ubuntu) or a Docker container as your
day-to-day shell for this stage onward — we'll set that up as part of
Lecture 01.
