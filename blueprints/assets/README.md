# Assets Override Blueprint

The optional third file for an `Assets` component, when that folder has rules of its own.

**Blueprint Version:** 0.6.0  
**Framework Version:** 0.9.3  
**Status:** in use in one project. Demoted in `0.5.0` from the normal way to attach a component to
the exception.

---

## When you need this

You do not need it to attach a folder of photography, brand files, contracts or the working material
of a workstream. [`../component/`](../component/) does that with two stubs, and the parent registry
entry carries the word `Assets`, which adds nothing to the project's principles: the folder is live
and the task governs what happens in it.

You need this file when something here has to be held still. An arrangement that must not be
rearranged, a naming scheme that has to be followed, a tool that owns part of the folder, a
subfolder that is worked code rather than stored material.

If you cannot name such a thing, do not create the file.

---

## Files

| File | Role |
| --- | --- |
| `ASSETS.md` | This folder's own rules. Not an entry point. |
| `AGENTS.md` | The component stub, plus one line sending the reader to `ASSETS.md`. |
| `CLAUDE.md` | The same, and it imports `ASSETS.md`, which is safe because the file is adjacent. |

Copy all three into the component. Do not copy this `README.md`.

---

## What happened to the preserve rules

Until `0.6.0` the word `Assets` carried four of them: do not reorganize, do not rename, do not move,
preserve the existing organization. They are gone.
[Decision 0006](../../.docs/decisions/0006-the-postures-carry-one-rule-between-them.md) records why.
An assets folder is live: material arrives and gets updated, and a rule that ordinary work breaks
every day teaches an assistant that the document can be ignored.

The registry block is now this much:

```text
## Northwind Brand Assets

Assets. Live material. Work here as the task requires.
Address: assets/brand
```

The cost is accepted and named in that decision. Nothing stops an assistant rearranging a folder on
its own initiative any more. This file is where that gets fixed for a folder that actually needs it,
and it is the first real case the override has had.

---

## Placeholders

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<COMPONENT_NAME>` | Name of this component. Must match its heading in the parent registry. | `Northwind Brand Assets` |
| `<LOCAL_RULES>` | Whatever has to be held still in this folder. | `Do not rearrange this folder. The layout mirrors the photographer's own catalogue.` |
| `<HAZARDS>` | Only what an assistant cannot find by looking. Usually empty; delete the section then. | `This folder syncs to a second machine; a file edited on both comes back as a conflicted copy.` |
| `<ASSETS_BLUEPRINT_VERSION>` | Blueprint version this file started from. | `0.6.0` |
| `<YYYY-MM-DD>` | Date. | `2026-08-23` |
| `<DOCUMENT_OWNER>` | Person responsible for this document. | `Alex` |

---

## What does not go in

The posture of the folder, which is in the registry. Anything true of the project rather than this
folder, which is in `PROJECT.md`. A description of the contents, which an assistant can see.

---

## How to adopt

1. Attach the component first, following [`../component/`](../component/).
2. Copy `ASSETS.md` into the component and delete the blueprint notice.
3. Write the exception in `Local rules`.
4. Fill `Hazards`, or delete the section.
5. Replace the stubs with the ones from this folder, which add the line pointing here.
6. Delete every remaining comment.

Before committing, search for `<!--` and for `<` followed by a capital letter.

---

## Verify the adoption

[Structure check](../checks/structure-check.md), then
[cold start check](../checks/cold-start-check.md) in a new session, using its component prompt.
