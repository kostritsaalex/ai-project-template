# Project Scope Blueprint

The one scope that holds project-wide context and the registry of everything below it.

**Blueprint Version:** 0.10.0  
**Framework Version:** 0.10.0  
**Status:** in use in two projects. `0.5.0` moved what a component says about itself into the
registry, and `0.6.0` cut that line down to one rule.

---

## Scope

A project passes through up to three states, and takes the documents of the state it is actually in.

**No documents.** The project is still finding its shape and has no rule, boundary or principle
settled enough to write down, and no second place to work in sight. Adopting anything here is
premature.

A project that has nothing recorded yet but knows a second place is coming belongs in the next state
rather than this one. The registry it is about to need is the thing only this scope can hold.

**This scope alone.** The project has settled on something worth recording and still lives in one
folder. It takes `PROJECT.md` with `AGENTS.md` and `CLAUDE.md` beside it, and nothing else. The
registry stays empty and says so in visible text. This is a finished setup rather than half of one.

**This scope with components.** The project works in a second place. Every place gets two stubs of
its own and one block in the registry, which is the one thing no other scope can hold.

A project moves to the next state when it gets there, never in advance. Many never leave the second
one.

Where the scope lives is a separate question. A repository or a folder in a synced store both work.
See [decision 0001](../../.docs/decisions/0001-project-scope-need-not-be-a-repository.md).

---

## Files

| File | Role |
| --- | --- |
| `PROJECT.md` | Canonical entry point. |
| `AGENTS.md` | Adapter. Points AI tools to `PROJECT.md`. |
| `CLAUDE.md` | Adapter for Claude. Points to `PROJECT.md` and imports it where supported. |

Copy all three into the project scope's root. Do not copy this `README.md`.

The root holds no second AI entry point. A component that sits inside this folder occupies its own
subfolder and carries its two stubs there. A second entry point beside `PROJECT.md` makes the
adapters ambiguous, because they name the one file to read first.

Ordinary project files are none of this framework's business. A `README.md`, a `LICENSE`, a
changelog: the rule above says nothing about them.

---

## A default for `Principles`, offered and not pre-filled

Two, and they are offered aloud in the interview rather than written into the template. Show them in
the summary table as proposed, and write only what the owner keeps. Saying nothing leaves the section
empty, which is a real answer.

- Validate ideas through practical use whenever possible.
- Avoid speculative additions.

Six more were considered and cut, each for failing the razor in
[decision 0008](../../.docs/decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md).
The reasoning is in
[decision 0012](../../.docs/decisions/0012-two-default-principles-of-eight.md). These two survive
because neither describes what an assistant does anyway, and neither assumes a codebase: the six cut
all did.

---

## What makes this scope different

Every other scope consumes an address. This one publishes one, and every component copies it. Get it
wrong and each of them knows a parent exists and cannot reach it.

It also holds the registry, which is what lets an assistant working in one folder move to another
that sits somewhere else entirely. That is the feature the framework exists for.

Since `0.5.0` the registry carries one thing more: each component's posture. Since `0.6.0` that word
carries the project's principles and, for `Repository`, one rule about platform and framework core.
A component normally holds two stubs and no document of its own, so this is the only place that says
it.

---

## Placeholders

