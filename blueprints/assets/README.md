# Assets Component Blueprint

Reusable blueprint for an asset component: a folder or storage location holding non-code project
resources such as photography, video, design files and business documents.

**Blueprint Version:** 0.1.0  
**Framework Version:** 0.0.1  
**Status:** derived from a working implementation, reviewed, in use in one project. Not yet
validated in a second project, so the contract is not considered stable.

---

## Files

| File | Role |
| --- | --- |
| `ASSETS.md` | Canonical entry point for the asset component. |
| `AGENTS.md` | Adapter. Points AI tools to `ASSETS.md`. |
| `CLAUDE.md` | Adapter for Claude. Points to `ASSETS.md` and imports it where supported. |

Copy all three into the target component. Do not copy this `README.md`.

---

## Placeholders

| Placeholder | Meaning |
| --- | --- |
| `<PROJECT_NAME>` | Name of the parent project. |
| `<CANONICAL_PROJECT_REPOSITORY_URL>` | URL of the repository holding the canonical `PROJECT.md`. |
| `<RECOMMENDED_LOCAL_CHECKOUT_PATH>` | Conventional local path of that checkout. Relative to the home directory, never a machine-specific absolute path. |
| `<COMPONENT_VERSION>` | Version of this component's entry point. Start at `1.0`. |
| `<PARENT_PROJECT_VERSION>` | Version of `PROJECT.md` this document was written against. Drift indicator. |
| `<ASSETS_BLUEPRINT_VERSION>` | Blueprint version this component was derived from. Currently `0.1.0`. |
| `<YYYY-MM-DD>` | Date of the last update. |
| `<DOCUMENT_OWNER>` | Person responsible for this document. |

---

## How to adopt

1. Copy `ASSETS.md`, `AGENTS.md` and `CLAUDE.md` into the asset component.
2. Delete the blueprint notice at the top of each file.
3. Replace every placeholder.
4. Adapt the contents list in `Component Context` to what the component actually holds.
5. Leave `Asset Management Principles` as it is until the asset structure is formalized, then
   replace that section with the real structure.

---

## Versioning

Blueprint-level metadata stays in this file and is not copied into adopted components:

- **Blueprint Version** tracks this blueprint.
- **Framework Version** records the AI Project Template version it is compatible with.

Adopted components carry only what their owner needs:

- **Component Version** tracks the component's own entry point.
- **Parent Project Version** records the `PROJECT.md` version the component was written against and
  acts as a drift indicator.
- **Derived from** records the blueprint version the component started from.

When the parent `PROJECT.md` changes, the component owner compares the change against the component:

- If the change affects the component, update the document, raise `Component Version`, and set
  `Parent Project Version` to the new parent version.
- If it does not, set `Parent Project Version` to the new parent version and leave
  `Component Version` unchanged. This records that compatibility was checked rather than assumed.

---

## Design notes

The asset component is a component scope, so it carries its own canonical entry point and points
upward to the project scope rather than restating project-wide rules.

Two behaviours are deliberate and worth keeping when adapting:

- **Graceful fallback.** If project-wide context is unavailable, the assistant asks instead of
  inventing requirements. Canonical project repositories are often private and unreachable by URL,
  so this path fires in practice.
- **Do not reorganize.** Asset folders accumulate informal structure that carries meaning the
  assistant cannot see. Reorganization stays opt-in until a structure is formally defined.

---

## Origin

Generalized from the ArtGlina Project Assets component, which went through several review rounds
before being extracted here.
