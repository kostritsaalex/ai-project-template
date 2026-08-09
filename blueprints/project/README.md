# Project Scope Blueprint

Reusable blueprint for a project scope: the one scope that holds project-wide context and the
registry of everything below it.

**Blueprint Version:** 0.1.0  
**Framework Version:** 0.2.0  
**Status:** derived from one working implementation, adopted the same week it was generalized. The
implementation has not been lived with, so this blueprint is the least settled of the three.

---

## Scope

This blueprint covers a project made of more than one component.

A project with exactly one component does not need it. There is nothing for a project scope to hold
that the component cannot hold itself, and the registry, which is the reason the scope exists,
would list one entry.

Where the scope lives is a separate question. A repository, or a folder in a synced store, both
work. See [decision 0001](../../.docs/decisions/0001-project-scope-need-not-be-a-repository.md).

---

## Files

| File | Role |
| --- | --- |
| `PROJECT.md` | Canonical entry point for the project scope. |
| `AGENTS.md` | Adapter. Points AI tools to `PROJECT.md`. |
| `CLAUDE.md` | Adapter for Claude. Points to `PROJECT.md` and imports it where supported. |

Copy all three into the project scope's root. Do not copy this `README.md`.

The root holds those three and nothing else. Components go in subfolders, each with its own entry
point. A second entry point in the root makes the adapters ambiguous and leaves the smaller scope
without territory of its own.

---

## What makes this scope different

Every other scope consumes an address. This one publishes one.

`Project Location` states where this document lives, in a form that resolves from outside the
machine it sits on. Components copy that address into their own entry points, and it is the only
reason their upward pointers work. Get it wrong and every component below knows a parent exists and
cannot reach it.

