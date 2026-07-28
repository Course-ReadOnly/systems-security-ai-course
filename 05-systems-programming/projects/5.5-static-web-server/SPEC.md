> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Project 5.5 — A Static Web Server

## Goal

A focused variant of 5.4: serve files from disk correctly and safely.
The real content of this project is the "safely" part — path traversal
is a genuine, common vulnerability class, and this is where you learn to
close it yourself before Stage 13 teaches you to exploit it in other
people's code.

## Requirements

1. Serves static files from a configured document root directory over
   HTTP `GET`.
2. Correct `Content-Type` based on file extension (at minimum:
   `.html`, `.txt`, `.css`, a binary fallback like
   `application/octet-stream`).
3. **Path traversal prevention**: a request for `/../../etc/passwd` (or
   equivalent) must **not** escape the document root — this is the
   load-bearing security requirement of this project, not optional
   polish.
4. Correct `404` for missing files, `403`-equivalent behavior (or a
   clear policy decision, documented) for files outside the root.
5. Can reuse 5.4's socket/HTTP-parsing code rather than duplicating it —
   if you build both, this one should be the smaller diff.

## Acceptance criteria

- [ ] Builds cleanly, `-Wall -Wextra` clean
- [ ] Paste `curl` output serving a real file correctly (right content,
      right `Content-Type`)
- [ ] **Path-traversal attempt pasted, showing it's blocked** — this is
      the single most important piece of evidence for this project.
      Try several variants (`../`, URL-encoded `%2e%2e%2f`, absolute
      paths) — a naive string check that only blocks literal `../` is
      not sufficient
- [ ] 404 case tested
- [ ] `git log` shows iteration

## Security relevance

Path traversal is a named instance of a broader class covered in
`SECURITY-CONCEPTS.md`'s "Access Control / Scoping" entry: a boundary
the code is supposed to enforce (requests stay inside the document
root) gets violated because the check happens on the wrong
representation of the input (raw path segments instead of the
fully-resolved, canonicalized path). A naive `strstr(path, "..")` check
is exactly the kind of scope-check-on-the-wrong-representation bug that
entry warns about — it's why the acceptance criteria specifically
demands URL-encoded and absolute-path variants, not just literal `../`.

## When done

Point me at the source + `git log`, with the path-traversal evidence
front and center. I will actively try to break the traversal protection
during review — treat this project as if it's genuinely going to be
attacked, because in spirit, that's exactly what Stage 13 will do to
servers like it.
