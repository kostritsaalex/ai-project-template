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

One row per component per check, so a failure names which folder it is in. Check 7 is the exception
and takes a single row, because it audits your reading rather than any component.

Result is pass, fail, or n/a. Evidence is a filename with the folder it sits in, a line number, and
the quoted line. If you cannot quote it, write "no evidence" and mark the row fail, including when it
looks like it passed.
That applies to rows asking whether something is present. The paragraph below governs the rest.

A check that asks whether something is absent is evidenced by the search you ran and what it
returned, for example: listed the root of wp-themes, no PROJECT.md. A search that returns nothing is
a pass, and passing it needs no quote. When the search does return something, quote the first match
and mark the row fail.

Resolving a path is computing, not inferring. Where a row below tells you to resolve one, do it, and
give what it resolved to as part of the evidence.

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
   Unless this row confirmed the folder exists, rows 2 to 6 for that component are n/a and name this
   row as the reason. They are not failures: nothing is wrong with stubs nobody could read, and a
   folder that does not exist will satisfy an absence check for no useful reason.
2. That folder holds both stubs, AGENTS.md and CLAUDE.md. List the root-level filenames you found.
   This row is evidenced by that listing. Do not quote a line from inside the files: their contents
   are not what the row asks about.
3. Both stubs name this component, and the name matches its registry heading in PROJECT.md exactly.
   Quote the heading and the naming line from each stub. A difference in wording, case or spacing
   fails: the heading is what the registry is keyed on.
4. Both stubs give the parent address, and it points at this scope. Which comparison you make is
   settled by what the stubs carry, and the two are different questions rather than two ways of
   asking one.
   A relative address such as "../" is resolved from the component's folder and has to land on the
   folder you are running in. The comparison is against that folder and against no line of text.
   Quote the address from each stub, give the path it resolved to, and say that it is this folder.
   Do not cite this document's local path line for it: a local path is a hint about where the folder
   usually sits, and a verdict resting on a hint is the "no evidence" case wearing a quote.
   Any other address, a URL or a location in a synced store, is compared as text against the
   "Address:" line under where the project lives, character for character. Quote both. That line and
   not the local path beneath it, because they are different claims and only the first is the address
   every component copies.
   This is the row that catches a project scope that has moved and left its components pointing at
   where it used to be.
5. Overrides agree in both directions. If a stub names REPOSITORY.md or ASSETS.md, that file is
   present in the same folder. If such a file is present, both stubs name it. Either half alone
   fails, and say which half is missing. If no stub names one and none is present, this is n/a.
6. The component folder holds no file named PROJECT.md. Test for that one path and give the result
   as the evidence. Do not list the folder: the fact this row needs is whether one named file is
   there, and a listing buries it among everything else. A component holding a PROJECT.md is a
   project scope and has been set up as the wrong thing.
7. One row, not one per component. Put "(read set)" in the Component column. This row audits your
   own reading, so it covers every folder you opened and not only the ones a component sits in.
   List in the evidence every folder you opened, without exception, including this scope's own root
   and including any folder you opened and then found irrelevant. Classify each as exactly one of:
   this scope's own root, which is in the read set by the first instruction in this prompt and needs
   no registry line; a folder the registry named, quoted with the line that named it; or neither.
   One folder in the third class fails this row, and name it.
   List before you judge. A folder you opened and left off the list is the failure this row exists
   to catch and the one thing it cannot see.

After the table, write one line: "Failed rows: N", counting rows marked fail. Rows here are one per
component per check, so a count of checks would hide a component.

Write nothing else. No summary, no overall verdict, no recommendations, no reassurance.
```

---

## Reading the result

Check 1 is the one this check was written for. A component's local path sits in the registry, nothing
re-derives it, and it goes stale the moment somebody moves the folder. That happened to the
`WordPress 7 Engine`, whose registry block was still naming its old path when the move was noticed on
2026-08-29.

No check caught it, and no check could have. `structure-check` had passed that block twice, but on
2026-08-25, when the path it named was still correct; it was not passing a stale path, and it cannot
read one, because it may not look outside the folder it audits. Between the move and the discovery no
check ran at all, and none existed that would have helped. That gap is what this file is for.

Check 4 fails in the direction that costs most. A component pointing at where its scope used to be
passes `structure-check` 8, which confirms the shape of an address and is forbidden from resolving
it, and passes the cold start check, which asks for the address to be repeated. It fails here, and
otherwise fails only when somebody follows it.

Check 5 catches the half-done override. Removing `REPOSITORY.md` while the stubs still name it, or
the reverse, leaves a component that reads as having rules it does not have; an assistant opening it
reports a missing file instead of doing the work. Add and remove an override as one operation.

Check 6 asks for one fact and takes one probe. It used to ask for a listing, and it was the least
stable row in the check: it flipped between fail and pass in two independent experiments, once
between a run and its own control on an unchanged scope, once between the two negative runs, and it
is why one negative run counted six failures and the other five. Two of the three causes were fixed
elsewhere, by restoring the absence half of the evidence rule and by making unevaluable rows n/a. The
third was the row itself, asking for a full listing when the only fact it needs is whether one named
file is present, and offering that listing as the place for a verdict to come from.

Check 7 audits the check itself. A tool that read something outside the declared set has broken the
rule the whole method rests on, and a table that fails it should not be trusted on any other row.

Its first version was wrong, and wrong in the direction that matters. It asked for a registry line
naming every folder read, and the scope's own root is not named by any registry line, so read
literally it failed every correct project. The run did not fail it: the tool found the scope's local
path line elsewhere in `PROJECT.md` and offered that as the naming line, which is a repair rather
than an answer. A row a tool has to repair to pass is a row that was not asking what it meant.

Its second version was wrong too, in a way the run could not have shown. Putting the scope root into
the read set closed the case the run exposed and left the class open: while the row was keyed to a
component, a folder belonging to no component had nowhere to appear, so `.docs/`, a subfolder of the
scope, or a stray directory could be read and never be listed. The row is now a single one covering
everything read, which is what it always meant.

The last line counts rows rather than checks. With one row per component per check, a count of
checks hides which component failed, and the first run made the ambiguity visible by answering
"Failed checks: 3" for two failing checks across three rows.

---

## What this check cannot see

**A green table can mean nothing was audited.** A component the registry never claimed is on this
machine, one addressed by a URL or a synced store with no reachable folder, is `n/a` on every row.
That is correct: nothing about it can be read from here, and reporting a failure would call a
perfectly good component broken. But the count at the bottom counts failures, so a project whose
components all sit elsewhere produces a table of `n/a` and `Failed rows: 0`, which looks exactly like
a project that passed. Read the table, not the count. If no row says `pass`, nothing was checked.

Whether the registry is right. It compares two documents and reports where they disagree; it has no
way to know that a component was given the wrong posture, or that a block describes a folder nobody
uses any more.

Anything not reachable from the registry. Two documents inside one scope contradicting each other,
or a document's claim about its own files, is outside the read set by construction, and no check
built under `0009` will find it. That is a different shape with a different instrument, and today the
instrument is somebody reading.
