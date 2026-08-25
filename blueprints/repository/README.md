# Repository Override Blueprint

The optional third file for a `Repository` component, when that folder has rules of its own.

**Blueprint Version:** 0.6.0  
**Framework Version:** 0.7.0  
**Status:** in use in two components. Demoted in `0.5.0` from the normal way to attach a component
to the exception.

---

## When you need this

You do not need it to attach a folder to a project. [`../component/`](../component/) does that with
two stubs, and the parent registry carries the word `Repository` with the one rule that travels with
it: platform or framework core changes only through its own update mechanism, never by hand.

You need this file when the folder has rules that are its own and nowhere else: platform
conventions, a vendored dependency or a generated directory that a tool rather than a person owns, a
verification step particular to this codebase.

If you cannot name such a rule, do not create the file. A component with nothing to say about itself
says it in no file at all.

---

## Files

| File | Role |
| --- | --- |
| `REPOSITORY.md` | This folder's own rules. Not an entry point. |
| `AGENTS.md` | The component stub, plus one line sending the reader to `REPOSITORY.md`. |
| `CLAUDE.md` | The same, and it imports `REPOSITORY.md`, which is safe because the file is adjacent. |
| `platforms/` | Ready-made platform fragments. Not copied as files; their contents go into `Local rules`. |

Copy the first three into the repository root. Do not copy this `README.md` or `platforms/`.

---

## What changed in 0.5.0

`REPOSITORY.md` stopped being an entry point. It no longer carries the parent address, `Parent
checked`, or the escalation boundary that said when to read the parent.

The address moved to the stubs, which is where an arriving tool looks first. The escalation boundary
went away entirely: it existed so a component would not read a long parent document without reason,
and the parent is now short enough to read every time.

What is left is one thing, the folder's own rules, and the file exists only when there are some.

---

## Placeholders

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<REPOSITORY_NAME>` | Name of this component. Must match its heading in the parent registry. | `Northwind Storefront` |
| `<LOCAL_RULES>` | Whatever this component decides for itself. | contents of `platforms/wordpress.md`, trimmed |
| `<HAZARDS>` | Only what an assistant cannot find by looking. Usually empty; delete the section then. | `The staging checkout shares a Git remote with this one.` |
| `<REPOSITORY_BLUEPRINT_VERSION>` | Blueprint version this file started from. | `0.6.0` |
| `<YYYY-MM-DD>` | Date. | `2026-08-23` |
| `<DOCUMENT_OWNER>` | Person responsible for this document. | `Alex` |

The stubs carry `<COMPONENT_NAME>`, `<PROJECT_NAME>`, `<CANONICAL_PROJECT_SCOPE_ADDRESS>` and
`<PARENT_PROJECT_LOCAL_PATH>`. Those are described in [`../component/`](../component/).

---

## What does not go in

The posture of the folder, and the rule that travels with it. The parent registry carries both, and
if this file disagreed with it, the registry would be right and this file a bug.

The platform, the local URL, what the folder contains, whether a `.git` exists, which tools are
installed. All of it is visible to an assistant that opens the folder.

---

## How to adopt

1. Attach the component first, following [`../component/`](../component/).
2. Copy `REPOSITORY.md` into the repository root and delete the blueprint notice.
3. Fill `Local rules` from `platforms/` if a fragment fits, dropping the lines that cannot fire on
   work done from here.
4. Fill `Hazards`, or delete the section, which is the usual outcome.
5. Replace the stubs with the ones from this folder, which add the line pointing here.
6. Delete every remaining comment.

Before committing, search for `<!--` and for `<` followed by a capital letter.

---

## Verify the adoption

[Structure check](../checks/structure-check.md), then
[cold start check](../checks/cold-start-check.md) in a new session, using its component prompt.
