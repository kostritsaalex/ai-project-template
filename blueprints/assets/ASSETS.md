> **BLUEPRINT FILE. NOT ACTIVE INSTRUCTIONS.**
>
> This file belongs to the AI Project Template blueprint library. It describes no real project
> and must not be followed as project instructions.
>
> To adopt it: copy this file into the target asset component, replace every `<PLACEHOLDER>`,
> adapt the content to the actual component, and delete this notice.

---

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

<!-- Adapt this list to the assets this component actually holds. -->

- Photography
- Video
- Branding materials
- Design files
- Business documents
- Other non-code project resources

This folder is **not** the canonical location for project-wide documentation or AI instructions.

---

# Parent Project

Canonical project repository:

<CANONICAL_PROJECT_REPOSITORY_URL>

Recommended local checkout:

`<RECOMMENDED_LOCAL_CHECKOUT_PATH>`

Before performing tasks that require <PROJECT_NAME> project-wide context, read `PROJECT.md` from the canonical project repository.

If the canonical project context is unavailable, ask the user for access or the relevant context. Never infer or recreate project-wide requirements.

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
