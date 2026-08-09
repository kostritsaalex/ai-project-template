# Assets Component Blueprint

Reusable blueprint for an asset component: a folder or storage location holding non-code project
resources such as photography, video, design files and business documents.

**Blueprint Version:** 0.1.1  
**Framework Version:** 0.1.0  
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

Examples use a fictional `Northwind` project throughout.

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<PROJECT_NAME>` | Name of the parent project. | `Northwind` |
| `<CANONICAL_PROJECT_REPOSITORY_URL>` | URL of the repository holding the canonical `PROJECT.md`. Full URL, scheme included. Private repositories still get their real URL. | `https://github.com/acme/northwind-project` |
| `<RECOMMENDED_LOCAL_CHECKOUT_PATH>` | Where that checkout usually sits. A hint, not a guarantee. Relative to the home folder, never with a username spelled out. | `~/Repositories/northwind-project` |
| `<COMPONENT_VERSION>` | Version of this component's entry point. Start at `1.0`. | `1.0` |
| `<PARENT_PROJECT_VERSION>` | Version of `PROJECT.md` this document was written against. Drift indicator. | `2.0` |
| `<ASSETS_BLUEPRINT_VERSION>` | Blueprint version this component was derived from. Currently `0.1.1`. | `0.1.1` |
| `<YYYY-MM-DD>` | Date of the last update. | `2026-08-09` |
| `<DOCUMENT_OWNER>` | Person responsible for this document. | `Alex` |

### Paths

`~` stands for the home folder, and the home folder already contains the username. So the username
is never written after it:

```text
~/Repositories/northwind-project        correct
~/alex/Repositories/northwind-project   resolves to /home/alex/alex/Repositories/...
```

The same location written out in full, for orientation:

```text
Linux, WSL    /home/alex/Repositories/northwind-project
macOS         /Users/alex/Repositories/northwind-project
Windows       C:\Users\alex\Repositories\northwind-project
```

All three name one person's machine, so none of them belong in the document. Write the `~` form,
one line, matching how the people working on this component actually keep their checkouts.

If the team works across several operating systems, still write one line. The path is a hint about
where to look, and the URL above it is the address that always works.

---

## Comments

Read the whole document before adopting it, then treat the comments as the work.

An HTML comment marks a place where a decision is yours to make. Text without a comment is ready to
use as it stands, and most of the document is that kind of text.

Comments come in two kinds:

- **Replace.** The comment describes what belongs there. Write it, then delete the comment and the
  placeholder next to it.
- **Keep.** The comment says the paragraph next to it holds as written. Leave the paragraph, delete
  the comment.

Either way the comment goes. It speaks to you, not to the finished document.

Nothing that has to survive adoption may stay inside a comment. The comment above
`Asset Management Principles` is the example: it explains why the section exists, and the section
itself already states in visible text that no formal structure is defined yet. Deleting the comment
loses nothing.

A leftover comment is worse than it looks. It disappears from the rendered document, so a human
reviewing the result never sees it, while an AI tool reads the raw file and treats
`Replace this section with...` as a task waiting to be done.

---

## How to adopt

1. Copy `ASSETS.md`, `AGENTS.md` and `CLAUDE.md` into the asset component.
2. Read each file end to end before changing anything.
3. Delete the blueprint notice at the top of each file.
4. Replace every placeholder.
5. Adapt the contents list in `Component Context` to what the component actually holds.
6. Leave `Asset Management Principles` as it is until the asset structure is formalized, then
   replace that section with the real structure.
7. Work through every remaining comment and delete it.

Before committing, search the adopted files for `<!--` and for `<` followed by a capital letter.
Both searches should return nothing.

---

## Verify the adoption

Two prompts in [`../checks/`](../checks/) verify the result. Both refer to a canonical entry point;
for this blueprint that is `ASSETS.md`.

1. [Structure check](../checks/structure-check.md). Leftovers, addresses, adapter wiring. Returns a
   table where every row carries a quote. Run it right after adoption.
2. [Cold start check](../checks/cold-start-check.md). Whether an assistant opening the component for
   the first time picks up the context. Run it in a new session once the structure check passes.

Do not skip the second one. The first says the files are well formed, which is not the same as the
chain working.

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
