# 0009. A check declares its read set in advance

**Date:** 2026-08-29  
**Status:** accepted

---

## Context

`structure-check` may not read outside the folder it audits. The prompt says so, and the constraint
does real work: every row's evidence is a filename, a line number and a quoted line the person
running it can open, and the set of files that could possibly be read is known before the check
starts. Neither property is decoration. A check that wanders produces evidence nobody can verify, and
a check whose scope depends on what it finds cannot be reasoned about at all.

That constraint is also why three of the four instances of the stale-derived-fact class cannot be
caught. Each is a claim about somewhere else, and the check is forbidden from looking there.

The third check has been on the backlog since `0.6.0` for exactly this reason: walk the registry from
`PROJECT.md`, open each declared component's stubs, and compare what they say against the block that
declares them. It cannot be written without reading more than one folder.

So the question is what the constraint actually protects. If it protects "one folder", the third
check breaks it and needs an exception. If it protects something else, the third check may not break
it at all.

## Decision

**A check declares its read set in advance, and that set must be computable from documents before any
file is opened.**

That is the rule the one-folder constraint was a special case of. `structure-check` declares a read
set of one folder's root. The third check declares the scope's own root plus the root of every folder
the registry names, which is enumerable from a single document before any component is opened, and
finite for the same reason.

This is **a second bounded scope, not an exception.** The distinction matters, because an exception
invites the next one and gives no way to judge it: the third exception would be argued on its merits
like the first two, and eventually a check reads whatever it likes. A rule about read sets can be
applied to a check nobody has written yet.

What the third check's read set does **not** include, and what no check may do:

- **Subfolders.** Root-level files only, in each folder named.
- **A component's contents.** The check compares documents. What is in the folder is the posture's
  business and `0004` already forbids describing it.
- **Following an address outward.** A component's stubs give the parent's address, and that address
  resolves anywhere, which is precisely why it cannot be followed: the read set would stop being
  computable and stop being finite. The walk goes registry to component and never the reverse. A
  check therefore runs from the project scope, not from a component.

## Consequences

**The one-folder rule stays exactly as it is for `structure-check`,** which is unchanged by this. Its
read set was already declared; this record only says what kind of thing that declaration is.

**A check can now report a failure in a folder the person running it was not thinking about.** Every
row must name which folder its evidence came from, or the table becomes unreadable the moment two
folders are in it.

**The read set is computed from the registry, so a wrong registry produces a wrong read set.** A
block whose declared location holds nothing yields "no folder at the declared location", which is not
a failure of the method but the single most valuable row the check can produce. That is the stale
path from 2026-08-29, and it is the reason the check exists.

**The accepted cost.** A check reading two folders can no longer be run by pasting a prompt into a
session that happens to be open in the component, which is how the other two checks are used. It has
to run from the scope, on the side of any filesystem boundary that reaches every component, which
makes it the first check with a precondition the session note has to satisfy. Projects in one
filesystem never notice; the one project that spans a boundary already carries the note.

**What this does not fix.** The read set is bounded by the registry, so this rule reaches only facts a
registry can lead to. Two documents in one repository contradicting each other, or a document's claim
about its own repository's files, are outside every read set a registry can compute, and no check
built under this rule will find them. The backlog carries those separately, as the second shape of
the class, and the instrument for them is a person or a session reading.

## Origin

Alex, 2026-08-29, on being asked to write the third check and stopping to ask whether it broke the
constraint that makes the other checks trustworthy.

The framing is his: a registry walk reads more than one folder but not arbitrarily, and the question
is whether that is a second bounded scope or a real exception. Naming it the former is what turns a
one-off permission into a rule that governs checks nobody has written yet.
