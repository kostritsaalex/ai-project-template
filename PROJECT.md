# AI Project Template

> **AI Project Entry Point**
>
> Canonical project-wide context and instructions for the AI Project Template framework.
>
> Read this document before performing project-level tasks.
>
> **Project Version:** 0.0.1  
> **Last Updated:** 2026-08-08  
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

- One canonical entry point per scope.
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

- Assets, available at version 0.1.0
- Repository, planned
- Project, planned

A blueprint is added only after it has been derived from a working implementation. Planned
blueprints have no placeholder directories.

Blueprints should be adapted rather than copied verbatim.

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

`PROJECT.md` is the canonical entry point for this repository. `AGENTS.md` and `CLAUDE.md` are adapters that point AI tools to it and carry no instructions of their own.

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