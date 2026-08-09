# Structure Check

Run this after adopting any blueprint, once the files are in place and filled in.

It checks the mechanics: leftovers, addresses, adapter wiring. It says nothing about whether an
assistant will actually pick up the context. That is what the [cold start check](cold-start-check.md)
is for.

Any AI tool with access to the folder will do. The session that performed the adoption is fine here.

---

## How to run

1. Open the folder where the adopted files live.
2. Paste the prompt below, replacing `<ENTRY_POINT>` with the canonical entry point's filename:
   `REPOSITORY.md` for the Repository Blueprint, `ASSETS.md` for the Assets Blueprint.
3. Read the table. Fix what failed, then run it again.

---

## Prompt

```text
You are auditing a folder where a document template has just been filled in.

The canonical entry point of this folder is <ENTRY_POINT>.

Read the files in the folder root: <ENTRY_POINT>, AGENTS.md, CLAUDE.md, and README.md if present.
Do not read anything else. Do not modify any file.

Answer with one table and nothing else. Columns: Check, Result, Evidence.

Result is pass, fail, or n/a.

Evidence is a filename, a line number, and the quoted line. A check without evidence is a failed
check, including one that looks like it passed: if you cannot quote anything, write "no evidence"
and mark it fail. Do not infer, do not assume, do not fill gaps from what such a document usually
contains.

Checks:

1. No HTML comment remains in any file. Quote the first one you find.
2. No unfilled placeholder remains, meaning a token in angle brackets written in capitals. Quote
   each one.
3. No file still carries the template notice at the top.
4. AGENTS.md and CLAUDE.md each point to <ENTRY_POINT> by name, and carry no instructions of their
   own beyond that redirect. Quote the pointing line from each.
5. Exactly one file in this folder declares itself a canonical entry point. Name it.
6. No file is named after a different scope's entry point. List every filename in the folder root.
7. The parent project's repository is given as a full URL including the scheme. Quote it.
8. Any local checkout path is written relative to the home folder, starting with ~/ , with no
   username after the tilde. Absolute paths such as /home/name/... or C:\Users\name\... fail this
   check. Quote the path.
9. The document states both when parent project context is required and when it is not. Quote both
   halves separately.
10. The document states what to do when parent project context is required but unreachable. Quote
    it.
11. Every file or folder path the document refers to either exists, or the document says in visible
    text that it does not exist yet. List each referenced path with which of the two applies.

After the table, write one line: "Failed checks: N".

Write nothing else. No summary, no overall verdict, no recommendations, no reassurance.
```

---

## Reading the result

A failed check is a fact, not an opinion, because every row carries a quote you can open and verify
yourself.

Two rows are worth extra attention:

Check 8 fails quietly. A path with a username in it works on the machine where it was written and
nowhere else, so nothing looks broken until someone else opens the repository.

Check 11 catches the common case of a `.docs/` list copied from the blueprint and never adapted. The
assistant then reports missing files as if something were wrong.

If the audit returns advice or a verdict despite the last line of the prompt, the tool is padding.
Judge the table, not the commentary.
