# 0001. A project scope need not be a repository

**Date:** 2026-08-09  
**Status:** accepted

---

## Context

`Cross-Scope References` requires a reference to another scope to carry an address that resolves
from where it is read, and names a repository URL as the form that qualifies. `.docs/architecture.md`
draws the conclusion: hosting the project scope in a repository of its own satisfies this even when
it holds no code.

ArtGlina ran that arrangement and abandoned it. The project scope was a repository holding one
document and an empty decisions folder, while every project-level artefact that had files, meaning
branding, photography, contracts and marketing material, sat in a synced folder elsewhere. The
repository was a scope with no territory, and its owner could not hold the arrangement in his head.
The project scope moved into the folder that already held the material.

The move was correct for that project and the framework had no room for it.

## Decision

A project scope may live anywhere it has an address that resolves from outside the machine it sits
on. A repository is one such place. An account-relative location in a synced store, written as
`OneDrive, Projects/Artglina`, is another: it resolves on any machine signed in to the same account
and names no username.

What the rule protects is reachability. Requiring a repository was a proxy for that, and the proxy
excluded a valid arrangement.

## Consequences

The framework gains a second recognized address form, and with it a case where a component sits
inside its parent's folder rather than apart from it. Such a component references its parent by
relative path, which is the simplest address of the three and was previously unavailable.

`Sources of Truth` is unaffected. A project scope outside version control loses history and review
on the document that governs everything, which is a real cost and belongs to the project that
chooses it rather than to the framework.

## Follow-up

All five were applied in `0.2.0`, together with three gaps found while applying them: the Assets
Blueprint stated when project context was required and never when it was not, both adoption guides
were silent about adapters taking no additions, and the cold start check treated a run in one tool
as sufficient when the adapters exist precisely because tools differ.

The original list, for the record:

1. `PROJECT.md`, `Cross-Scope References`. States that a repository URL qualifies and does not
   admit the second form.
2. `.docs/architecture.md`, closing paragraph. Draws the repository conclusion outright.
3. `blueprints/checks/structure-check.md`, check 7. Demands the parent project's repository as a
   full URL, so it fails a correct adoption under this decision.
4. `blueprints/repository/`. Prose, the `<CANONICAL_PROJECT_REPOSITORY_URL>` placeholder name, and
   the `Documentation` and `Decisions` sections all read as though the parent is a repository.

A fifth item is smaller and unrelated to addressing. A `~/` path hint resolves in one environment
and not another when the same folder is reached through a mount, as with WSL reading a Windows
OneDrive folder. A symlink at the written location makes one written form true everywhere, and both
blueprints should say so rather than leaving the hint half broken.

## Origin

ArtGlina, 2026-08-09. Items 3 and 4 were found by the assistant performing the adoption, which
reported that the blueprint and the project scope disagreed and followed the project scope.
