# AI Project Template

One roof over a project that lives in more than one place.

---

## The idea

A real project is rarely one folder. Code sits in a repository, material sits in a synced drive, a
workstream sits somewhere else again, and none of them knows the others exist. Ask an assistant
working in one of them to go and do something in another and it has nowhere to look.

This framework gives the project **one entry point**. One folder holds `PROJECT.md`, and that
document holds the one thing no other folder can: the registry of every part of the project, where
each sits, and how each is to be treated. Work anywhere, reach everywhere.

That entry point is also where project-wide truth lives, and the only place it lives. Whatever is
true of the whole project is written once, there. Whatever is true of one part belongs to that part
and nowhere else. Every part is answerable for itself and for nothing more.

Everything a document says is measured against one test:

> A document carries what cannot be seen, and nothing that can.

An assistant can open a folder and look. The platform, the local URL, the file layout, what the
folder holds: all visible, so none of it belongs in a document. What survives is the registry, the
address of the parent, the owner's principles, and what the project does not do.

---

## How it fits together

```text
PROJECT.md          the entry point: principles, boundaries, and the registry
   │
   ├── a component  two stubs naming it and pointing back here
   ├── a component  two stubs
   └── a component  two stubs, plus its own rules if it has any
```

A **component** is any folder belonging to the project: a codebase, a site, a folder of photography,
the working material of a workstream. It carries `AGENTS.md` and `CLAUDE.md`, identical apart from
the heading, saying which component the folder is and where the parent is. That is the whole file.

What separates one component from another is one word in the registry. Both words inherit the
project's principles and nothing else is shared. `Assets` adds nothing on top: the folder is live,
material arrives and gets updated, and the task governs what happens in it. `Repository` adds a
single rule, that platform or framework core changes only through its own update mechanism and never
by hand.

So the two are a floor and one layer above it, and the layer is where anything learned later will
go. A folder that needs more than its word gives it takes an override file of its own.

A folder nobody declared a component is not one. It is files, belonging to whichever component
contains it and taking that component's posture. Being a component is a decision written into the
registry, so no tree gets surveyed for candidates.

The two addresses point opposite ways, and this is the thing most easily got wrong. The registry says
where the component is, read from `PROJECT.md`. The stubs say where the parent is, read from the
component. A nested component is `assets/brand` in one and `../` in the other.

---

## Blueprints

| Blueprint | What it is for | Version |
| --- | --- | --- |
| [project](blueprints/project/) | The entry point. Principles, boundaries, the registry. One per project. | 0.7.0 |
| [component](blueprints/component/) | Attaching a folder. Two stubs, nothing else. | 0.6.0 |
| [repository](blueprints/repository/) | Override, for a `Repository` component that has rules of its own. | 0.6.0 |
| [assets](blueprints/assets/) | Override, for an `Assets` component that has rules of its own. | 0.6.0 |

The first two do the ordinary work. The other two exist for a folder that needs to say something
true of itself alone: platform conventions, a directory a tool rather than a person owns, an
arrangement that must not be rearranged. A component that cannot name such a rule gets no third
file.

Blueprints are derived from working implementations rather than designed up front, and are meant to
be adapted rather than copied verbatim.

---

## Adopting one

[`blueprints/setup/`](blueprints/setup/) holds two prompts. You paste one, answer questions, and get
filled files: `new-project.md` for the entry point, `new-component.md` for every folder after that.

[`blueprints/checks/`](blueprints/checks/) holds two more. `structure-check.md` audits the mechanics
and returns a quote for every row. `cold-start-check.md` asks whether an assistant opening the folder
for the first time actually picks up the context, and has to run in a session that did not perform
the adoption.

---

## Folder names

Keep spaces out of the folders that make up a project's paths. Use hyphens or underscores.

A space resolves fine on every operating system. What it costs is a pair of quotes in every shell
command that touches the folder, for as long as the project exists, plus silent breakage in anything
that splits a path on whitespace. `cd ~/Projects/My Project` fails; `cd ~/Projects/my-project` does
not.

The project's own name keeps its spaces and is the title of `PROJECT.md`. Only the folder is
constrained, and nothing requires the two to match.

