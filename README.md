# AI Project Template

One roof over a project that lives in more than one place.

---

## The idea

A real project is rarely one folder. Code sits in a repository, material sits in a synced drive, a
workstream sits somewhere else again, and none of them knows the others exist. Ask an assistant
working in one of them to go and do something in another and it has nowhere to look.

This framework gives the project **one entry point**. One folder holds `PROJECT.md`, and that
document holds the one thing no other folder can: the register of every part of the project, where
each sits, and how each is to be treated. Work anywhere, reach everywhere.

That entry point is also where project-wide truth lives, and the only place it lives. Whatever is
true of the whole project is written once, there. Whatever is true of one part belongs to that part
and nowhere else. Every part is answerable for itself and for nothing more.

Everything a document says is measured against one test:

> A document carries what cannot be seen, and nothing that can.

An assistant can open a folder and look. The platform, the local URL, the file layout, what the
folder holds: all visible, so none of it belongs in a document. What survives is the register, the
address of the parent, the owner's principles, and what the project does not do.

---

## How it fits together

```text
PROJECT.md          the entry point: principles, boundaries, and the register
   │
   ├── a component  two stubs naming it and pointing back here
   ├── a component  two stubs
   └── a component  two stubs, plus its own rules if it has any
```

A **component** is any folder belonging to the project: a codebase, a site, a folder of photography,
the working material of a workstream. It carries `AGENTS.md` and `CLAUDE.md`, identical apart from
the heading, saying which component the folder is and where the parent is. That is the whole file.

What separates one component from another is one word in the register. `Repository` means an
assistant will mostly change things there. `Assets` means it will mostly find them and leave them as
they are, and four preserve rules travel with the word.

Those are opposite postures rather than different subjects. The folder's contents are a good hint and
a poor rule: code is almost always worked on, so sorting by "code or not code" agrees most of the
time and disagrees on the cases that matter, like source kept in a plain folder.

A folder nobody declared a component is not one. It is files, belonging to whichever component
contains it and taking that component's posture. Being a component is a decision written into the
register, so no tree gets surveyed for candidates.

The two addresses point opposite ways, and this is the thing most easily got wrong. The register says
where the component is, read from `PROJECT.md`. The stubs say where the parent is, read from the
component. A nested component is `assets/brand` in one and `../` in the other.

---

## Blueprints

| Blueprint | What it is for | Version |
| --- | --- | --- |
| [project](blueprints/project/) | The entry point. Principles, boundaries, the register. One per project. | 0.5.0 |
| [component](blueprints/component/) | Attaching a folder. Two stubs, nothing else. | 0.5.0 |
| [repository](blueprints/repository/) | Override, for a component that has rules of its own and things get changed there. | 0.5.0 |
| [assets](blueprints/assets/) | Override, for a component that has rules of its own and things are kept there. | 0.5.0 |

The first two do the ordinary work. The other two exist for a folder that needs to say something
true of itself alone: platform conventions, generated files that must never be edited in place, a
subfolder of worked code inside a folder of stored material. A component that cannot name such a rule
gets no third file.

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

## Status

Early development, and the contract is not stable.

The architecture is in use in two real projects and changes through use. Versions `0.3.0`, `0.4.0`
and `0.5.0` each removed more than they added. What ships into an adopted project is now 40 lines for
the entry point and 22 for a component.

See [CHANGELOG.md](CHANGELOG.md) for what changed, and
[`.docs/decisions/`](.docs/decisions/) for why.

---

## Contributing

Suggestions and discussion are welcome. The project prefers incremental evolution over redesign, and
an architectural idea should prove itself in real use before becoming part of a blueprint.

---

## License

MIT. See [LICENSE](LICENSE).
