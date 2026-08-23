# 0004. Documents carry what cannot be seen

**Date:** 2026-08-23  
**Status:** accepted

---

## Context

[Decision 0003](0003-cut-the-framework-to-four-jobs.md) cut the framework to four jobs and removed a
third of the text that ships into an adopted project. It was not enough. Setting up a project still
took an interview long enough to exhaust its owner, and the questions that tired him were the ones he
could see no point in: which platform, what the local environment is, whether deployment belongs
here, what the folder contains.

The four jobs turned out to be a description of the answer rather than a rule for finding it. Asked
to justify a section, the reply was always "job two" or "job four", which is a category and not a
test.

The rule that does work came from the owner in one sentence: an assistant should not care what is in
the folder. It is told where the principles are and where the main folder is, and it looks at
everything else itself.

## Decision

**A document carries what cannot be seen, and nothing that can.**

An assistant opens the folder and looks. The platform, the local URL, the file layout, the installed
tooling, whether a `.git` exists, what the folder holds: all visible, none of it belongs in a
document, and none of it is worth a question during setup.

What survives the test is what no amount of looking reveals:

- **The registry.** A folder does not know its siblings exist. This is the feature the framework is
  for: working in one folder, an assistant reads the registry and reaches another that may sit on a
  different disk or in a different filesystem.
- **The address of the parent, and when to go to it.** A folder does not know it is part of something.
- **The owner's principles.**
- **What the project does not do.** The only rule in the framework with a measured before and after.
- **Hazards**, narrowly: a shared remote, a folder that syncs elsewhere, credentials that reach
  production. Almost always empty.
- **Where to start a session**, when components sit on different sides of a mount boundary.

Applied, this removes from the shipped documents: every description of contents, the platform and
environment block, the registry's platform and production fields, `Scope Ownership`, `Workstreams`,
the separate `Project Overview` and `Project Scope` sections, and the `.docs/` inventory.

A component's own rules become one free section it may leave empty.

## Consequences

The text that ships into an adopted project falls from 166 lines to 88, and from 272 before the first
cut. A component entry point is 25 lines. The setup procedure falls from 320 lines to 145, because an
interview cannot be longer than the fields it fills.

Two things get worse. A registry entry no longer says what platform a component runs on, so anyone
who wants that opens the component. And a document that describes nothing is harder to skim for a
human, who cannot run `ls` while reading it on a phone. Both were accepted: the framework is for the
assistant, and the assistant can look.

The version counters removed in `0.3.0` stay removed. `Parent checked` remains a date.

Decision 0003 stands as the record of the first cut. Its four jobs are superseded by the single test
above.

## Origin

Alex, 2026-08-22 into 2026-08-23, after setting up the same project three times and losing patience
with the interview. The formulation is his; the assistant had spent the week defending sections that
this test deletes.
