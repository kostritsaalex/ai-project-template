# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
where practical.

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
