# Architecture

The framework has one structural idea: a project is a set of places, and one of them holds the map.

```text
Project scope          PROJECT.md + AGENTS.md + CLAUDE.md
│                      principles, boundaries, and the registry of everything below
│
├── Component          AGENTS.md + CLAUDE.md
├── Component          AGENTS.md + CLAUDE.md
└── Component          AGENTS.md + CLAUDE.md + REPOSITORY.md or ASSETS.md
```

A component is any folder belonging to the project. It may sit inside the project scope's folder, in
a repository of its own, on another drive, or in another filesystem entirely.

---

## Why the registry cannot live anywhere else

A folder does not know its siblings exist. Nothing an assistant can observe from inside one component
tells it that another exists, where it is, or how it is to be treated.

That is the one piece of knowledge no component can hold, because holding it would mean describing
the others. So one scope holds it, and every component points back at that scope. This is the one
job only this scope can do.

It has a second job as well. Since `0.5.0` a component holds no document of its own, so a project
living in a single folder still comes here for anything it wants to record, and the registry sits
empty while it does.

---

## What a component is told

One word, written in the registry beside its name.

Being listed in the registry is what gives a component the project's principles. That is the floor,
and it is the whole of `Assets`: the folder is live, material arrives and gets updated, and the task
governs what happens in it.

`Repository` adds one rule on top of that floor. Platform or framework core changes only through its
own update mechanism, never by hand. The axis is ownership rather than immutability: core belongs to
its updater, so an upgrade that replaces it wholesale is the owner doing its job, while a hand edit
in the same files is silently undone by the next one.

So the two are a floor and one layer, and the layer is where anything learned later will go. See
[decision 0006](decisions/0006-the-postures-carry-one-rule-between-them.md).

Everything else a component might have said about itself is either visible from inside it, and so
belongs in no document, or true of the whole project, and so belongs in the project scope.

A folder that has not been declared a component is not one. It is files, belonging to whichever
component contains it and taking that component's posture. Being a component is a decision written
into the registry rather than a property of what sits on disk.

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

**No form covers a component that exists on one machine only,** with no remote and nothing syncing
it. That case is real and unsettled. Attaching the same such component twice produced two different
inventions: once an `Address:` line saying plainly that there is no remote, once the machine-local
path written into the `Address:` slot as though it were one. No check caught either, because
`structure-check` 11 asks a registry block for an address without saying what makes one valid, and
check 8 defines validity but reads only the component's own folder.

Until it is settled, write it the first way: say in the `Address:` line that the component has none
and why, and give its local path on its own line beneath. That is honest, and it leaves the reader
looking for a real address rather than following one that resolves nowhere.

A local path may sit beside the address as a hint about where the folder usually is. Write it
relative to the home folder, as `~/parent/name`, and never spell out a username: `~` already stands
for the home folder that contains it.

### The two directions

The registry says where the component is, read from `PROJECT.md`. The stubs say where the parent is,
read from the component. For a component nested inside the project folder, that is `assets/brand` in
one and `../` in the other.

They are different values and writing one where the other belongs sends a reader out of the project.
`structure-check` fails a registry block addressed `../`.

### When a path spans a mount boundary

A `~/` path under a synced store, read from another filesystem, holds because somebody made a symlink
once. Nothing in any file records that, so a document naming the path and not the arrangement is true
where it was written and false everywhere else.

Two lines in the project scope answer that, and they answer different questions.

What makes its own local path true: the arrangement holding it up and the command that creates it on
a machine that lacks it. This has nothing to do with components. A project living in a single folder
reached through a mount needs it just as much, and a scope adopted before it has any components will
need it on its first day.

Where to start a session so that every component resolves. This one does depend on the components,
so it cannot be settled before they are named and has to be revisited when one is added. A scope with
no components carries no such line, correctly, and attaching one on the far side of a boundary is
what brings it into existence.

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