---

## Filesystem boundaries

Find your setup in the first column. If it is the first row, this section is over and nothing here
applies to you.

| Your setup | Path note | Session note | What to do | What goes wrong if you skip it |
| --- | --- | --- | --- | --- |
| Everything in one filesystem. The scope and every component reached the same way, whatever the operating system. Windows only, macOS only, Linux only. | no | no | Nothing. | Nothing. Delete both lines at adoption and forget they exist. |
| The scope's own folder is reached through a mount or a symlink, and every component sits with it. For example the scope in a synced store, opened from WSL. | yes | no | Work from the side that reaches both. On Windows with WSL that is WSL, where `/home` and `/mnt/c` are both ordinary paths. Make the symlink once so the `~/` form is true there. | The `~/` path is true on the machine that wrote it and false on the next one, with nothing recording why. |
| Components sit on both sides of a boundary. For example the scope in a synced store on Windows and a component in the WSL home filesystem. | yes | yes | The same, and now write it down: the session note names that side. | A session started on the wrong side cannot resolve part of the registry at all, and the path form that does reach across is local to one machine. |

**Pick the side that sees everything and start every session there, and the problem stops happening
to you.** On Windows with WSL that side is WSL: from there the Linux filesystem and the Windows one
are both ordinary paths, so nothing in the registry is out of reach. The two lines still get written,
because the next person, the next machine and the next assistant do not know your habit.

This is about where you work, not where files live. Code belongs in the WSL filesystem, where it is
fast, and material in a synced store has to sit on the Windows side to sync at all. Neither has to
move.

Everything in this section comes from one project on one machine running Windows with WSL. A macOS
setup with a network volume is expected to have the same shape and has not been tried. The reasoning
is in [`.docs/architecture.md`](.docs/architecture.md).

---

## Status

Early development, and the contract is not stable.

**What would make it `1.0`.** Two things, and neither has happened. Both are checkable, which is the
point of writing them down rather than waiting to feel ready.

*The shape survives a project somebody else adopted.* Every project the framework has been through
was adopted by its author, who knows what each document is for and repairs it without noticing. An
adoption by somebody else, who then works in the project for a while and comes back with what broke,
is the first evidence that the shape is a shape rather than one person's habit.

*A check catches a defect nobody planted.* The checks have been run positively many times and
negatively a few, against documents broken on purpose to see whether the check notices. That proves
the check fires. It does not prove the check is worth running, which needs a real defect, arriving
by ordinary carelessness, found by a check before a person found it.

The architecture is in use in two real projects and changes through use. Every release from `0.3.0`
to `0.5.0` removed more than it added. `0.6.0` was the first to spend a line: it cut four rules down
to one and put that one where it fires. What ships into an adopted project is 41 non-blank lines for
a project scope, 34 of them `PROJECT.md` and 7 its two adapters, and 22 for a component across its
two stubs. The metric is non-blank lines with the blueprint notice and every HTML comment stripped,
summed across the files a scope ships; an override is not counted, since a folder has one only when
it has something to add. Re-measured at `0.9.0`, and re-measured at every release, which
is a step in [`.docs/release.md`](.docs/release.md).

`0.6.0` was also the first release validated by resetting a real project to bare folders and
adopting it again from scratch. Five structure checks, five cold starts, no failures, and eleven
defects found and fixed on the way.

`0.8.0` is the first release to remove a rule because it was measured and made no difference, rather
than because it had never been run. Two copies of one component, differing only in whether it carried
its own rules, produced the same work on the same task.

`0.9.0` adds the third check, run in both directions before shipping and with every run committed.
It also puts a measured limit on what any of these checks is worth: two runs of one prompt against
one unchanged scope disagreed on a row, so a check's result is mechanical only as far as each row is
fully specified.

See [CHANGELOG.md](CHANGELOG.md) for what changed, and
[`.docs/decisions/`](.docs/decisions/) for why.

---

## Contributing

Suggestions and discussion are welcome. The project prefers incremental evolution over redesign, and
an architectural idea should prove itself in real use before becoming part of a blueprint.

---

## License

MIT. See [LICENSE](LICENSE).
