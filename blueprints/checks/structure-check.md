# Structure Check

Run this after adopting any blueprint, once the files are in place and filled in.

It checks the mechanics: leftovers, addresses, stub wiring. It says nothing about whether an
assistant will actually pick up the context. That is what the [cold start check](cold-start-check.md)
is for.

Any AI tool with access to the folder will do. The session that performed the adoption is fine here.

---

## How to run

1. Open the folder where the adopted files live.
2. Copy the prompt below from this file's raw text rather than from a rendered view. A rendered view
   eats angle brackets and backslashes, and the prompt contains both.
3. Paste it. There is one thing to fill in, on its second line: whether this folder is a project
   scope or a component.
4. Read the table. Fix what failed, then run it again.

The prompt carries everything else it needs, including what to skip in each case. Nothing on this
page has to be open while it runs.

---

## Prompt

```text
You are auditing a folder where a document template has just been filled in.

This folder is: A PROJECT SCOPE | A COMPONENT
Delete the one that does not apply before answering.

A project scope holds PROJECT.md and two stub files, AGENTS.md and CLAUDE.md.
A component holds two stub files and nothing else, unless it has rules of its own, in which case it
also holds REPOSITORY.md or ASSETS.md.

Read the files in the folder root: PROJECT.md, REPOSITORY.md or ASSETS.md if present, AGENTS.md,
CLAUDE.md, and README.md if present. Do not read anything else. Do not modify any file.

Answer with one table and nothing else. Columns: Check, Result, Evidence.

Result is pass, fail, or n/a. Where a check says it applies to only one of the two cases, n/a is the
correct answer in the other, not a failure.

Evidence depends on what the check asks.

A check that asks whether something is present is evidenced by a filename, a line number, and the
quoted line. If you cannot quote it, write "no evidence" and mark the check fail, including when it
looks like it passed.

A check that asks whether something is absent is evidenced by the search you ran and what it
returned, for example: searched AGENTS.md, CLAUDE.md for an HTML comment opener, no match. A search
that returns nothing is a pass, and passing it needs no quote. When the search does return
something, quote the first match and mark the check fail.

Do not infer, do not assume, do not fill gaps from what such a document usually contains.

Checks:

1. No HTML comment remains in any file. Search for the opening sequence of an HTML comment.
2. No unfilled placeholder remains. A placeholder is a run of capital letters and underscores
   wrapped in angle brackets. Quote each one you find.
3. No file still carries the blueprint notice. That notice begins with the words "BLUEPRINT FILE.
   NOT ACTIVE INSTRUCTIONS." A document's own header, such as a line reading "AI Project Entry
   Point" or "Local rules for this component", is not that notice and does not fail this check.
4. AGENTS.md and CLAUDE.md carry the same text, apart from their first heading, apart from any line
   beginning with the at sign, and ignoring blank lines. Report any other difference and fail the
   check if there is one.
5. Project scope only. PROJECT.md is present, and neither REPOSITORY.md nor ASSETS.md is in this
   root. List every filename in the folder root.
6. Component only. PROJECT.md is not in this folder. A component that holds one is a project scope
   and has been set up as the wrong thing. List every filename in the folder root.
7. Component only. Both stubs name which component this folder is, and both name the same one.
   Quote the naming line from each.
8. Component only. Both stubs give the parent as an address that resolves from outside this machine.
   A full URL including the scheme, an account-relative location in a synced store such as
   "OneDrive, Projects/Northwind", and a relative path to a containing folder all pass. A bare local
   path fails. Quote it from each file.
9. Component only. Both stubs say what to do when the parent cannot be reached. Quote it.
10. Component only. If REPOSITORY.md or ASSETS.md is present, both stubs point at it by name, and
    that file carries no parent address and does not state the folder's posture. Both of those
    belong to the parent. A sentence saying where the posture is stated does not fail this check; a
    sentence stating it does. If neither file is present, this check is n/a.
11. Project scope only. Every block in the components registry carries a name, the word Repository
    or the word Assets, and an address. Name any block missing one of the three. A block whose word
    is Repository also carries the rule that travels with it, that platform or framework core
    changes only through its own update mechanism and never by hand; quote it or fail the block.
    The address says where that component is, read from this document, and it takes one of four
    forms. A full URL including the scheme. An account-relative location in a synced store, such as
    "OneDrive, Projects/Northwind". A relative path into a folder this document's folder contains.
    Or a plain statement that no address exists, together with the reason, such as "none. No copy of
    this folder exists off this machine." Anything else fails, and a bare local path such as
    "~/wordpress-7" written into the address is the case worth catching: it reads as an address,
    resolves nowhere off this machine, and gives no sign that there was never anything to follow.
    A block whose address is ".." or "../" fails too: that points out of this folder rather than into
    the component, and it is the address the component writes in its own stubs to point back here.
    A local path may sit on its own line beneath the address, and belongs there rather than in it.
    A registry holding no blocks at all is not a failure and is not n/a. It passes when the document
    says in visible text that no components are declared; quote that sentence. It fails when there
    are no blocks and no such sentence.
12. Any local path is written relative to the home folder, starting with ~/ , with no username after
    the tilde. Absolute paths such as /home/name/... or C:\Users\name\... fail this check. Quote the
    path. One exception: a command that creates a symlink so a ~/ path resolves across a mount
    boundary has to name the absolute source, so a line such as
    "ln -s /mnt/c/Users/alex/OneDrive ~/OneDrive" passes, and so does the mount location named in the
    sentence that explains it.
13. This check covers the locations inside this scope that the documents point to: a documentation
    folder, a decisions folder, a subfolder holding a component, any other file or folder they say
    is here. Each one either exists, or the document says in visible text that it does not exist
    yet. List each with which of the two applies.
    Four things are outside this check and must not be listed. A filename given as an example of a
    naming convention rather than as a location. A location belonging to another scope, including a
    component's own local path written in the registry, which resolves on the machine and in the
    environment that component lives in rather than this one. A path appearing only inside a symlink
    command or the sentence explaining it. Anything that is a URL rather than a path.

14. Project scope only. If the document says what makes its local path true, it names both things
    that take: the arrangement holding the path up, a symlink or a mount, and the command that
    creates it on a machine that lacks it. Quote both. This is checked whether or not the document
    also says where to start a session. Those are two separate lines answering different questions,
    and a project living in one folder reached through a mount needs the first without the second.
    If the document says nothing about what holds its local path up, this check is n/a.

After the table, write one line: "Failed checks: N".

Write nothing else. No summary, no overall verdict, no recommendations, no reassurance.
```

