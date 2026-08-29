# AI Project Template

> **AI Project Entry Point**
>
> Read this before working anywhere in this project.
>
> **Derived from:** Project Blueprint 0.6.0  
> **Last Updated:** 2026-08-29  
> **Document Owner:** Alex

---

# What this project is

AI Project Template is an open framework for putting one roof over a project that lives in more than
one place.

A real project is rarely one folder. Code sits in a repository, material sits in a synced drive, a
workstream sits somewhere else again, and none of them knows the others exist. The framework gives
the project one entry point and one registry of everything under it, so that an assistant working in
any part can reach every other part.

Two rules follow. Whatever is true of the whole project is written once, in that one document.
Whatever is true of one part belongs to that part and nowhere else.

The framework is technology-agnostic. It suits software projects and equally suits work where
software is one part of something larger.

This project does not currently cover programming languages, development methodologies, technology
stacks, repository hosting, or business processes. It says where things live and how they are to be
treated, and stops there.

---

# Principles

1. One entry point per project, and every part of the project can reach it.
2. A document carries what cannot be seen, and nothing that can.
3. Information belongs to the smallest scope that fully covers everything it applies to.
4. A reference to another scope carries an address that resolves from where the reference is read.
5. Avoid duplication. A rule in two places is a rule that will disagree with itself.
6. Evolve through real use. An idea earns its place by being run, not by being argued for.
7. Cut before adding. A release that adds something has to name what it removed in exchange.

---

# Where this project lives

Address:

```text
https://github.com/kostritsaalex/ai-project-template
```

Local path:

```text
~/Projects/Frameworks/ai-project-template
```

---

# Components

This project has none. Everything lives in this one repository, so there is nothing for a registry
to point at.

The section stays because the blueprint has it and because the framework applies its own shape to
itself. A project that grows a second place to work adds a block here and two stubs there.

---

# Documentation and decisions

`.docs/architecture.md` explains the scope model. `.docs/decisions/` holds the record of why the
framework is shaped as it is, one file per decision, newest last. `.docs/release.md` is the procedure
for cutting a release of the framework, and a session about to cut one reads it first.

Blueprint-specific documentation lives beside its blueprint, in that folder's `README.md`.
