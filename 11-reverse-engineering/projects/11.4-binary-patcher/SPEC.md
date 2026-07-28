> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 11.4 — Binary Patcher

## Goal

Modify a compiled binary's behavior by editing raw bytes — no source, no
recompiling. This closes the loop on 11.1's crackme-solving: instead of
finding the right input, you directly change the binary's logic (e.g.
flip a conditional jump), the technique behind most crackme "patched"
solutions and plenty of real-world binary patching.

## Requirements

1. Given a target binary and a specific instruction to modify (e.g. a
   conditional jump you want to force one way), correctly locates the
   right bytes using your understanding of the binary's layout (from
   11.2/11.3's parsing work or a disassembler) and patches them.
2. Preserves the binary's overall structure — patching one instruction
   must not corrupt anything else (section headers, other code) or make
   the binary unloadable.
3. Verifies the patch actually changes runtime behavior, not just that
   the file's bytes changed — run the patched binary and observe the
   intended behavioral difference.
4. Works against **at least one real crackme** from your 11.1 set —
   patch it to always "succeed" regardless of input, as an alternative
   to solving it via correct input.

## Acceptance criteria

- [ ] A working patcher (script or program) that takes a target file +
      patch instructions and produces a modified binary
- [ ] Paste a disassembly diff (before/after, e.g. via objdump/Ghidra)
      showing exactly which bytes changed and why
- [ ] Paste the patched binary actually running with the new behavior —
      the real proof this isn't just byte-editing for its own sake
- [ ] Confirm the patched binary still runs correctly otherwise (didn't
      break anything unrelated)
- [ ] `git log` shows iteration

## Security relevance

Binary patching is dual-use in the most direct sense: the exact
technique used here to bypass a crackme's check is the same technique
used to bypass a real license check, disable a security control in a
compromised binary, or (defensively) apply a hex-level fix when source
isn't available. Requirement 2 (don't corrupt anything else) matters
for a security reason beyond correctness — a patch that shifts file
offsets without updating dependent structures is exactly the kind of
mistake that turns a working exploit/patch into a crashed process.

## When done

Point me at the tool + `git log` and the before/after disassembly diff
plus the running proof. I'll check that the patch is minimal and
targeted — a patch that happens to work by accidentally breaking a
bounds check elsewhere isn't a good patch, even if the demo looks right.