---

## Reading the result

A failed check should be a fact rather than an opinion. A presence check carries a quote you can
open. An absence check carries a search you can run yourself.

Four rows are worth extra attention:

Check 4 is new in `0.5.0`. The two stubs are one text under two filenames, and nothing stops someone
editing one and forgetting the other. A difference between them is a rule that fires for one tool and
not another.

Its first run produced a false positive. `CLAUDE.md` carried a sentence introducing the import, which
is a real difference and an intended one, so the check failed a correct document. The sentence was
removed rather than the check widened: whether a tool supports the import is a property of the tool,
and the import fails silently anyway, so the warning bought nothing.

Check 10 catches the override drifting back into an entry point. `REPOSITORY.md` and `ASSETS.md`
used to carry the parent address and the posture of the folder. Both moved out, and a file that has
picked them up again is stating something the registry also states. The line between the two cases
is worth holding: "how this folder is to be treated is in `PROJECT.md`" points, and passes.
"Things get changed here" states, and fails.

Check 11 catches four things. A block written without a posture leaves a folder with no rules at
all, since that word is the only thing the component is ever told about itself. A `Repository` block
written without the rule about platform core leaves the word carrying nothing, because since `0.6.0`
that rule is the entire difference between the two words. A block addressed `../` sends a reader out
of the project instead of into the component: the two directions carry different values, and the one
belonging in the component's stubs was written here by mistake.

And since `0.7.0` it knows what an address is. It used to ask for one without saying what made one
valid, which let a machine-local path into the slot and certified it as a pass. Attaching the same
component twice produced two different inventions for a folder that has no address at all, and the
worse of the two read as an address and resolved nowhere. See
[decision 0007](../../.docs/decisions/0007-a-component-with-no-address-says-so.md).

Check 14 is the one that fails on a machine other than the one it was written on. A `~/` path under a
synced store, read from another filesystem, resolves because somebody made a symlink once. Nothing in
any file records that, so a document naming the path and not the arrangement is true where it was
written and false everywhere else. This was observed twice: one setup run volunteered the symlink
line, the next did not, from the same blueprint.

Until `0.6.0` the check was gated on the session note, and so it never ran: the first scope that
carried a symlink line had no components yet, no boundary to cross and no session note, and the one
line holding its path up went unverified. The two are separate questions and the check now follows
the path note alone.

Check 12 fails quietly in the other direction. A path with a username in it works on the machine
where it was written and nowhere else, so nothing looks broken until someone else opens the
repository.

If the audit returns advice or a verdict despite the last line of the prompt, the tool is padding.
Judge the table, not the commentary.

---

## Declared limits

**Row 14 cannot tell correct silence from wrong silence.** A document that says nothing about what
holds its local path up is `n/a`, whether it correctly needs no path note or needs one and lacks it.
The framework's own `PROJECT.md` carried that second case on 2026-08-25 and this row passed it.

The remedy exists and was rejected with its cost stated, in
[decision 0010](../../.docs/decisions/0010-the-path-note-stays-optional.md): requiring every document
that gives a local path to say either what holds it up or that nothing does would land a sentence on
the majority of projects, which live in one filesystem, to serve the few that span a boundary. This
is a limit rather than a defect, and it is written down so the two are not confused from outside.

---

## What this check cannot see

An address that is well formed and wrong. The prompt forbids reading anything outside the folder, so
check 8 confirms the shape of a parent address and never resolves it. A component left pointing where
its project scope used to be passes here, and fails only when somebody follows the address.

It also cannot see whether the parent still lists this component, or lists it under this name.
Nothing in this folder knows what the parent holds. A folder that appears in no registry is not a
component at all, by the rule in
[decision 0005](../../.docs/decisions/0005-the-registry-carries-the-component.md), so what is
missing is a check that walks the registry and opens each component's stubs from there.
