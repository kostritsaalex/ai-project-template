# Repository Component Blueprint

Reusable blueprint for a code repository that is one component of a larger project: a website, an
application, a service, a library maintained alongside other components.

**Blueprint Version:** 0.1.0  
**Framework Version:** 0.1.0  
**Status:** derived from a working implementation, reviewed, in use in one repository. Not yet
validated in a second repository or on a second platform, so the contract is not considered stable.

---

## Scope

This blueprint covers a repository that belongs to a parent project and points upward to it.

A standalone repository with no parent project is not covered. That case raises a separate question,
whether `PROJECT.md` and `REPOSITORY.md` collapse into one document, and it has not been worked
through yet.

---

## Files

| File | Role |
| --- | --- |
| `REPOSITORY.md` | Canonical entry point for the repository. |
| `AGENTS.md` | Adapter. Points AI tools to `REPOSITORY.md`. |
| `CLAUDE.md` | Adapter for Claude. Points to `REPOSITORY.md` and imports it where supported. |
| `platforms/` | Ready-made platform fragments. Not copied as files; their contents go into one section. |

Copy the first three into the repository root. Do not copy this `README.md` or the `platforms/`
folder.

---

## Placeholders

Examples use a fictional `Northwind` project throughout.

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<REPOSITORY_NAME>` | Human-readable name of this repository. | `Northwind Storefront` |
| `<REPOSITORY_PURPOSE>` | What the repository holds and what it produces, in one or two sentences. | `the Northwind storefront: the English-language shop at https://shop.northwind.example` |
| `<PROJECT_NAME>` | Name of the parent project. | `Northwind` |
| `<CANONICAL_PROJECT_REPOSITORY_URL>` | URL of the repository holding the canonical `PROJECT.md`. Full URL, scheme included. Private repositories still get their real URL. | `https://github.com/acme/northwind-project` |
| `<RECOMMENDED_LOCAL_CHECKOUT_PATH>` | Where that checkout usually sits. A hint, not a guarantee. Relative to the home folder, never with a username spelled out. | `~/Repositories/northwind-project` |
| `<PROJECT_WIDE_CONCERNS>` | The concerns that live above this repository and justify reading the parent `PROJECT.md`. | `brand and tone of voice, conventions shared with other components, anything visible to end users` |
| `<PLATFORM>` | Technology the repository is built on. | `Django + Wagtail` |
| `<LOCAL_ENVIRONMENT>` | How the local environment runs. | `Docker Compose on WSL Ubuntu` |
| `<LOCAL_DEVELOPMENT_URL>` | Address of the local environment. | `https://northwind.test` |
| `<PRODUCTION_URL>` | Address of the deployed result. | `https://shop.northwind.example` |
| `<ENVIRONMENT_HAZARDS>` | Conditions the assistant cannot infer from the files. Delete the section if none apply. | `The staging database shares credentials with production.` |
| `<PLATFORM_PRINCIPLES>` | Replaced by a fragment from `platforms/`, or by rules written for the platform in use. | contents of `platforms/wordpress.md` |
| `<REPOSITORY_VERSION>` | Version of this repository's entry point. Start at `1.0`. | `1.0` |
| `<PARENT_PROJECT_VERSION>` | Version of `PROJECT.md` this document was written against. Drift indicator. | `2.0` |
| `<REPOSITORY_BLUEPRINT_VERSION>` | Blueprint version this repository was derived from. Currently `0.1.0`. | `0.1.0` |
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
one line, matching how the people working on this repository actually keep their checkouts.

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
- **Keep.** The comment says the paragraph next to it holds regardless of platform or project.
  Leave the paragraph, delete the comment.

Either way the comment goes. It speaks to you, not to the finished document.

Nothing that has to survive adoption may stay inside a comment. If a decision is being deferred,
write the deferral in visible text, the way `Repository Context` states what the repository holds
rather than hinting at it.

A leftover comment is worse than it looks. It disappears from the rendered document, so a human
reviewing the result never sees it, while an AI tool reads the raw file and treats
`Replace this section with...` as a task waiting to be done.

---

## How to adopt

1. Copy `REPOSITORY.md`, `AGENTS.md` and `CLAUDE.md` into the repository root.
2. Read each file end to end before changing anything.
3. Delete the blueprint notice at the top of each file.
4. Replace every placeholder.
5. Fill `Platform Principles` from `platforms/`, or write the rules for the platform in use.
6. Fill `Environment hazards`, or delete the section if nothing applies.
7. Adapt the `.docs/` list to the documents this repository actually needs, and say which of them do
   not exist yet.
8. Move commands and setup procedures out of `REPOSITORY.md` into `.docs/development.md`.
9. Work through every remaining comment and delete it.

Before committing, search the adopted files for `<!--` and for `<` followed by a capital letter.
Both searches should return nothing.

---

## Verify the adoption

Two prompts in [`../checks/`](../checks/) verify the result. Both refer to a canonical entry point;
for this blueprint that is `REPOSITORY.md`.

1. [Structure check](../checks/structure-check.md). Leftovers, addresses, adapter wiring. Returns a
   table where every row carries a quote. Run it right after adoption.
2. [Cold start check](../checks/cold-start-check.md). Whether an assistant opening the repository
   for the first time picks up the context. Run it in a new session once the structure check passes.

Do not skip the second one. The first says the files are well formed, which is not the same as the
chain working.

---

## Versioning

Blueprint-level metadata stays in this file and is not copied into adopted repositories:

- **Blueprint Version** tracks this blueprint.
- **Framework Version** records the AI Project Template version it is compatible with.

Platform fragments carry their own version and evolve on their own schedule.

Adopted repositories carry only what their owner needs:

- **Repository Version** tracks the repository's own entry point.
- **Parent Project Version** records the `PROJECT.md` version the repository was written against and
  acts as a drift indicator.
- **Derived from** records the blueprint version the repository started from.

When the parent `PROJECT.md` changes, the repository owner compares the change against the
repository:

- If the change affects the repository, update the document, raise `Repository Version`, and set
  `Parent Project Version` to the new parent version.
- If it does not, set `Parent Project Version` to the new parent version and leave
  `Repository Version` unchanged. This records that compatibility was checked rather than assumed.

---

## Design notes

The repository is a component scope, so it carries its own canonical entry point and points upward
to the project scope rather than restating project-wide rules.

Five behaviours are deliberate and worth keeping when adapting:

- **An addressed pointer upward.** The `Parent Project` section names a URL and a conventional
  checkout path. Naming the parent project without an address leaves the assistant aware that
  context exists and unable to reach it, which is what the earlier draft of this pattern did.
- **A stated escalation boundary.** The same section says which concerns justify reading the parent
  `PROJECT.md`. Without it, every change turns into a trip upward.
- **Graceful fallback.** If project-wide context is unavailable, the assistant asks instead of
  inventing requirements. Canonical project repositories are often private and unreachable by URL,
  so this path fires in practice.
- **Environment access is not assumed.** An assistant with a sandboxed shell will believe it has the
  development environment and work against nothing. The rule says a terminal is not the same as
  access to this machine.
- **Environment hazards are written down.** A second checkout sharing a Git remote, a staging
  database wired to production credentials: none of it is visible in the files, so it has to be
  stated.

Platform rules sit in one section rather than being spread through the document, which keeps them
replaceable. The framework itself stays technology-agnostic, and `platforms/` holds the specifics.

---

## Origin

Generalized from a WordPress and WooCommerce storefront repository that is one component of a
multi-component project. The upward pointer in that repository failed in its first form, which is
where the address and escalation-boundary rules come from.
