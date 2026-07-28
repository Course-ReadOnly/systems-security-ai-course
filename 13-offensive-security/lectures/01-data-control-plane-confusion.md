> **Generated ahead of schedule** (2026-07-28, per learner request). Revisit
> when actually reached — this is a bridge to the source material, not a
> replacement for it.

# Lecture 13.01 — Data/Control-Plane Confusion

## Why this matters

This stage looks like two unrelated skill sets — SQL injection has
nothing to do with a stack buffer overflow, on the surface. It does.
Every exploit class in 13.1, from PortSwigger's web labs to ROP
Emporium's binaries, is the same root cause wearing a different
costume: somewhere, attacker-controlled *data* gets interpreted as
*instructions* by something downstream that was never told to draw a
hard line between the two. See that once and you stop memorizing a
list of vulnerability classes and start recognizing the shape wherever
it shows up — including in Stage 24's smart contracts and Stage 25's
prompt-injection work, both of which are this exact bug in new
clothing.

## Core concepts

**Every program draws an implicit line between "data" and "control."**
Data is the stuff the program processes — a search term, a username,
a number to add. Control is what decides *what the program does next*
— a return address, a SQL keyword, a format specifier, an HTML tag.
The program's author assumes user input stays on the data side of that
line. Exploitation is finding the place where that assumption is
false — where input the author thought was inert actually gets parsed,
interpreted, or executed as control.

**SQL injection** is the cleanest example. `"SELECT * FROM users WHERE
name = '" + input + "'"` treats `input` as data — until `input`
contains a `'`, and now part of what you supplied is syntax the SQL
parser reads as *structure*, not as a name to search for. The
vulnerability isn't "forgetting to sanitize a string" in the abstract
— it's that string concatenation builds the query and the input, using
the same channel, so there is no actual boundary between them for the
parser to respect. Parameterized queries fix this not by "escaping
better" but by sending data and query structure over genuinely
separate channels, so the database itself can't confuse one for the
other.

**A stack buffer overflow is the identical bug on a different
substrate.** `strcpy(buf, input)` with no bounds check writes past
`buf` and, if `buf` is a stack-local array, eventually overwrites the
saved return address sitting further up the stack. The CPU doesn't
know or care that those bytes came from user input — when the function
returns, it jumps to whatever's in that slot, treating attacker data as
a control-flow target. Format string bugs (`printf(input)` instead of
`printf("%s", input)`) are the same idea one layer up: `input` is data,
but if it contains `%x` or `%n`, `printf` reads it as *formatting
instructions* — `%n` will even write to memory. Three completely
different technologies, one identical root cause.

**ROP exists because the direct version of this attack got mitigated.**
Once DEP/NX made the stack non-executable, you can overwrite the
return address, but you can't point it at injected shellcode anymore —
the CPU refuses to execute stack memory. Return-Oriented Programming
routes around this by pointing the return address at tiny, legitimate
instruction sequences that already exist in the executable's own
loaded code (a "gadget," typically ending in `ret`), and chaining many
of them via a stack full of attacker-controlled addresses. You're
still exploiting data/control confusion — the stack data still becomes
a sequence of control-flow jumps — you're just building the "shellcode"
out of the program's own bytes so there's nothing new to block. Read
`SECURITY-CONCEPTS.md`'s "Mitigation Bypass" entry for the fuller
canary → DEP/NX → ROP → ASLR arms-race history before 13.1's ROP
Emporium work; that context is what makes the technique make sense
instead of feeling like an arbitrary trick.

**Access control and SSRF bugs generalize the same pattern one level
up.** The "control" being confused isn't a parser's syntax, it's a
trust decision: "this request came from an authenticated admin," "this
URL is safe for the server to fetch." The server treats attacker-
supplied data (a role parameter, a URL) as if it were a control signal
it already validated, when it never actually enforced that boundary.
Same shape, no parser involved at all — which is why this framing
outlasts any specific vulnerability list.

## Required reading

Per this stage's `README.md` resource table: [PortSwigger Web Security
Academy](https://portswigger.net/web-security) for the web-exploitation
half — work the labs, don't just read the theory pages. For binary
exploitation, [ROP Emporium](https://ropemporium.com/) — its challenges
are ordered specifically to build from a plain stack overflow up to
full ROP chains.

## Check yourself

1. In a parameterized SQL query, data and query structure travel to
   the database over separate channels. What's the equivalent
   separation that DEP/NX enforces on a CPU — what two things does it
   keep apart, and how?
2. Why does a format string bug (`printf(input)`) count as data/control
   confusion even though there's no buffer overflow and no return
   address involved at all?
3. A ROP gadget chain is built entirely out of instructions already
   present in the target binary. Why does that specifically defeat a
   mitigation whose whole point is "don't execute injected code"?
4. An SSRF bug lets an attacker make the server fetch an
   attacker-chosen URL. What's the "data" and what's the "control"
   being confused here, given there's no parser or CPU instruction
   pointer in sight?
5. Once you understand the data/control framing, what would you look
   for first when reading unfamiliar code to spot a candidate
   vulnerability, before even trying specific payloads?

Answers withheld until asked — the PortSwigger and ROP Emporium labs in
13.1 are where these stop being abstract.

## Project

This lecture is the bridge into **Project 13.1 — Exploit Labs
(Self-Hosted)** (`projects/13.1-exploit-labs/SPEC.md`). Start there —
everything targets designated legal practice platforms only, per this
stage's scope note.
