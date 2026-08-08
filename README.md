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

- One canonical entry point per scope.
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
    └── assets/
```

`PROJECT.md` is the canonical entry point. `AGENTS.md` and `CLAUDE.md` are adapters that point AI
tools to it. The framework applies its own architecture to itself.

---

## Blueprints

The framework provides reusable blueprints for common project scopes.

Blueprints are derived from working implementations rather than designed up front, so they become
available one at a time.

| Blueprint | Scope | Status |
| --- | --- | --- |
| **Assets** | Organization of non-code project resources. | Available, version 0.1.0 |
| **Repository** | Repository-level AI instructions and technical documentation. | Planned |
| **Project** | Project-wide AI entry point and documentation structure. | Planned |

Planned blueprints have no placeholder directories. A blueprint appears once it has been derived
from a working implementation.

Blueprints are intended to be adapted rather than copied verbatim.

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