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

Four forms qualify:

- A repository URL, written in full with the scheme. A private repository still gets its real URL,
  because it identifies the parent even when it cannot be opened.
- An account-relative location in a synced store, written as `OneDrive, Projects/northwind`. It
  resolves on any machine signed in to the same account and names no username.
- A relative path, when the referenced scope is a folder containing the referring one.
- None, said plainly, with the reason: `none. No copy of this folder exists off this machine.` The
  criterion is a copy that exists off the machine rather than version control. `git init` changes
  nothing here, and only a remote, a synced store, or a containing folder that travels makes one of
  the first three possible.

A location on one person's machine is not an address in any of these senses. Write the fourth form
instead, and put the local path on its own line beneath. See
[decision 0001](decisions/0001-project-scope-need-not-be-a-repository.md) for what this constrains
about where a project scope may live, and
[decision 0007](decisions/0007-a-component-with-no-address-says-so.md) for why the fourth form
exists.

The fourth form is what a component that exists on one machine only carries. `structure-check` 11
requires one of the four, and the case it exists to catch is a bare local path written into the
`Address:` slot: it reads as an address, resolves nowhere off this machine, and gives no sign that
there was never anything to follow.

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

**Most projects never meet any of this.** Everything in one filesystem means no boundary, no path
note and no session note, and both lines are deleted at adoption. Which setups are affected, and what
to do about each, is a table in the [README](../README.md#filesystem-boundaries). What follows here
is why.

A component that exists on one machine only is a different question, and it is answered under
Addresses above.

---

A `~/` path under a synced store, read from another filesystem, holds because somebody made a symlink
once. Nothing in any file records that, so a document naming the path and not the arrangement is true
where it was written and false everywhere else.

Two lines in the project scope answer that, and they answer different questions.

**The path note:** what makes the scope's own local path true, the arrangement holding it up and the
command that creates it on a machine that lacks it. This has nothing to do with components. A project
living in a single folder reached through a mount needs it just as much, and a scope adopted before
it has any components will need it on its first day.

**The session note:** where to start a session so that every component resolves. This one does depend
on the components, so it cannot be settled before they are named and has to be revisited when one is
added. A scope with no components carries no such line, correctly, and attaching one on the far side
of a boundary is what brings it into existence.

The session note is a precondition rather than a preference. When a project spans a boundary, one
side can usually reach both and the other cannot: from WSL, `/home` and `/mnt/c` are both ordinary
paths, while from the Windows side the WSL filesystem needs a `\\wsl.localhost\...` form. Read from
the wrong side, the local paths in the document are not inconvenient, they are false. And that
crossing form is worse than useless off the machine: the name is a local alias, so on another
computer it resolves to that computer's WSL and hands back a different folder rather than an error.

**On the evidence.** Everything in this section comes from one project, one machine and one person,
running Windows with WSL. A macOS setup with a network volume or an external disk is expected to have
the same shape and has not been tried. Weigh it accordingly; the rest of this document rests on more.

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
