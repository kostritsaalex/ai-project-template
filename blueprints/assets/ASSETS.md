> **BLUEPRINT FILE. NOT ACTIVE INSTRUCTIONS.**
>
> This file belongs to the AI Project Template blueprint library. It describes no real project
> and must not be followed as project instructions.
>
> To adopt it: copy this file into the target asset component, replace every `<PLACEHOLDER>`,
> adapt the content to the actual component, and delete this notice.

---

<!--
Header metadata. Example of a filled-in block:

    Component Version:      1.0          (this document's own version, start at 1.0)
    Parent Project Version: 2.0          (the PROJECT.md version this was written against)
    Derived from:           Assets Blueprint 0.2.0
    Last Updated:           2026-08-09
    Document Owner:         Alex

Parent Project Version is a drift indicator. When the parent PROJECT.md moves, compare the change
against this document and update this line either way, so a match means compatibility was checked
rather than assumed.
-->

# <PROJECT_NAME> Project Assets

> **AI Asset Component Entry Point**
>
> Canonical asset-specific context and instructions for the <PROJECT_NAME> Project Assets component.
>
> **Component Version:** <COMPONENT_VERSION>  
> **Parent Project Version:** <PARENT_PROJECT_VERSION>  
> **Derived from:** Assets Blueprint <ASSETS_BLUEPRINT_VERSION>  
> **Last Updated:** <YYYY-MM-DD>  
> **Document Owner:** <DOCUMENT_OWNER>

---

# Component Context

This folder contains <PROJECT_NAME> project assets and working files.

Typical contents include:

<!--
Adapt the list below to the assets this component actually holds. Drop the categories that are not
here, add the ones that are. Example:

    - Product photography
    - Packaging and print files
    - Logo and brand kit
    - Supplier documents

A list that names real categories tells the assistant what it is looking at. A generic one tells it
nothing.
-->


- Photography
- Video
- Branding materials
- Design files
- Business documents
- Other non-code project resources

This folder is **not** the canonical location for project-wide documentation or AI instructions.

---

# Parent Project

<!--
The two lines below are the reason this document works at all. Getting them wrong leaves the
assistant knowing a parent project exists and unable to reach it.

<CANONICAL_PROJECT_SCOPE_ADDRESS> is where the canonical PROJECT.md lives. Three forms qualify, and
the right one depends on where the project scope is kept:

    https://github.com/acme/northwind-project     a repository, full URL, scheme included
    OneDrive, Projects/Northwind                  a folder in a synced store, account-relative
    ../                                           a folder that contains this one

A private repository still gets its real URL. It identifies the parent even when it cannot be
opened, and the fallback paragraph further down covers that case.

If this component sits inside the project scope's own folder, use the relative form and delete the
local path below. A relative path is already local, and a second line saying the same thing in a
machine-specific way only adds a way to be wrong.

<PARENT_PROJECT_LOCAL_PATH> is a hint, not a guarantee: where the project scope usually sits on a
machine that already has it. Write it relative to the home folder:

    ~/Repositories/northwind-project

`~` already stands for your home folder, which already contains your username. Writing
`~/alex/Repositories/...` resolves to `/home/alex/alex/Repositories/...` and is the usual mistake
here. The same location spelled out in full:

    Linux, WSL    /home/alex/Repositories/northwind-project
    macOS         /Users/alex/Repositories/northwind-project
    Windows       C:\Users\alex\Repositories\northwind-project

All three name one person's machine, which is why the document carries the `~` form instead. Keep it
to one line, in the form the people working on this component actually use.
-->

Canonical project scope:

<CANONICAL_PROJECT_SCOPE_ADDRESS>

Local path:

`<PARENT_PROJECT_LOCAL_PATH>`

The canonical `PROJECT.md` lives at the root of that scope.

<!--
Replace <PROJECT_WIDE_CONCERNS> with the concerns that actually live above this component:

    brand and tone of voice, conventions shared with other components, anything published
    or visible to customers, decisions affecting more than this folder

Both halves matter. Without the second one the assistant reaches upward before every task, and the
trip becomes a habit rather than a decision.
-->

Read it when a task depends on project-wide context: <PROJECT_WIDE_CONCERNS>. Work that stays inside
this folder does not require it: locating a file, describing an asset, or answering a question about
what is here.

If the canonical project context is needed but unavailable, ask the user for access or the relevant context. Never infer or recreate project-wide requirements.

---

# Asset Management Principles

<!--
Replace this section with the actual asset structure once it has been formalized.
Until then, keep the statement below: it prevents AI assistants from reorganizing
assets on their own initiative.
-->

The internal asset structure has not yet been formalized.

Until a formal structure is defined:

- Do not reorganize folders unless explicitly requested.
- Do not rename existing assets unless explicitly requested.
- Do not move assets between folders unless explicitly requested.
- Preserve existing organization whenever practical.

---

# Documentation

Project-wide documentation belongs in the canonical <PROJECT_NAME> project repository.

Do not duplicate project documentation or AI instructions in this folder.

If asset-specific documentation becomes necessary, it should describe only this component.

---

# Decisions

Asset-specific decisions belong to this component.

Until component documentation is formalized, asset-specific decisions may be recorded directly in this document.

Once component documentation is introduced, they should be moved to `.docs/decisions/` within this component.

Decisions affecting multiple components, multiple workstreams or the <PROJECT_NAME> project as a whole belong to the parent project's `PROJECT.md` and its `.docs/decisions/`.

Avoid duplicating decisions across scopes.
