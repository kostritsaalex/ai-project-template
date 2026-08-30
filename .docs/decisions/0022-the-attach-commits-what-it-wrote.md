# 0022. The attach commits what it wrote

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

[`blueprints/setup/procedure.md`](../../blueprints/setup/procedure.md), the shared attach procedure.
**Nothing in it asks for a commit, and two live runs on 2026-08-30 did not make one.** On ArtGlina the
stubs were committed by hand afterwards, outside the procedure. On NorsePath, after the attach and
after both checks and a behaviour test, `git status --short` in the component still printed
`?? AGENTS.md` and `?? CLAUDE.md`. Recorded as defect 8 of the nine in
[`backlog.md`](../backlog.md), where the argument it depends on was already written: a
repository-backed component whose stubs are not committed gives a fresh clone no stubs at all, and an
assistant opening that clone knows nothing about the project it belongs to, which is the exact failure
this framework exists to prevent.

**The failure is invisible to everything the framework has.** `structure-check` and `registry-check`
both read the working tree, where an untracked file reads exactly like a committed one. Every row
passes on a component that a `git clean -fd` would strip of its identity, and passes again on a clone
that never had it.

**The blueprints already assume the commit that no step asks for.** `grep -rni 'commit' blueprints/`
returns four hits in this tree, one sentence repeated in each adoption README —
`component/README.md:114`, `project/README.md:152`, `assets/README.md:91`,
`repository/README.md:104` — *"Before committing, search for `<!--` and for `<` followed by a capital
letter."* Four documents name a commit as the thing the search precedes, and no procedure step names
it at all.

## Decision

**One instruction, in Step 8, after the placeholder search:**

> **Commit the files you wrote, and only those, in each folder you wrote into that is under version
> control.** A folder under none needs nothing here; an uncommitted stub is absent from a fresh clone
> and removed by a sweep of untracked files, and no check sees the difference, because a written file
> reads in the working tree exactly like a committed one.

**Step 8 and not Step 7, decided on the four READMEs.** Their shared sentence fixes an order — search,
then commit — and that search is Step 8's first instruction, so a commit written into Step 7 runs on
the wrong side of a precondition four shipped documents state. Two further reasons come out of the
procedure itself. Step 7 opens *"Skip this for a project scope, which has no parent"*, so an
instruction placed there is unreachable for a project adoption, which writes files into the same kind
of folder and leaves them untracked in the same way. And Step 7's *"A component is attached when both
halves are written"* is a definition; repairing the word *written* means editing what attachment
means, which is a larger change than the one this release makes.

**The session commits, rather than reporting that a commit is needed.** Step 8 already requires it to
*"say which files you wrote or changed"*, and both live runs produced that report while the stubs
stayed untracked in both. An instruction to report that the files are uncommitted is a weaker form of
one that exists and has already failed twice, and under
[`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md) it would not earn its line. The
objection is real and is answered by scope rather than by omission: a setup session should not start
making commits nobody asked for, and this one commits only the files it wrote itself, into folders it
was sent to write into. The clause *"and only those"* carries that limit and is the part under test.

**The condition is version control, not `git`, and its correct outcome in a folder under none is that
nothing happens.** [`0001`](0001-project-scope-need-not-be-a-repository.md) admits a project scope
that is not a repository, and [`0007`](0007-a-component-with-no-address-says-so.md) settles that local
version control and reachability are separate questions — *"What does not fix it: `git init`"*. The
instruction names no tool and no command, and it must not read as an argument for putting the folder
under version control, which is the project's decision and not the framework's.

## Consequences

**A setup session now writes to a history it did not write to before.** That is the cost, stated
plainly. It is bounded to the files the session wrote, and it is a smaller act than the writes it
already makes: the framework has been content to have an assistant create documents in a person's
folders since `0.1.0`, and this only makes those documents survive the next clone.

**The multiplication stays open and is not decided here.** Committed stubs travel with every clone,
so a second working copy carries a true-looking claim to be the component. That question — whether a
component is a folder or a repository — is recorded in `backlog.md` and is deliberately left where it
is. This decision does not settle it; it makes the branch the backlog already established as forced
into an instruction, and if the question is ever settled the other way, this is the line that changes.

**Nothing was removed in exchange, and principle 7 gets a number instead of a promise.**
`procedure.md` goes from 128 to 132 non-blank lines, 182 to 186 counting blanks. The step gained an
instruction it had been missing for its whole life and nothing in it became redundant, so there was
nothing to take out without repairing a second defect, which this release is not doing. The debt is
now four releases old, and the queued subtraction pass over `blueprints/` inherits four more lines
than it was promised.

**The eight other attach defects are untouched**, including the two adjacent to this one: the
competing four-step adoption procedure in `component/README.md`, which is where the commit sentence
already half lives, and the absence of any run log for an attach at all.

**Pre-registered in
[`attach-commits-what-it-wrote.md`](../predictions/attach-commits-what-it-wrote.md)** before the edit
existed: three arms, including a negative half with the instruction removed, and three controls not
derived from the hypothesis — a project scope in a folder with no version control, which must produce
no action and no confusion; a repository holding unrelated modified files, which tests *"and only
those"*; and a session that cannot run commands, which must not report a commit it did not make.

**It ships unrun, and that is the same defect as number 2 of the nine.** Every arm needs a fresh
session against a real or scratch scope, and the session that wrote the instruction cannot be one.
Principle 6 says an idea earns its place by being run, and this one has not yet. It is named here, in
the changelog and in the backlog rather than left to be noticed, and the arms stand registered against
the next attach. What justifies shipping ahead of the runs is that the defect it repairs has two live
instances and no check that can see either.

## Origin

Alex, 2026-08-30. The observation arrived with the instruction to repair it: two attaches, the
untracked stubs in both, and the three questions this record answers — which step, whether the session
commits or only reports, and wording that holds for a folder with no version control. The answers were
taken from the files named above rather than from the message, and the report that carried the
observation was explicit that they should be.
