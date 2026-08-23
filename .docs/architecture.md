# Architecture

The framework has one structural idea: a project is a set of places, and one of them holds the map.

```text
Project scope          PROJECT.md + AGENTS.md + CLAUDE.md
│                      principles, boundaries, and the register of everything below
│
├── Component          AGENTS.md + CLAUDE.md
├── Component          AGENTS.md + CLAUDE.md
└── Component          AGENTS.md + CLAUDE.md + REPOSITORY.md or ASSETS.md
```

A component is any folder belonging to the project. It may sit inside the project scope's folder, in
a repository of its own, on another drive, or in another filesystem entirely.

---

## Why the register cannot live anywhere else

A folder does not know its siblings exist. Nothing an assistant can observe from inside one component
tells it that another exists, where it is, or how it is to be treated.

That is the one piece of knowledge no component can hold, because holding it would mean describing
the others. So one scope holds it, and every component points back at that scope. This is the whole
reason a project scope exists, and a project with no second place to work does not need one.

---

## What a component is told

One word, written in the register beside its name.

`Repository` means an assistant will mostly change things in that folder. `Assets` means it will
mostly find them and leave them as they are, and the four preserve rules travel with the word: do not
reorganize, do not rename, do not move, preserve the existing organization.

These are opposite postures rather than different subjects. A folder of photography and a folder of
marketing material differ in topic and not in kind. A folder of source kept without version control
takes `Repository`, because what it needs is rules for changing things safely.

Everything else a component might have said about itself is either visible from inside it, and so
belongs in no document, or true of the whole project, and so belongs in the project scope.

A folder that has not been declared a component is not one. It is files, belonging to whichever
component contains it and taking that component's posture. Being a component is a decision written
into the register rather than a property of what sits on disk.

---

## Addresses

A reference to another scope carries an address that resolves from where the reference is read.
Naming a scope without an address leaves the reader aware that context exists and unable to reach it.

Three forms qualify:

- A repository URL, written in full with the scheme. A private repository still gets its real URL,
  because it identifies the parent even when it cannot be opened.
- An account-relative location in a synced store, written as `OneDrive, Projects/northwind`. It
  resolves on any machine signed in to the same account and names no username.
- A relative path, when the referenced scope is a folder containing the referring one.

A location on one person's machine does not qualify. See
[decision 0001](decisions/0001-project-scope-need-not-be-a-repository.md) for what this constrains
about where a project scope may live.

A local path may sit beside the address as a hint about where the folder usually is. Write it
relative to the home folder, as `~/parent/name`, and never spell out a username: `~` already stands
for the home folder that contains it.

### The two directions

The register says where the component is, read from `PROJECT.md`. The stubs say where the parent is,
read from the component. For a component nested inside the project folder, that is `assets/brand` in
one and `../` in the other.

They are different values and writing one where the other belongs sends a reader out of the project.
`structure-check` fails a register block addressed `../`.

### When a path spans a mount boundary

A `~/` path under a synced store, read from another filesystem, holds because somebody made a symlink
once. Nothing in any file records that, so a document naming the path and not the arrangement is true
where it was written and false everywhere else.

When components sit on different sides of such a boundary, the project scope says where to start a
session so all of them resolve, and what makes its own local path true from there, with the command
that creates it.

---

## Entry points and stubs

The project scope has one canonical entry point, `PROJECT.md`. A component has none: its two stubs
are the first and only thing to read there.

`AGENTS.md` and `CLAUDE.md` exist because tools look for fixed filenames the framework does not
control. They carry identical text under two names. A rule written into one of them is a rule that
fires for one tool and not another.

`CLAUDE.md` may import a file that sits beside it, which is how an override reaches the reader
automatically. It never imports across folders: that would state the parent's location a second time,
in a second format, and an import outside the working directory asks for approval once and stays
disabled if declined, without saying so again.

---

## The test

> A document carries what cannot be seen, and nothing that can.

Everything above follows from it. See
[decision 0004](decisions/0004-documents-carry-what-cannot-be-seen.md) for where it came from, and
[decision 0005](decisions/0005-the-registry-carries-the-component.md) for what it removed when
applied to the number of documents rather than their contents.
