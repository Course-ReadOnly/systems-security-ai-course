> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 11.3 — PE Parser

## Goal

The Windows equivalent of 11.2 — parse the PE (Portable Executable)
format: headers, sections, and critically the **import/export tables**,
directly building on Stage 6's DLL project (now reading the export table
you built there, from the outside, plus reading imports for the first
time). This is the format every Windows malware sample in Stage 12 comes
wrapped in.

## Requirements

1. Parses the DOS header, PE header (`IMAGE_NT_HEADERS`), and section
   headers.
2. Parses the **import table**: which DLLs this binary depends on and
   which functions it imports from each — this is often the single most
   revealing thing about what a binary does, and directly what Stage 12's
   malware triage relies on.
3. Parses the **export table** if present (relevant for DLLs — reuse
   your Stage 6 DLL as a real test case here).
4. Correctly handles both 32-bit (`PE32`) and 64-bit (`PE32+`) — or
   documents supporting only one, with why.
5. Handles a corrupted/truncated PE file without crashing.

## Acceptance criteria

- [ ] Builds cleanly, no warnings
- [ ] Paste output parsing a real Windows executable's import table,
      cross-checked against a known tool (e.g. `dumpbin /imports`, or
      PE-bear/CFF Explorer if available) for agreement
- [ ] Your Stage 6 DLL parsed for its export table, confirming it
      matches what `dumpbin /exports` showed back in that project
- [ ] Corrupted-file case tested and handled cleanly
- [ ] `git log` shows iteration
- [ ] README explaining why the import table matters for malware
      triage, in your own words — this is direct prep for Stage 12

## Security relevance

Already the load-bearing point of Requirement 2: an import table is
often the fastest, cheapest signal in malware triage — `WinHTTP`/
`WinInet` imports suggest network capability, `CreateRemoteThread`/
`WriteProcessMemory` suggest process injection, `CryptEncrypt`-family
imports suggest ransomware, all readable before a single instruction is
disassembled. Requirement 5 (handling corrupted/truncated files) is the
same untrusted-input discipline as every other parser in this course —
here the stakes are higher, since the files this parser will eventually
see in Stage 12 are actively hostile, not just imperfect.

## When done

Point me at the source + `git log` and the cross-checks. Import-table
parsing correctness is what I'll check first — this exact skill is
reused, not just conceptually but literally, in Stage 12.