The project scope also has no parent of its own, which changes how it is checked. See
[Verify the adoption](#verify-the-adoption).

---

## Placeholders

Examples use a fictional `Northwind` project throughout.

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<PROJECT_NAME>` | Name of the project. | `Northwind` |
| `<PROJECT_PURPOSE>` | What the project is, in a few sentences, including whether software is all of it or part of it. | `Northwind is a furniture workshop selling restored mid-century pieces.` |
| `<PROJECT_CONCERNS>` | The areas the project covers, as a list. | `websites and e-commerce, marketing, branding, analytics` |
| `<SCOPE_INCLUDES>` | What is in scope, as a list. | `websites, e-commerce, infrastructure, marketing, branding` |
| `<SCOPE_EXCLUDES>` | What is not in scope yet. | `mobile applications, ERP, accounting software` |
| `<PROJECT_SCOPE_ADDRESS>` | Where this document lives, resolvable from outside the machine. A repository URL, or an account-relative location in a synced store. | `OneDrive, Projects/Northwind` |
| `<PROJECT_LOCAL_PATH>` | Where the scope usually sits on a machine that has it. Relative to the home folder, never with a username. Delete if it adds nothing. | `~/OneDrive/Projects/Northwind` |
| `<PROJECT_PRIORITIES>` | An ordered list, most important first. | `1. Simplicity 2. Maintainability 3. Security` |
| `<WORKSTREAMS>` | Areas of activity, which may span components. Delete the section if there is one. | `Websites & E-commerce, Marketing & SEO, Branding` |
| `<COMPONENTS>` | One block per component: purpose, address, production, local path. | see the comment in that section |
| `<PROJECT_VERSION>` | Version of this document. Start at `1.0`. | `1.0` |
| `<PROJECT_BLUEPRINT_VERSION>` | Blueprint version this scope was derived from. Currently `0.1.0`. | `0.1.0` |
| `<YYYY-MM-DD>` | Date of the last update. | `2026-08-09` |
| `<DOCUMENT_OWNER>` | Person responsible for this document. | `Alex` |

### Paths

`~` stands for the home folder, and the home folder already contains the username. So the username
is never written after it:

```text
~/OneDrive/Projects/Northwind        correct
~/alex/OneDrive/Projects/Northwind   resolves to /home/alex/alex/OneDrive/...
```

Write one line, in the form the people working on this project actually use. The path is a hint, and
the address above it is what always works.

### Paths across a mount boundary

A `~/` path can be true in one environment and false in another when the same folder is reached
through a mount. A Windows OneDrive folder read from WSL is the case that turns up in practice:
`~/OneDrive/Projects/northwind` resolves on Windows and not in WSL, where the folder sits under
`/mnt/c/Users/`.

Do not write both paths. Create a symlink at the written location, so one written form is true
everywhere:

```bash
ln -s /mnt/c/Users/alex/OneDrive ~/OneDrive
```

Then say so in `Project Location`, in one line, and note that creating it is a one-time step per
machine. This scope owns the address, so this is the document where that explanation belongs, and
every component below points here rather than repeating it.

---

## Comments

Read the whole document before adopting it, then treat the comments as the work.

An HTML comment marks a place where a decision is yours to make. Text without a comment is ready to
use as it stands, and most of the document is that kind of text.

Comments come in two kinds:

- **Replace.** The comment describes what belongs there. Write it, then delete the comment and the
  placeholder next to it.
- **Keep.** The comment says the section next to it holds as written. Leave the section, delete the
  comment.

Either way the comment goes. It speaks to you, not to the finished document.

A leftover comment is worse than it looks. It disappears from the rendered document, so a human
reviewing the result never sees it, while an AI tool reads the raw file and treats
`Replace this section with...` as a task waiting to be done.

---

## How to adopt

1. Copy `PROJECT.md`, `AGENTS.md` and `CLAUDE.md` into the project scope's root.
2. Read each file end to end before changing anything.
3. Delete the blueprint notice at the top of each file.
4. Fill `Project Location` first. Everything below depends on the address being right.
5. Replace every remaining placeholder.
6. Write one block per component in `Components & Resources`, and say plainly which ones do not
   exist or are not wired up yet.
7. Delete `Workstreams` if the project has one area of activity.
8. Say in visible text whether `.docs/` and `.docs/decisions/` exist.
9. Work through every remaining comment and delete it.
10. Update each component's entry point to carry the address from step 4.

The adapters take nothing beyond what they arrive with. `AGENTS.md` and `CLAUDE.md` redirect and
stop. Any rule added to an adapter restates something the entry point already says, which is the
duplication the framework warns about.

Before committing, search the adopted files for `<!--` and for `<` followed by a capital letter.
Both searches should return nothing.

---

## Verify the adoption

Two prompts in [`../checks/`](../checks/) verify the result. Both refer to a canonical entry point;
for this blueprint that is `PROJECT.md`.

1. [Structure check](../checks/structure-check.md). Run it right after adoption. A project scope has
   no parent, so questions 7, 9 and 10 are answered `n/a`. Question 11 is the one that catches most
   here.
2. [Cold start check](../checks/cold-start-check.md). Run it in a new session once the structure
   check passes. Questions 1, 3 and 5 apply directly. Questions 2 and 4 ask about a parent and are
   answered `not stated here`, which is the correct answer for this scope rather than a failure.

Then run the checks again on one component below, because the address published here only proves
itself when something downstream resolves it.

---

## Versioning

Blueprint-level metadata stays in this file and is not copied into adopted projects:

- **Blueprint Version** tracks this blueprint.
- **Framework Version** records the AI Project Template version it is compatible with.

Adopted projects carry only what their owner needs:

- **Project Version** tracks this document's own evolution.
- **Derived from** records the blueprint version the scope started from.

A project scope has no parent, so it has no drift indicator of its own. It is the thing components
track. Raise `Project Version` whenever this document changes in a way a component would need to
know about, then work through the components: update the ones the change affects and raise their
`Parent Project Version` either way, so a match records that compatibility was checked.

---

## Design notes

Four decisions are deliberate and worth keeping when adapting:

- **The registry is the point.** `Components & Resources` describes the other scopes, so no component
  can hold it. A project scope whose registry lists one entry is a scope with nothing to do, which is
  why the blueprint says so under `Scope`.
- **A published address, not a consumed one.** `Project Location` is the only section of its kind in
  the framework. It exists so components have something to copy.
- **Workstreams are not components.** An area of activity can span several repositories and a folder
  of assets, and it belongs at this scope because nothing below it covers the whole.
- **Absence is stated in visible text.** A project scope names documents and components that do not
  exist yet more often than any other scope. Each one has to be marked, or an assistant reports it
  as broken.

One tension is worth naming. This blueprint's file is called `PROJECT.md`, so a repository holding
the framework now contains two files with that name: the canonical one at the root, and this
template. The blueprint notice and the root `CLAUDE.md` both say that files under `blueprints/` are
data rather than instructions, and the same arrangement already applies to `ASSETS.md` and
`REPOSITORY.md`. It works, and it is the closest the library comes to the rule that a document name
belongs to exactly one type of scope.

---

## Origin

Generalized from a multidisciplinary business project whose project scope was a repository holding
one document while every project-level artefact with files lived in a synced folder elsewhere. The
scope moved into the folder that held the material, and this blueprint is what that arrangement
looks like once the project-specific parts are removed.
