# 0005. The registry carries the component

**Date:** 2026-08-23  
**Status:** accepted

---

## Context

[Decision 0004](0004-documents-carry-what-cannot-be-seen.md) cut every document to what an assistant
cannot see for itself. It worked on the contents of the documents and left their number alone. A
component still shipped three files: an entry point of 25 to 30 lines, and two adapters pointing at
it.

The owner asked what was actually in that entry point. Read against the same test, it holds four
things:

- The address of the parent. One line.
- The escalation boundary, saying when to go up and read it.
- `Local rules`, which the blueprints themselves describe as usually empty.
- `Hazards`, which the blueprints describe as usually deleted.

Three of the four are generic. Only `Local rules` is particular to the folder, and it is the one the
blueprints expect to be empty.

Checked against the only project that has run long enough to show wear, ArtGlina: of three
components, one carries genuine local rules, the platform conventions for a WordPress site. One
carries the four preserve rules, which are not particular to it at all; every component that keeps
material rather than changes it needs the same four. The third carries nothing.

So the entry point exists in most components to hold one line of address and a rule that follows
from a single word.

## Decision

**The registry carries the component. The component carries two stubs.**

A registry block gains one line, the posture of the folder:

```text
## Northwind Brand Assets

Assets. Do not reorganize, rename or move anything here. Preserve the existing organization.
Address: assets/brand
```

`Repository` means an assistant will mostly change things there. `Assets` means it will mostly find
them and leave them alone, and the preserve rules travel with the word rather than with the folder.

`AGENTS.md` and `CLAUDE.md` become the whole of a component. They name which component the folder is,
carry the parent's address, and stop. They are identical apart from the heading.

**A folder that has not been declared a component is not one.** It is files, belonging to whichever
component contains it and taking that component's posture. Being a component is a decision written
into the registry rather than a property of what sits on disk.

This was added the same day, after a setup run stopped to ask whether a folder of themes was one
component or one per theme. The question has no answer that can be read off the disk, and it arrives
once per nested folder. The rule removes it: none of them, until somebody says otherwise.

`REPOSITORY.md` and `ASSETS.md` survive as the override, for a folder that has a rule of its own.
They lose the parent address, the escalation boundary and `Parent checked`, and keep only
`Local rules` and `Hazards`. Where an override and the registry disagree, the registry is right.

## Consequences

A component falls from three files to two, and from 32 lines shipped to 22. The larger change is
that none of the 22 is a decision: two lines are the parent address and the rest are fixed text. The
component interview falls to three questions, one of which is the name.

Adding, renaming or moving a component becomes one edit in one file.

The escalation boundary is removed rather than relocated. It existed so a component would not walk up
to a long parent document without cause, and the parent is now 33 lines. Reading it every time costs
nothing, so there is no boundary left to draw.

`Parent checked` goes with the file that held it. A component holds no copy of anything in the parent
except the address, so nothing it holds can fall out of date on its own.

The `@` import in `CLAUDE.md` is restricted to a file in the same folder. Pointed at a parent across
a mount boundary it would state the parent's location a second time, in a second format, and its
documented failure mode is silent: an import outside the working directory asks for approval once,
and a declined approval disables it permanently without saying so again.

**The accepted cost.** A component that cannot reach its parent now knows nothing at all: no
principles, no posture, no preserve rules. Copying the posture down into the stub was rejected
because it puts one rule in two places, and two copies drift. Instead the stub is told to fail
loudly: an assistant that cannot reach `PROJECT.md` says so and stops.

This failure is not hypothetical. Reaching a component inside a Linux environment on a Windows
machine has broken twice in practice, and each time the fix was to start the session on the other
side of the boundary.

Two risks are accepted without a mitigation, because neither is a mechanism.

The registry can regrow. Adding a line to an open file has always been cheaper than creating one, so
rules that would never have justified a file will be tempting to write there. The registry is read by
everyone, so a line put in it is paid for by every reader. The guard is a rule and not a check:
whatever is needed to reach a component belongs in the registry, whatever is needed to work inside
one belongs in the component.

And a rule can now be written in two places, the registry or an override. Nothing detects a
disagreement between them. `structure-check` gains a check that an override states no posture, which
catches the common case and not the general one.

## Origin

Alex, 2026-08-23, in a single sentence: what is needed is a registry of a project's components, one
`PROJECT.md` in the main folder, and nothing told to the components themselves.

A second proposal in the same conversation was rejected: giving every folder its own `PROJECT.md`
with no central file. With N components and no centre, each folder has to know the other N minus one,
so adding a component becomes N edits and renaming a folder becomes N edits. A registry distributed
across every folder is not a registry.
