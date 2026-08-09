> **BLUEPRINT FILE. NOT ACTIVE INSTRUCTIONS.**
>
> This file belongs to the AI Project Template blueprint library. It describes no real repository
> and must not be followed as project instructions.
>
> To adopt it: copy this file into the target repository, replace every `<PLACEHOLDER>`, adapt the
> content to the actual repository, and delete this notice.

---

<!--
Header metadata. Example of a filled-in block:

    Repository Version:     1.0          (this document's own version, start at 1.0)
    Parent Project:         https://github.com/acme/northwind-project
    Parent Project Version: 2.0          (the PROJECT.md version this was written against)
    Derived from:           Repository Blueprint 0.1.0
    Last Updated:           2026-08-09
    Document Owner:         Alex

Parent Project Version is a drift indicator. When the parent PROJECT.md moves, compare the change
against this document and update this line either way, so a match means compatibility was checked
rather than assumed.
-->

# <REPOSITORY_NAME>

> **AI Repository Entry Point**
>
> Canonical repository-wide context and instructions for the <REPOSITORY_NAME> component.
>
> Read this document before performing any task in this repository.
>
> **Repository Version:** <REPOSITORY_VERSION>  
> **Parent Project:** <CANONICAL_PROJECT_REPOSITORY_URL>  
> **Parent Project Version:** <PARENT_PROJECT_VERSION>  
> **Derived from:** Repository Blueprint <REPOSITORY_BLUEPRINT_VERSION>  
> **Last Updated:** <YYYY-MM-DD>  
> **Document Owner:** <DOCUMENT_OWNER>

---

# Repository Context

<!--
One or two sentences: what this repository holds and what it produces. Name the technology and the
deployed result, so the assistant knows what it is looking at before it opens a single file.

    the Northwind storefront: the English-language shop at https://shop.northwind.example,
    built on <platform> and <commerce plugin>
-->

This repository contains <REPOSITORY_PURPOSE>.

It is one component of the <PROJECT_NAME> project. Project-wide goals, conventions and
cross-component decisions are defined by the project, not here.

This document defines repository-specific guidance only.

---

# Parent Project

<!--
The two lines below are the reason this document works at all. Getting them wrong leaves the
assistant knowing a parent project exists and unable to reach it.

<CANONICAL_PROJECT_REPOSITORY_URL> is the repository that holds the canonical PROJECT.md. Write the
full URL, scheme included:

    https://github.com/acme/northwind-project

A private repository still gets its real URL. It identifies the parent even when it cannot be
opened, and the fallback paragraph further down covers that case.

<RECOMMENDED_LOCAL_CHECKOUT_PATH> is a hint, not a guarantee: where the checkout usually sits when
someone already has one. Write it relative to the home folder:

    ~/Repositories/northwind-project

`~` already stands for your home folder, which already contains your username. Writing
`~/alex/Repositories/...` resolves to `/home/alex/alex/Repositories/...` and is the usual mistake
here. The same location spelled out in full:

    Linux, WSL    /home/alex/Repositories/northwind-project
    macOS         /Users/alex/Repositories/northwind-project
    Windows       C:\Users\alex\Repositories\northwind-project

All three name one person's machine, which is why the document carries the `~` form instead. Keep it
to one line, in the form the people working on this repository actually use.
-->

Canonical project repository:

<CANONICAL_PROJECT_REPOSITORY_URL>

Recommended local checkout:

`<RECOMMENDED_LOCAL_CHECKOUT_PATH>`

The canonical `PROJECT.md` lives at the root of that repository.

Read it when a task depends on project-wide context: <PROJECT_WIDE_CONCERNS>. Purely technical work
inside this repository does not require it.

<!--
Replace <PROJECT_WIDE_CONCERNS> with the concerns that actually live above this repository:

    brand and tone of voice, conventions shared with other components, search strategy,
    anything visible to end users, decisions affecting more than this repository

Keep the list specific and short. Without it the assistant reaches for project context before every
change, and the trip upward becomes a habit rather than a decision.
-->

If the canonical project context is needed but unavailable, ask for access or for the relevant
context. Never infer or recreate project-wide requirements.

When repository-specific guidance conflicts with a project-wide principle, ask before proceeding.

---

# Development Environment

<!--
Four short facts, no commands. Example:

    Platform:           <framework or CMS> + <notable extension>
    Environment:        <container or runtime tooling>, on <host OS if it matters>
    Local development:  https://northwind.test
    Production:         https://shop.northwind.example

Add a Sandbox line if a second environment exists, and describe it under Environment hazards below.
-->

**Platform:** <PLATFORM>  
**Environment:** <LOCAL_ENVIRONMENT>  
**Local development:** <LOCAL_DEVELOPMENT_URL>  
**Production:** <PRODUCTION_URL>

Commands and setup procedures belong in `.docs/development.md`.

## Environment access

If the AI environment does not have shell access to the developer's actual machine, ask for the
environment to be started and confirmed ready before performing tasks that depend on it. A sandboxed
or remote shell does not qualify: having a terminal is not the same as having access to this
machine.

Local environments often need time after their containers or services report ready. Retry loading
the local development URL rather than treating the first failed check as a failure.

<!-- Keep both paragraphs above as written. They hold regardless of platform. -->

## Environment hazards

<!--
List conditions the assistant cannot infer from the files in front of it: shared Git remotes,
shared databases, credentials that reach production, services that look isolated and are not.
Delete this section if none apply.

Example from a working implementation:

  The sandbox is a second checkout of this repository, not an isolated one. It shares the same Git
  remote and branch as the local development checkout, so a push from the sandbox goes to the
  production repository. Confirm the working directory before any Git operation that writes to the
  remote.
-->

<ENVIRONMENT_HAZARDS>

---

# Platform Principles

<!--
Replace this section with the principles of the platform this repository is built on.

Ready-made fragments live in `platforms/` in the Repository Blueprint. Copy the matching fragment
here in full. If none matches, write the rules that keep the platform upgradeable and its documented
extension points intact. Example of that kind of rule:

    Never modify the platform's own code or third-party extensions. Prefer documented
    extension points, so an update does not silently revert the change.

Six to nine lines is enough. Detailed conventions belong in `.docs/`.
-->

<PLATFORM_PRINCIPLES>

---

# Sources of Truth

Repository-specific:

- Source code and configuration define the implementation.
- Production defines currently deployed behavior.
- Repository documentation in `.docs/` defines intended technical behavior and conventions.

Project-wide:

- The canonical `PROJECT.md` defines project context and conventions.

When sources conflict, investigate the code, configuration and environment. Do not assume
documentation is current. Ask for clarification if the intended behavior remains unclear.

---

# Change Principles

Before modifying existing functionality:

- Inspect and understand the current implementation.
- Identify relevant dependencies and affected components.
- Check relevant repository documentation.
- Prefer extending existing patterns over replacing working functionality.

While making changes:

- Change only what is necessary for the requested task.
- Do not refactor, reformat or improve unrelated code.
- Follow existing code style and patterns.
- Remove only dead code created by your own changes.
- Mention unrelated issues when relevant, but do not fix them unless requested.

Present a plan before significant changes and explain meaningful trade-offs.

Never implement based solely on assumptions about the repository structure.

---

# Verification

- Define what successful completion means before significant changes.
- Verify the result after implementation, in the running local environment where practical.
- For bug fixes, reproduce the issue first and confirm it is resolved.
- Include verification in multi-step implementation plans.

A task is not complete solely because the code was changed.

---

# Documentation

Repository documentation lives in `.docs/`.

Read the documents relevant to the current task before making significant changes. Verify that a
referenced document exists before relying on it.

Expected destinations:

- `.docs/development.md` for environment setup, commands and local workflow.
- `.docs/deployment.md` for deployment procedures.
- `.docs/architecture.md` for technical structure.
- `.docs/security.md` for security conventions.
- `.docs/decisions/` for repository-level decisions.

<!--
Adapt the list above to the documents this repository actually needs. Drop the ones that will never
exist here. If the rest are planned rather than written, say so in one line, for example:

    Most of these do not exist yet. Verify a document is there before relying on it.

Without that line the assistant treats the list as a set of existing files and reports them missing
as if something were broken.
-->

Project-wide documentation belongs to the canonical project repository. Do not duplicate it here.

---

# Decisions

Decisions affecting only this repository belong in `.docs/decisions/`.

Decisions affecting multiple components, multiple workstreams or the <PROJECT_NAME> project as a
whole belong to the canonical project repository.

Avoid duplicating decisions across scopes.