Examples use a fictional `Northwind` project.

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<PROJECT_NAME>` | Name of the project. Keeps its spaces; the folder need not match. | `Northwind Furniture` |
| `<PROJECT_PURPOSE>` | What the project is, in a few sentences, including whether software is all of it or part of it. | `Northwind is a furniture workshop selling restored mid-century pieces. Websites and software are one part of it.` |
| `<SCOPE_COVERS>` | What the project covers, followed by the closure sentence that makes it a boundary. The one line proven to change what an assistant does. A near miss may be named after it and need not be. Undecided is an answer: replace the whole sentence with what will settle it and what to do meanwhile, and never leave the topic out. See [decision 0011](../../.docs/decisions/0011-the-boundary-is-a-closed-inclusion.md). | `the main folder and the northwind-storefront repository` |
| `<PROJECT_PRINCIPLES>` | The rules that hold across the project, in the owner's words. Priorities in order if the order was decided. | `1. Simplicity 2. Maintainability 3. Security` |
| `<PROJECT_SCOPE_ADDRESS>` | Where this document lives, resolvable from outside the machine. | `OneDrive, Projects/northwind` |
| `<PROJECT_LOCAL_PATH>` | Where the scope usually sits on a machine that has it. Relative to the home folder, no username after the tilde. Delete if it adds nothing. | `~/OneDrive/Projects/northwind` |
| `<PATH_NOTE>` | What makes the local path above true: the symlink or mount holding it up, and the command that creates it. Nothing to do with components; a single-folder project reached through a mount needs it too. Delete only when the path holds on its own. | a line naming the symlink, plus `ln -s /mnt/c/Users/alex/OneDrive ~/OneDrive` |
| `<SESSION_NOTE>` | Where to start a session so every component in the registry resolves. Depends on the components, so it is settled after they are named and revisited when one is added. Delete while every component sits on this folder's side. | `Start sessions inside WSL. From there both this folder and ~/wordpress-7 are ordinary paths.` |
| `<COMPONENTS>` | One block per component: name, posture, address, local path. | see the comment in that section |
| `<PROJECT_BLUEPRINT_VERSION>` | Blueprint version this scope started from. | `0.7.0` |
| `<YYYY-MM-DD>` | Date of the last update. | `2026-08-23` |
| `<DOCUMENT_OWNER>` | Person responsible for this document. | `Alex` |

### Paths and folder names

`~` already contains the username, so nothing follows it: `~/OneDrive/Projects/northwind`, never
`~/alex/OneDrive/...`, which resolves to `/home/alex/alex/...`.

Keep spaces out of folder names. A space resolves fine on every system and costs a pair of quotes in
every shell command that touches the folder, forever, plus breakage in anything that splits paths on
whitespace. Hyphens or underscores instead.

A `~/` path can be true in one environment and false in another when the folder is reached through a
mount. Do not write two paths: create a symlink at the written location so one form is true
everywhere, and say so in one line.

```bash
ln -s /mnt/c/Users/alex/OneDrive ~/OneDrive
```

---

## Comments

An HTML comment marks a decision that is yours. Text without one is ready as it stands. Either way
the comment goes when you are done: it speaks to you, not to the finished document, and a leftover
comment is invisible to a human reviewer while an AI tool reads it as a task waiting to be done.

---

## How to adopt

1. Copy the three files into the project scope's root.
2. Delete the blueprint notice at the top of each.
3. Fill the address first. Everything below depends on it.
4. Replace the remaining placeholders.
5. Write one block per component, and say plainly which do not exist or are not wired yet.
6. Say in visible text whether `.docs/` and `.docs/decisions/` exist.
7. Delete every remaining comment.

The adapters redirect and stop. A rule added to one duplicates the entry point.

Before committing, search for `<!--` and for `<` followed by a capital letter. Both should return
nothing.

---

## Keeping up to date

Blueprint metadata stays in this file and is not copied into adopted projects.

An adopted project carries no version counter. Editing `PROJECT.md` obliges you to do nothing else:
change the text, set `Last Updated`, stop. Components hold no copy of anything written here, so
none of them can fall behind it.

One change still reaches the components by hand: an edit to the address. Each stub holds a copy of
it, and a stale copy passes both checks in [`../checks/`](../checks/) and fails only when somebody
follows it.

Adding, renaming or moving a component is one edit here and nothing else, unless the folder itself
moved, in which case its two stubs get the new parent address.

---

## Verify the adoption

[Structure check](../checks/structure-check.md) right after adoption, then
[cold start check](../checks/cold-start-check.md) in a new session, using its project scope prompt.
Then run both on one component, because the address published here only proves itself when something
downstream resolves it.
