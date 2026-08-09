# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
where practical.

## [0.2.0] - 2026-08-09

### Added

- Project Scope Blueprint `0.1.0`, derived from one working implementation. Covers the scope that
  holds project-wide context, the registry of the components below it, and the address those
  components point at. It is the only scope that publishes an address rather than consuming one, and
  the only one with no parent, which changes how both checks read against it.
- Decision `0001`: a project scope need not be a repository. Recorded in `.docs/decisions/` with the
  reasoning and the five places that still assumed the old form.
- Two further address forms in `Cross-Scope References`: an account-relative location in a synced
  store, and a relative path when the referenced scope contains the referring one. A repository URL
  remains the first of three rather than the only one.
- `Where the component sits` in the Assets Blueprint: the case of a component nested inside its
  parent's folder, which addresses the parent as `../` and carries no local path at all.
- `Paths across a mount boundary` in both blueprints. A `~/` hint can be true in one environment and
  false in another when the same folder is reached through a mount, and a symlink at the written
  location makes one written form true everywhere.
- A stated escalation boundary in the Assets Blueprint, with a `<PROJECT_WIDE_CONCERNS>` placeholder.
  The blueprint previously said when project context was required and never when it was not, so it
  failed the structure check's own question 9.
- Adapter purity in both adoption guides. Adapters redirect and stop, and anything added to one
  restates what the entry point or the framework already says.
- `Which one you need` in `README.md`: what separates the three blueprints in plain terms, the root
  against the codebase against everything else.
- Rule that an entry point is named for the kind of scope it opens and not for its subject, which
  fixes the set of names at three. A folder organized by workstream is an asset component and
  carries `ASSETS.md`; there is no `MARKETING.md`. Without this, the name slot collects topics and
  the set grows with every new area of work.
- `On a project scope` in the structure check: questions 7, 9 and 10 do not apply where there is no
  parent, and question 11 matters most.
- `A second tool` in the cold start check. The adapters exist because tools look for different
  filenames, so a run in one tool proves only the file that tool opened.

### Changed

- `<CANONICAL_PROJECT_REPOSITORY_URL>` renamed to `<CANONICAL_PROJECT_SCOPE_ADDRESS>` in both
  blueprints, and `<RECOMMENDED_LOCAL_CHECKOUT_PATH>` to `<PARENT_PROJECT_LOCAL_PATH>`. The old names
  named a git artefact and prescribed the answer.
- Structure check question 7 now asks for an address that resolves from outside the machine rather
  than for a repository URL. In its previous form it failed a correct adoption.
- `canonical project repository` replaced with `project scope` throughout both blueprints, including
  the `Documentation` and `Decisions` sections and the design notes.
- Both blueprints raised to `0.2.0`, and the WordPress fragment now names that version.

### Notes

- Every change here comes from one live adoption. A project scope that held one document while all
  its real material sat elsewhere was collapsed into the folder that held the material, and the
  framework had no room for the result.
- The Project Scope Blueprint was released against the owner's judgement rather than the usual
  caution. Its implementation is one day old and has not been lived with, so it is the least settled
  of the three and its README says so. If the arrangement does not hold, this is the blueprint that
  will move first.

## [0.1.0] - 2026-08-09

### Added

- `Scope Entry Points` section: the adapter rule, now stated for every scope rather than for the
  repository root only, and the separation between framework entry point names and the filenames
  external tools discover.
- Rule that a document name belongs to exactly one type of scope, which rules out placing a pointer
  named after another scope's entry point inside a smaller scope.
- `Cross-Scope References` section: a reference to another scope carries a resolvable address, which
  constrains where a referenced scope is allowed to live.
- Rule that a scope states when parent context is actually required.
- Three matching entries in `Design Philosophy`.

- Repository Component Blueprint `0.1.0`, derived from one working implementation. Covers a
  repository that is one component of a larger project.
- Platform fragment library inside the Repository Blueprint, starting with WordPress. Platform rules
  live in one replaceable section, so the blueprint itself stays technology-agnostic.
- `Blueprint Comments` convention: an HTML comment marks an unresolved decision, addresses the
  person adopting the blueprint, and is removed once worked through. Uncommented text is ready to
  use as it stands.
- `Comments` section and a final comment-removal step in both blueprint adoption guides.
- `Example` column in both placeholder tables, and a `Paths` section explaining the home-relative
  form. Every placeholder now has a concrete example.
- Rule at project scope that a local path accompanying an address is written relative to the home
  folder and never with a username: `~` already stands for the folder that contains it.
- An example in every replace-type blueprint comment, including a filled-in header block and the
  address pair that makes the upward reference work.
- `blueprints/checks/`: two prompts for verifying an adoption, shared by every blueprint. The
  structural audit returns a table where every row carries a file and line quote and an unevidenced
  check counts as failed. The cold start check tests whether an assistant opening the folder for the
  first time follows the chain, and states the conditions that make the run valid.
- `Adoption Checks` section in `PROJECT.md` recording why both checks return evidence rather than a
  verdict.
- `.gitattributes` normalizing line endings to LF.

### Changed

- Assets Blueprint raised to `0.1.1`: comment handling, placeholder examples, and address and path
  guidance in `ASSETS.md`.

### Notes

- These rules come from applying the framework to a live project, where an unaddressed reference to
  a parent scope turned out to be unusable in practice.
- The Assets Blueprint already satisfied the new rules and did not change.
- A standalone repository with no parent project is outside the Repository Blueprint's scope for
  now.

## [0.0.1] - 2026-08-08

### Added

- Core framework documentation and the canonical `PROJECT.md` entry point.
- Root `AGENTS.md` and `CLAUDE.md` adapters for AI tools.
- Assets Component Blueprint `0.1.0`, derived from one working implementation.
- Blueprint versioning and parent-project drift-check procedure.
- MIT license.

### Notes

- The framework is in early development; its contract is not yet stable.
- Repository and Project blueprints, reference examples, and documentation guides are planned.
