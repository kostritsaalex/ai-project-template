# Assets Override Blueprint

The optional third file for a component where things get kept, when that folder has rules of its
own.

**Blueprint Version:** 0.5.0  
**Framework Version:** 0.5.0  
**Status:** in use in one project. Demoted in `0.5.0` from the normal way to attach a component to
the exception.

---

## When you need this

You do not need it to attach a folder of photography, brand files, contracts or the working material
of a workstream. [`../component/`](../component/) does that with two stubs, and the parent registry
entry carries the word `Assets` together with the preserve rules that follow from it.

You need this file for the exception: a subfolder that is worked code rather than stored material, a
naming scheme that has to be followed, a tool that owns part of the folder.

If you cannot name such an exception, do not create the file.

---

## Files

| File | Role |
| --- | --- |
| `ASSETS.md` | This folder's own rules. Not an entry point. |
| `AGENTS.md` | The component stub, plus one line sending the reader to `ASSETS.md`. |
| `CLAUDE.md` | The same, and it imports `ASSETS.md`, which is safe because the file is adjacent. |

Copy all three into the component. Do not copy this `README.md`.

---

## Where the preserve rules went

Into the parent registry, next to the word `Assets`:

```text
## Northwind Brand Assets

Assets. Do not reorganize, rename or move anything here. Preserve the existing organization.
Address: assets/brand
```

Every component that keeps things needs the same four rules, so they follow from the posture rather
than from the folder. Writing them once in the registry and never in the component removes the one
place they could drift.

The cost is accepted and named in [`../component/`](../component/): a component cut off from its
parent no longer carries them.

---

## Placeholders

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<COMPONENT_NAME>` | Name of this component. Must match its heading in the parent registry. | `Northwind Brand Assets` |
| `<LOCAL_RULES>` | The exception this folder needs beyond the preserve rules. | `The scripts/ folder is worked code rather than stored material.` |
| `<HAZARDS>` | Only what an assistant cannot find by looking. Usually empty; delete the section then. | `This folder syncs to a second machine; a file edited on both comes back as a conflicted copy.` |
| `<ASSETS_BLUEPRINT_VERSION>` | Blueprint version this file started from. | `0.5.0` |
| `<YYYY-MM-DD>` | Date. | `2026-08-23` |
| `<DOCUMENT_OWNER>` | Person responsible for this document. | `Alex` |

---

## What does not go in

The preserve rules, which are in the registry. The posture of the folder, which is in the registry.
A description of the contents, which an assistant can see.

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
