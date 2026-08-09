# AI Project Template

A practical framework for building AI-friendly software and multidisciplinary projects.

The framework provides a consistent architecture for organizing project knowledge, documentation, repositories, assets, and AI instructions.

Rather than being just a collection of templates, it captures a set of architectural principles refined through real-world use.

The framework is in early development. One blueprint is available today; the rest of the library is still being derived from working implementations.

---

## Mission

Make AI-assisted projects easier to organize, easier to maintain, and easier for both humans and AI to understand.

---

## Goals

The framework aims to provide:

- Consistent AI entry points
- Clear documentation hierarchy
- Scope-based knowledge organization
- Reusable blueprints
- Architectural patterns validated in practice

---

## Framework Overview

The framework is organized around two building blocks:

- **Blueprints** provide reusable starting points for common project scopes.
- **Documentation** explains the underlying architecture and design principles.

Reference examples are planned and will be added once the blueprint library is complete.

---

## Core Concepts

The framework is built around a small set of simple concepts:

- **Project**
- **Repository**
- **Component**
- **Scope**
- **Canonical Entry Point**
- **Source of Truth**

These concepts form the foundation for organizing both documentation and AI instructions.

---

## Design Principles

The framework follows a few fundamental principles:

- One canonical entry point per scope. Every other instruction document in that scope is an adapter.
- A document name belongs to exactly one type of scope.
- A reference to another scope carries an address that can be resolved from where the reference is read.
- Documentation lives as close as practical to the scope it describes.
- Information belongs to the smallest scope that fully covers everything it applies to.
- Avoid duplication.
- Evolve through real-world usage rather than theoretical design.

---

## Repository Structure

```text
.
├── PROJECT.md
├── AGENTS.md
├── CLAUDE.md
├── README.md
├── CHANGELOG.md
├── LICENSE
│
├── .docs/
│
└── blueprints/
    ├── assets/
    ├── repository/
    └── checks/
```

`PROJECT.md` is the canonical entry point. `AGENTS.md` and `CLAUDE.md` are adapters that point AI
tools to it. The framework applies its own architecture to itself.

---

## Blueprints

The framework provides reusable blueprints for common project scopes.

Blueprints are derived from working implementations rather than designed up front, so they become
available one at a time.

### Which one you need

The three match the three kinds of place work actually lives.

**Project** is the root. It holds `PROJECT.md`, the decisions folder, and the context that describes
the whole thing: what the project is, what falls inside it, what the priorities are, and where every
component sits. Nothing below can hold that, because it describes the others. There is one per
project, and everything else points at it.

**Repository** is a codebase. A website, an application, a service, a library. Its entry point
carries what someone needs in order to work on the code and stops there, then points upward for
anything reaching beyond it.

**Assets** is the rest: a folder of photography, brand files, video, contracts, or the working
material of a workstream such as marketing, SEO or sales. Its entry point says what the folder holds
and what may not be done to it, and points upward the same way.

A project typically has one project scope, one or more repositories, and one or more asset folders.
The asset folders can sit inside the project scope's own folder, which is often the simplest
arrangement when most of the non-code material already lives in one place.

`ASSETS.md` is the entry point for every non-code component, whatever the folder is about. A
`marketing/` folder beside `sales/` beside `media/` gets three copies of `ASSETS.md`, each
describing its own contents and rules. There is no `MARKETING.md`.

An entry point is named for the kind of scope it opens, not for its subject. Those three folders
differ in topic and not in kind: all hold material rather than code, and all are read the same way.
Naming them after subjects would grow the set of names with every new area of work and tell a reader
nothing they could not see from the folder name.

| Blueprint | Scope | Status |
| --- | --- | --- |
| **Assets** | Organization of non-code project resources. | Available, version 0.2.0 |
| **Repository** | Repository-level AI instructions and technical documentation. | Available, version 0.2.0 |
| **Project** | Project-wide AI entry point, component registry and published address. | Available, version 0.1.0 |

A blueprint appears once it has been derived from a working implementation. Planned ones have no
placeholder directories.

Blueprints are intended to be adapted rather than copied verbatim.

`blueprints/checks/` holds two prompts for verifying an adoption: one for the mechanics of the files,
one for whether an assistant opening the folder cold actually picks up the context. They apply to
every blueprint.

---

## Documentation

Project-wide documentation lives in `.docs/`.

Blueprint-specific documentation lives alongside its corresponding blueprint.

Documentation follows one fundamental rule:

> Documentation lives as close as practical to the scope it describes.

---

## Roadmap

Current focus:

- Core project architecture
- Blueprint architecture
- Complete blueprint library
- Documentation guides
- Reference examples
- Initial stable release (v1.0)

The first two are in place. The rest is open.

---

## Project Status

The project is under active development and its contract is not yet stable.

The architecture is in use in one real-world project and will keep evolving through practical experience.

---

## Contributing

Suggestions, discussions, and improvements are welcome.

The project prefers incremental evolution over large redesigns.

Architectural ideas should first prove themselves in real-world usage before becoming part of the framework.

---

## License

MIT. See the `LICENSE` file.