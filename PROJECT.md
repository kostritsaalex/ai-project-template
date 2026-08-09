# AI Project Template

> **AI Project Entry Point**
>
> Canonical project-wide context and instructions for the AI Project Template framework.
>
> Read this document before performing project-level tasks.
>
> **Project Version:** 0.1.0  
> **Last Updated:** 2026-08-09  
> **Document Owner:** Alex

---

# Project Overview

## Purpose

AI Project Template is an open framework for organizing AI-assisted projects.

It provides a consistent architecture for project documentation, AI instructions and reusable blueprints.

The framework is technology-agnostic and is intended to support software projects as well as multidisciplinary initiatives.

---

## Mission

Make AI-assisted projects easier to organize, easier to maintain, and easier for both humans and AI to understand.

---

# Project Scope

The framework currently covers:

- Project organization
- Documentation architecture
- AI entry points
- Blueprint library
- Documentation conventions
- AI collaboration patterns

Reference examples are a planned addition and do not exist yet.

The framework does not prescribe:

- Programming languages
- Development methodologies
- Technology stacks
- Repository hosting platforms
- Business processes

---

# Project Principles

Before making significant changes:

1. Understand the current architecture.
2. Identify the affected scope.
3. Read relevant documentation.
4. Prefer improving existing patterns over introducing new ones.
5. Keep the framework simple and internally consistent.
6. Validate architectural ideas through practical usage whenever possible.
7. Avoid speculative additions.
8. Preserve backward compatibility where practical.

---

# Design Philosophy

The framework is guided by several core principles:

- One canonical entry point per scope. Every other instruction document in that scope is an adapter.
- A document name belongs to exactly one type of scope.
- A reference to another scope carries an address that can be resolved from where the reference is read.
- Documentation lives as close as practical to the scope it describes.
- Information belongs to the smallest scope that fully covers everything it applies to.
- Avoid duplication.
- Evolve through real-world usage.
- Prefer simplicity over unnecessary flexibility.

---

# Framework Structure

The framework currently consists of:

## Documentation

Project-wide documentation explaining the framework architecture and philosophy.

## Blueprints

Reusable starting points for common project scopes.

- Assets, available at version 0.1.1
- Repository, available at version 0.1.0
- Project, planned

A blueprint is added only after it has been derived from a working implementation. Planned
blueprints have no placeholder directories.

Blueprints should be adapted rather than copied verbatim.

## Blueprint Comments

Blueprint files mark every unresolved decision with an HTML comment. Text without a comment is
ready to use as it stands.

A comment addresses the person adopting the blueprint. It has no place in the adopted document.
Adoption is finished when every comment has been worked through and removed, and the material it
asked for has been written in its place.

Anything that has to survive adoption belongs in visible text. A comment left in the file is read
by AI tools as an instruction, because they see the raw file rather than the rendered one. A leftover
`Replace this section` reads as a task, and a human reviewing the rendered document will not see it
sitting there.

## Adoption Checks

An adoption is verified rather than assumed. `blueprints/checks/` holds two prompts that apply to
every blueprint: a structural audit of the filled-in files, and a cold start check of whether an
assistant opening the folder for the first time picks up the context and follows it.

Both are built to return evidence rather than a verdict. The structural audit quotes a file and a
line for every check and treats an unevidenced check as failed. The cold start check runs in a new
session with no hints, because an assistant that already knows the answer from the conversation
tells you nothing about the files.

---

# Sources of Truth

Sources of truth follow the framework hierarchy:

- `PROJECT.md` defines project-wide context.
- Blueprint documentation defines reusable architectural patterns.
- Historical discussions provide context but may become outdated.

When information conflicts, prefer the canonical documentation for the relevant scope.

---

# Scope Ownership

Information should live at the smallest scope that fully covers everything it applies to.

- Framework-wide knowledge belongs at the project scope.
- Blueprint-specific knowledge belongs with the corresponding blueprint.
- Avoid duplicating the same guidance across scopes.

Blueprints may specialize framework conventions but should not contradict project-wide principles.

---

# Scope Entry Points

Every scope has exactly one canonical entry point. It holds the full context and instructions for
that scope.

Every other instruction document inside the same scope is an adapter. An adapter points to the
canonical entry point and holds no content of its own.

Adapters exist because external tools look for fixed filenames the framework does not control, such
as `AGENTS.md` and `CLAUDE.md`. Canonical entry point names are defined by the framework and are not
discovery names, so a canonical entry point is reached through an adapter rather than found directly
by a tool.

A document name belongs to exactly one type of scope. A scope must not contain a file named after
another scope's entry point, even as a pointer. Two files with the same name in different scopes
make it ambiguous which one is canonical, and a tool entering the smaller scope finds the wrong one
first.

---

# Cross-Scope References

A reference to another scope must carry an address that can be resolved from inside the referring
scope. Naming the other scope without an address leaves the reader aware that context exists and
unable to reach it.

An address is resolvable when it does not depend on knowledge the reader has no way to obtain. A
repository URL qualifies. A location on one person's machine does not.

A local path may sit alongside the address as a hint about where a checkout usually lives. Write it
relative to the home folder, as `~/parent-folder/name`, and never spell out a username. A username
ties the path to one machine, and `~` already stands for the home folder that contains it.

This constrains where a scope lives. A scope that other scopes reference has to be hosted somewhere
addressable.

Blueprints carry a placeholder where the address belongs. The adopted instance replaces it with a
real value. Independence from any particular environment is a property of the blueprint, and the
instance is free to name a specific address.

A scope should also state when parent context is actually required. Without that boundary, work the
scope fully covers on its own still sends the reader outward.

---

# Blueprint Lifecycle

Blueprints evolve through practical application.

The preferred lifecycle is:

```text
Working Implementation
        ↓
Generalization
        ↓
Blueprint
        ↓
Reference Example
        ↓
Production Projects
```

Architectural ideas should be validated in real-world usage before becoming part of a reusable blueprint.

---

# Documentation

`PROJECT.md` is the canonical entry point for this repository. `AGENTS.md` and `CLAUDE.md` are its adapters, as described in Scope Entry Points.

Project-wide documentation lives in `.docs/`.

Documentation should remain close to the scope it describes.

Create documentation when it becomes useful rather than creating speculative documents.

---

# Decisions

Architectural decisions should be documented and evolve alongside the framework.

Project-wide decisions belong in:

```text
.docs/decisions/
```

Blueprint-specific decisions belong alongside the corresponding blueprint.

Avoid duplicating decisions across scopes.

---

# Versioning

The framework follows Semantic Versioning where practical.

Framework releases describe the evolution of the overall architecture.

Individual blueprints may evolve independently while remaining compatible with the current framework version.

---

# Success Criteria

The framework is considered successful when it:

- Makes AI collaboration more predictable.
- Reduces ambiguity across projects.
- Encourages consistent documentation.
- Scales from small to large projects.
- Evolves through practical experience rather than theoretical design.

---

# Long-Term Vision

The goal is to build a practical, open framework for AI-assisted project organization that can be applied across different technologies, teams, and domains while remaining simple, maintainable, and easy to adopt.