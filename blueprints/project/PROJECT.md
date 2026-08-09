> **BLUEPRINT FILE. NOT ACTIVE INSTRUCTIONS.**
>
> This file belongs to the AI Project Template blueprint library. It describes no real project
> and must not be followed as project instructions.
>
> To adopt it: copy this file into the project scope, replace every `<PLACEHOLDER>`, adapt the
> content to the actual project, and delete this notice.

---

<!--
Header metadata. Example of a filled-in block:

    Project Version:  1.0          (this document's own version, start at 1.0)
    Derived from:     Project Blueprint 0.1.0
    Last Updated:     2026-08-09
    Document Owner:   Alex

Project Version is what every component tracks as its Parent Project Version. Raise it whenever this
document changes in a way a component would need to know about, so the drift indicator downstream
means something.
-->

# <PROJECT_NAME>

> **AI Project Entry Point**
>
> Canonical project-wide context and instructions for <PROJECT_NAME>.
>
> Read this document before performing project-level tasks.
>
> **Project Version:** <PROJECT_VERSION>  
> **Derived from:** Project Blueprint <PROJECT_BLUEPRINT_VERSION>  
> **Last Updated:** <YYYY-MM-DD>  
> **Document Owner:** <DOCUMENT_OWNER>

---

# Project Overview

<!--
What the project is, in a few sentences. Write it for someone who has never heard of it.

Say whether the project is only software or whether software is one part of something larger. An
assistant that believes it is looking at a software project will treat everything else as out of
scope. Example:

    Northwind is a furniture workshop selling restored mid-century pieces.

    Northwind is a multidisciplinary business project. Websites and software matter, and they are
    one part of the whole.
-->

<PROJECT_PURPOSE>

The project covers:

<PROJECT_CONCERNS>

---

# Project Scope

<!--
Two lists. The second one matters more than it looks: without it, every adjacent idea reads as
in scope, and an assistant proposes work nobody asked for.

    Includes: websites, e-commerce, marketing, branding, analytics, internal automation
    Does not currently include: mobile applications, ERP, accounting software

"Does not currently include" is deliberate wording. It records a present boundary rather than a
permanent one.
-->

Includes:

<SCOPE_INCLUDES>

Does not currently include:

<SCOPE_EXCLUDES>

---

# Project Location

<!--
This section is what makes every component below reachable, and it is the one thing a project scope
publishes that no other scope does. Components copy the address from here into their own entry
points.

<PROJECT_SCOPE_ADDRESS> is where this document lives, in a form that resolves from outside the
machine it sits on:

    https://github.com/acme/northwind-project     a repository, full URL, scheme included
    OneDrive, Projects/Northwind                  a folder in a synced store, account-relative

<PROJECT_LOCAL_PATH> is a hint: where the scope usually sits on a machine that has it. Relative to
the home folder, never with a username spelled out:

    ~/Repositories/northwind-project
    ~/OneDrive/Projects/Northwind

If the scope is a repository and the local path adds nothing, delete the local path lines.

If a written ~/ path crosses a mount boundary, say what makes it resolve. A Windows folder read from
WSL is the case that comes up: create a symlink at the written location and state that doing so is a
one-time step per machine. Do not write two paths.
-->

This document is the canonical entry point for the <PROJECT_NAME> project scope.

Address:

```text
<PROJECT_SCOPE_ADDRESS>
```

Local path:

```text
<PROJECT_LOCAL_PATH>
```

Components outside this scope reference it by that address. Components inside it reference it by
relative path.

---

# Project-Wide AI Principles

<!-- Keep the list below as written. It holds regardless of project or technology. -->

Before performing a task:

1. Understand the relevant project context and current state.
2. Identify the affected workstream or component.
3. Read documentation relevant to the task.
4. Ask for clarification when requirements are unclear. Never invent requirements.
5. Change only what is necessary for the requested task.
6. Prefer simple, maintainable solutions over unnecessary complexity.
7. Explain meaningful trade-offs when multiple solutions exist.
8. Define what successful completion means and verify the result.

Do not modify unrelated work unless explicitly requested.

---

# Project Priorities

<!--
An ordered list, most important first. The order is the content: a list everyone agrees with in any
order decides nothing. Example:

    1. Simplicity
    2. Maintainability
    3. Security
    4. Performance
    5. Accessibility
    6. User Experience
    7. Appearance

Keep the closing paragraph. Without it the order is read as absolute and applied where it does not
belong.
-->

<PROJECT_PRIORITIES>

Apply priorities in the context of the relevant task. Not every priority applies equally to every
workstream.

---

# Decision Rules

<!-- Keep this section as written unless the project has a reason to decide differently. -->

When multiple solutions exist:

- Prefer native platform capabilities when appropriate.
- Prefer fewer dependencies.
- Prefer long-term maintainability.
- Do not add speculative features, abstractions or configurability.
- Avoid unnecessary complexity.
- Explain meaningful advantages and disadvantages.

---

# Sources of Truth

<!-- Keep this section as written. Drop the lines that name things this project does not have. -->

Sources of truth depend on the relevant scope:

- Project documentation defines project-wide context, conventions and intended direction.
- Component documentation defines component-specific context and conventions.
- Repositories and configuration define technical implementation.
- Production systems and published channels define currently deployed or published state.
- Historical notes and discussions provide context but may be outdated.

When sources conflict, investigate before proceeding. Ask for clarification when intended behavior
cannot be determined confidently.

---

# Scope Ownership

<!-- Keep this section as written. It is the rule the whole arrangement rests on. -->

Information should live at the smallest scope that fully covers everything it applies to.

- Project-wide information belongs to the <PROJECT_NAME> project scope.
- Information specific to one component belongs to that component.
- Information spanning multiple components belongs at the project scope.
- Avoid duplicating the same instruction or decision across scopes.

Component-level instructions may specialize project-wide rules for their scope, but should not
contradict project-wide principles unless explicitly authorized.

---

# Workstreams

<!--
Areas of activity, which are not the same thing as components. A workstream can span several
components, and several workstreams can run inside one. Example:

    - Websites & E-commerce
    - Marketing & SEO
    - Branding
    - Analytics & Customer Experience
    - Internal Automation

Delete this section if the project has one area of activity. Naming a single workstream adds a layer
that decides nothing.
-->

Current <PROJECT_NAME> workstreams include:

<WORKSTREAMS>

Workstreams describe areas of activity. They are independent from repositories and storage locations
and may span multiple components.

Workstream documentation that spans multiple components belongs in project-level documentation.
Component-specific implementation details belong to the relevant component documentation.

---

# Components & Resources

## Component Conventions

<!--
Keep this subsection as written. It is repeated here rather than left to the framework because an
assistant working in this project has no access to the framework documentation.
-->

Each project component should have exactly one canonical AI entry point.

The entry point should be named according to the nature of the component.

Examples:

- Project → `PROJECT.md`
- Repository → `REPOSITORY.md`
- Assets → `ASSETS.md`

`AGENTS.md` and `CLAUDE.md` act as adapters and should always direct AI assistants to the
component's canonical entry point.

A component may live in its own repository or inside this scope's folder. A component inside this
folder occupies its own subfolder and carries its entry point there. This scope's root holds
`PROJECT.md` and its adapters and nothing else, so that a tool entering the root reaches the project
and a tool entering a subfolder reaches that component.

<!--
Below, one block per component. This is the registry, and it is the reason a project scope exists at
all: no component can hold it, because it describes the others. Give each one enough to be reached.

    ## Northwind Storefront

    **Purpose:** English-language shop
    **Platform:** Django + Wagtail
    **Repository:** https://github.com/acme/northwind-storefront
    **Production:** https://shop.northwind.example
    **Local checkout:** `~/Repositories/northwind-storefront`

    Repository-specific instructions and technical documentation belong to that repository.

State plainly when something does not exist yet: a component with no repository, or one whose
repository has never been wired to this scope. An assistant told nothing assumes the chain works.

A second working copy of a repository is not a component. Record it inside the component it belongs
to.
-->

<COMPONENTS>

---

# Documentation

`PROJECT.md` is the canonical project-wide AI entry point.

Detailed project documentation belongs in `.docs/`.

Documentation should live as close as practical to the scope it describes:

- Project-wide knowledge → project `.docs/`
- Repository-specific knowledge → repository `.docs/`
- Component-specific knowledge → component documentation

Create documentation when it is needed rather than creating speculative empty documents.

<!--
If `.docs/` does not exist yet, say so here in one visible line:

    A project `.docs/` folder does not exist yet. Create it when there is something to put in it.

A project scope collects references to documents that do not exist faster than anything else in the
framework, and an assistant reports each one as missing unless the document says otherwise.
-->

---

# Decisions

Decisions should be recorded at the smallest scope that fully covers everything they affect.

- Decisions affecting <PROJECT_NAME> as a whole, multiple components or multiple workstreams belong
  in project `.docs/decisions/`.
- Decisions affecting only one component or repository belong in that scope's `.docs/decisions/`.

Avoid duplicating the same decision across scopes.

<!--
If `.docs/decisions/` does not exist yet, keep a line saying where decisions go meanwhile:

    Until project `.docs/decisions/` exists, project-wide decisions may be recorded in this document.
-->
