# Registry Check

Run this from the project scope, after the components it declares have been attached.

It is the only check that reads two scopes. `structure-check` audits one folder and cannot see the
registry that lists it; the cold start check starts in one folder and never resolves what it quotes.
Between them, a component whose folder has moved, whose name no longer matches its registry heading,
or whose stubs point at a parent that has moved, passes everything.

Its read set is declared in advance and is the reason it is allowed to read more than one folder. See
[decision 0009](../../.docs/decisions/0009-a-check-declares-its-read-set-in-advance.md).

---

## How to run

1. Open the project scope, the folder holding `PROJECT.md`.
2. Start the session on the side of any filesystem boundary that reaches every component. This is
   the only check with that precondition, and it is what the session note in `PROJECT.md` exists to
   answer. Where the project sits in one filesystem, there is nothing to do.
3. Copy the prompt below from this file's raw text rather than from a rendered view.
4. Paste it. There is nothing to fill in.
5. Read the table. Fix what failed, then run it again.

---

## Prompt

```text
You are auditing a project scope against the components its registry declares.

Read PROJECT.md in the folder you have open. From its components registry, work out the location of
each declared component, and read the root-level Markdown files of each: AGENTS.md, CLAUDE.md, and
REPOSITORY.md or ASSETS.md if present.

That is your entire read set: this folder's own root, and the root of each folder the registry names.
Do not descend into subfolders. Do not read a component's contents. Do not follow a component's
parent address anywhere. If the registry names no components, every check below is n/a and you say
so in one line.

Do not modify any file.

Answer with one table and nothing else. Columns: Check, Component, Result, Evidence.

One row per component per check, so a failure names which folder it is in. Result is pass, fail, or
n/a. Evidence is a filename with the folder it sits in, a line number, and the quoted line. If you
cannot quote it, write "no evidence" and mark the check fail, including when it looks like it
passed.

Do not infer, do not assume, do not fill a gap from what such a document usually contains. Where two
documents disagree, both are quoted and the row fails; it is not your job to decide which is right.

Checks:

1. The component's folder exists where the registry says. Say which line you used to locate it: the
   address when it is a relative path, otherwise the local path line beneath it. Quote that line and
   say whether the folder is there. A folder that is not there fails, unless PROJECT.md says in
   visible text that this component is not attached yet, which is n/a.
   A component whose address is a URL or a synced-store location, with no local path line and no
   folder you can reach, is n/a rather than a failure: nothing in the registry claimed it was on this
   machine.
2. That folder holds both stubs, AGENTS.md and CLAUDE.md. List the root-level filenames you found.
3. Both stubs name this component, and the name matches its registry heading in PROJECT.md exactly.
   Quote the heading and the naming line from each stub. A difference in wording, case or spacing
   fails: the heading is what the registry is keyed on.
4. Both stubs give the parent address, and it matches the address PROJECT.md gives for itself under
   where the project lives. Quote both. This is the row that catches a project scope that has moved
   and left its components pointing at where it used to be.
5. Overrides agree in both directions. If a stub names REPOSITORY.md or ASSETS.md, that file is
   present in the same folder. If such a file is present, both stubs name it. Either half alone
   fails, and say which half is missing. If no stub names one and none is present, this is n/a.
6. The component folder holds no PROJECT.md. A component holding one is a project scope and has been
   set up as the wrong thing.
7. Every folder you opened is one the registry named. List the folders you read, and PROJECT.md's
   line that named each. A folder you read that no line named fails this check.

After the table, write one line: "Failed checks: N".

Write nothing else. No summary, no overall verdict, no recommendations, no reassurance.
```

---

## Reading the result

Check 1 is the one this check was written for. A component's local path sits in the registry, nothing
re-derives it, and it goes stale the moment somebody moves the folder. That happened on 2026-08-29:
the `WordPress 7 Engine` moved and its registry block was still naming the old path, which
`structure-check` passed twice because the path is well formed and check 12 only asks what form it is
written in.

Check 4 fails in the direction that costs most. A component pointing at where its scope used to be
passes `structure-check` 8, which confirms the shape of an address and is forbidden from resolving
it, and passes the cold start check, which asks for the address to be repeated. It fails here, and
otherwise fails only when somebody follows it.

Check 5 catches the half-done override. Removing `REPOSITORY.md` while the stubs still name it, or
the reverse, leaves a component that reads as having rules it does not have; an assistant opening it
reports a missing file instead of doing the work. Add and remove an override as one operation.

Check 7 audits the check itself. A tool that read something outside the declared set has broken the
rule the whole method rests on, and a table that fails check 7 should not be trusted on any other
row.

---

## What this check cannot see

Whether the registry is right. It compares two documents and reports where they disagree; it has no
way to know that a component was given the wrong posture, or that a block describes a folder nobody
uses any more.

Anything not reachable from the registry. Two documents inside one scope contradicting each other,
or a document's claim about its own files, is outside the read set by construction, and no check
built under `0009` will find it. That is a different shape with a different instrument, and today the
instrument is somebody reading.
