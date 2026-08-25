# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
where practical.

## [0.7.0] - 2026-08-25

**A component with no address says so.** See
[decision 0007](.docs/decisions/0007-a-component-with-no-address-says-so.md).

### Added

- A fourth address form: none, said plainly, with the reason.
  `Address: none. No copy of this folder exists off this machine.` The criterion is a copy that
  exists off the machine, not version control: `git init` changes nothing here, and only a remote,
  a synced store or a containing folder that travels makes an address possible.
- `structure-check` 11 now knows what an address is and requires one of the four forms. It used to
  ask for one without saying what made one valid, which let a machine-local path into the slot and
  certified it as a pass.
- A table in the `README`, under **Filesystem boundaries**, answering "does any of this apply to me"
  in one glance. Three rows, and the first is "everything in one filesystem, nothing to do". The
  reasoning stays in `.docs/architecture.md`, which now points at the table rather than repeating it.

### Changed

- The session note is a precondition rather than a preference, and names the side from which every
  local path in the document is read. When a project spans a boundary one side usually reaches both
  and the other does not; read from the wrong side the paths are false rather than awkward.
- `.docs/architecture.md` says out loud that everything it knows about filesystem boundaries comes
  from one project, one machine and one person. A macOS setup with a network volume is expected to
  behave the same way and has not been tried.
- Blueprint versions now move only when that blueprint moves. `0.7.0` changed the project blueprint
  alone; component, repository and assets stay at `0.6.0` and carry `Framework Version: 0.7.0`.

### Rejected

- Naming the machine in the address, as `Machine-local. WSL on some-laptop`. It reads as an address,
  invites being followed, and becomes false the day the machine is replaced.
- Refusing to register such a folder at all. Under that rule `~/wordpress-7` would carry no stubs and
  no pointer to `PROJECT.md`, and the run where an assistant refused to set up a staging deployment
  and routed the decision back could not have happened.
- Reaching the WSL filesystem from Windows through `\\wsl.localhost\...` and calling that an address.
  It resolves, which is the problem: the name is a local alias, so on another machine it returns a
  different folder rather than an error.

**The accepted cost, stated plainly.** A reader on another machine gets a component's name, its
posture and a dead end. No wording produces a copy of a folder that exists in one place, and a
document implying otherwise is worse than one that says so. The gap runs one way only: the
component's own stubs still point upward with an address that resolves from anywhere, which is the
direction the framework exists for.

## [0.6.0] - 2026-08-24

A cut at what the postures carry. **Both inherit the project's principles. `Assets` adds nothing.
`Repository` adds one rule.** See
[decision 0006](.docs/decisions/0006-the-postures-carry-one-rule-between-them.md).

### Added

- One rule travelling with the word `Repository`: platform or framework core changes only through
  its own update mechanism, never by hand. The axis is ownership rather than immutability, so an
  upgrade that replaces core wholesale is the owner doing its job and a hand edit in the same files
  is not.
- `structure-check` 11 now fails a `Repository` block written without that rule, since the rule is
  the entire difference between the two words.
- A sixth thing to establish at Step 2 of the setup procedure: whether the folder holds code a
  platform or framework updates. It is the only reason to look at the contents, and it is what
  settles the posture.

### Changed

- The postures stop being opposites. `0.5.0` described them as two directions, change against
  preserve. They are a floor and one layer now, and one of them is empty.
- An `Assets` registry block reads `Assets. Live material. Work here as the task requires.`
- The component interview drops to two questions, the name and whether the folder has a rule of its
  own. The posture is proposed from what was seen and shown in the summary table as settled, where
  it can be overturned in a sentence.
- Cold start question 3 changes axis. It asked whether things get changed here or found and left
  alone. It now asks what limits what may be changed here and where that is written, which both
  postures answer only by reaching the parent.
- Cold start question 4 asks for the project boundary instead of any rule governing the folder.
  Under `0.6.0` the old question had the same answer as question 3 for an assets component, and the
  boundary is the one rule in the framework with a measured before and after.
- The assets override changes purpose. It is now where something in a live folder gets held still.
- `structure-check` 10 says what it means: an override may point at where the posture is stated and
  may not state it. The blueprint headers were rewritten so a literal reading cannot fail a correct
  file.

### Removed

- The four preserve rules: do not reorganize, do not rename, do not move, preserve the existing
  organization. An assets folder is live, and a rule that ordinary work breaks every day teaches an
  assistant that the document can be ignored.
- The posture question from the component interview. Whether platform code sits in the folder is
  visible, and `0004` forbids asking about what can be read.
- The rule about `blueprints/` from this repository's own adapters. Every blueprint file carries a
  visible notice at the top, so the rule described something already on screen, and
  `blueprints/project/README.md` forbids adapters from carrying rules at all.

**The accepted cost, stated plainly.** Nothing now stops an assistant rearranging a folder of
material on its own initiative. The rules that would have stopped it were never run: the assets
posture has not been used end to end on `0.5.0`. A folder that genuinely needs its arrangement held
is what `ASSETS.md` is for, and that is now the first real case the assets override has had.

**Closed.** Whether the two postures should collapse into one flag, and whether the pair should be
renamed. Both stay. `Repository` carries a layer that is expected to grow, and a layer that grows
needs somewhere to grow into.

### Documentation

- The project scope is described by the three states a project passes through: no documents, this
  scope alone with an empty registry, this scope with components. A single folder that has grown
  rules takes the scope on its own, and that is a finished setup rather than half of one. The old
  rule sent such a project to the component blueprint, which sends it straight back.
- `.docs/architecture.md` names the scope's second job: since `0.5.0` a component holds no document
  of its own, so a one-folder project still comes here for anything it wants to record.
- Both checks stop describing "a component that appears in no registry" as an uncovered gap. Under
  `0.5.0` such a folder is not a component at all. What is uncovered is a component whose stubs and
  registry block have drifted apart, and that needs a prompt reading both scopes at once.
- `register` becomes `registry` in `README.md` and `.docs/architecture.md`, matching every blueprint.
- The root of a project scope holds no second AI entry point, which is what the rule always meant.
  It says nothing about a `README.md` or a `LICENSE`.
- Step 2 of the setup procedure said four things and listed five.
- The `Status` section records the metric behind its numbers: non-blank lines, summed across the
  files of a scope.

## [0.5.0] - 2026-08-23

A third cut, at the number of documents rather than their contents. **The registry carries the
component; the component carries two stubs.** See
[decision 0005](.docs/decisions/0005-the-registry-carries-the-component.md).

### Added

- `blueprints/component/`, the normal way a folder is attached to a project. Two stubs, `AGENTS.md`
  and `CLAUDE.md`, identical apart from the heading. They name which component the folder is, carry
  the parent's address, and stop.
- A posture line in every registry block: `Repository` where things get changed, `Assets` where they
  are kept, and for `Assets` the four preserve rules travel with the word. This is the only thing a
  component is ever told about itself.
- An instruction in the stubs to fail loudly. An assistant that cannot reach `PROJECT.md` says so and
  stops, rather than working on whatever it can see.
- One rule that ends a whole class of setup question: a folder that has not been declared a
  component is not one. It is files, belonging to whichever component contains it and taking that
  component's posture. Being a component is a decision written into the registry, not a property of
  what sits on disk, so no tree gets surveyed for candidates.
- `blueprints/setup/new-component.md`, one prompt for any component. Three questions: what it is
  called, whether things get changed here or kept, and whether it has a rule of its own yet.
- A rule for local paths at setup: resolve the path in the exact form you mean to write, and when it
  holds only because of a symlink or mount, name that arrangement and the command that creates it. A
  `~/` path under a synced store read from another filesystem is true on the machine it was written
  on and false everywhere else, and nothing in any file records why. Observed twice: one setup run
  volunteered the symlink line, the next did not, from the same blueprint.
- Two checks. `structure-check` now verifies that the two stubs carry the same text, and that every
  registry block names a posture.

### Changed

- `REPOSITORY.md` and `ASSETS.md` are demoted from the normal way to attach a component to the
  override, for a folder that has rules of its own. Both keep `Local rules` and `Hazards` and nothing
  else.
- A registry address says where the component is, read from `PROJECT.md`. A component's stubs say
  where the parent is, read from the component. The two point opposite ways and carry different
  values, which the old component entry point hid by holding only one of them.
- The registry is authoritative. Where an override and the registry disagree about a component, the
  registry is right and the override is a bug.
- The `@` import in `CLAUDE.md` is restricted to a file in the same folder. Across a mount boundary it
  would state the parent's location a second time in a second format, and its failure mode is silent:
  a declined approval disables it permanently without saying so again.
- The cold start check for a component asks a different question. It now tests one chain end to end,
  stub to parent to the registry block, by asking whether things are changed or kept in this folder
  and what said so.

### Removed

- The component entry point as the normal case. A component holds no document of its own unless it
  has something to say that is true of it alone.
- The escalation boundary, `<PROJECT_WIDE_CONCERNS>`. It existed so a component would not walk up to
  a long parent without cause, and the parent is 33 lines. Reading it every time costs nothing.
- `Parent checked`, with the file that held it. A component holds no copy of anything in the parent
  except the address, so nothing it holds can fall out of date on its own.
- The parent address and the posture from `REPOSITORY.md` and `ASSETS.md`. Both are in the parent.
- The four preserve rules from `ASSETS.md`. They follow from the word `Assets` rather than from any
  particular folder, so they are written once in the registry.
- `blueprints/setup/new-repository.md` and `blueprints/setup/new-assets.md`, replaced by the single
  component prompt.

A component falls from three files to two and from 32 shipped lines to 22. The larger change is that
none of the 22 is a decision: two lines are the parent address and the rest are fixed text. Adding,
renaming or moving a component becomes one edit in one file.

**The accepted cost, stated plainly.** A component that cannot reach its parent now knows nothing at
all. Copying the posture down into the stub was rejected because it puts one rule in two places. The
stub fails loudly instead.

### Fixed after the validation run

The whole of `0.6.0` was validated by resetting a real project to bare folders and re-adopting it:
three scopes, three structure checks at 14/14, three cold starts at 5/5, plus two behavioural tests.
These are what the run turned up.

- `<SESSION_NOTE>` is split in two. `<PATH_NOTE>` says what makes the local path true and has nothing
  to do with components; `<SESSION_NOTE>` says where to start a session and depends entirely on them.
  A scope with no components needed the first and not the second, and one placeholder could not carry
  that. Three separate agents split them by hand during the run.
- Attaching a component now revisits the parent's session note. A scope adopted with no components
  correctly has none, and attaching one across a mount boundary makes it necessary; step 7 of the
  procedure covered only the stubs and the registry block, so nothing brought it back.
- `structure-check` 11 answers the empty registry. Two tools ran the same prompt on the same folder
  and disagreed, `n/a` against `pass`, because 11 is a presence check and the prompt tells a presence
  check with nothing to quote to fail. No blocks now passes when the document says so in visible text.
- `structure-check` 14 is no longer gated on the session note, so it can finally run. The first scope
  to carry a symlink line had no components, no boundary and no note, which left the one line holding
  its path up verified by nothing.
- `<SCOPE_EXCLUDES>` carries the undecided case. The fixed sentence had no empty form, so an agent
  improvised a replacement paragraph containing an instruction it invented. Measured on the way:
  with the boundary written as "not decided yet", two tools independently answered the boundary
  question by quoting a sentence about a component not being *attached*. An absent boundary is a
  decoy rather than a hole.
- The project-scope cold start catches up. Its question 3 still asked "changed there or kept", the
  axis this release removed, and it assumed at least one component existed.
- The three states make room for a project that has recorded nothing yet and knows a second place is
  coming. The text this release replaced carried "and no second one planned".
- "Knows nothing at all" is corrected. With its parent folder moved away, a component reported the
  failure before answering anything, found the folder at its new path, refused to open it because
  following it would be the guess the stub forbids, and named what it could not know. It is cut off
  from the posture and the principles; it is not left knowing nothing.
- The project blueprint says component state belongs to the registry alone. A sentence in "What this
  project is" saying the installation was not attached had to be repaired by hand the moment it was.
- `platforms/wordpress.md` is rewritten for `0.6.0`. It had told its reader to fill a
  `Platform Principles` section and a `<PLATFORM_PRINCIPLES>` placeholder, neither of which had
  existed since `0.5.0`, and it instructed dropping WooCommerce lines it did not contain. Used
  anyway, it produced no error: the agent mapped the old names onto the new ones silently. It now
  carries the blueprint version it was written against, and the rule about core is gone from it,
  because the registry carries that since `0.6.0`.

### Documentation

The framework's own documents were rebuilt to the shape they describe, having drifted three versions
behind it.

- `PROJECT.md` falls from 302 lines to 78 and follows the Project Blueprint. Gone with it: the
  `Project Version` counter, `Scope Ownership`, `Scope Entry Points`, `Framework Structure`,
  `Sources of Truth`, `Blueprint Lifecycle`, `Success Criteria` and `Long-Term Vision`, all of which
  described machinery that no longer exists or restated what the README already said.
- `README.md` falls from 238 lines to 130 and stops repeating `PROJECT.md`. It answers what the
  framework is for and how to adopt one; `PROJECT.md` is the entry point for working on it.
- `.docs/architecture.md` is rewritten for the current shape: why the registry cannot live anywhere
  else, what a component is told, the two address directions, and what a path spanning a mount
  boundary needs.
- The purpose is stated once, at the top of both: one roof over a project that lives in more than one
  place, one entry point holding the register, project-wide truth written once and each part
  answerable only for itself.
- Decision `0002` is marked superseded, and `0003`'s four jobs are marked as superseded by the single
  test in `0004`. Neither file is deleted; the record of why something existed outlives it.

---

## [0.4.0] - 2026-08-23

A second cut, deeper than `0.3.0` and made against a single rule instead of a list of jobs:
**a document carries what cannot be seen, and nothing that can.** See
[decision 0004](.docs/decisions/0004-documents-carry-what-cannot-be-seen.md).

### Changed

- The framework's purpose is stated as navigation. Working in one folder, an assistant reads the
  registry and reaches another that may sit on a different disk or in a different filesystem. The
  registry and the shared rules at the root are the feature; the rest supports them.
- A registry entry carries what a move needs and nothing else: name, one line, address, local path,
  entry point. Platform and production are gone from it.
- A component's own rules become one free `Local rules` section that may be left empty. The
  Repository Blueprint no longer prescribes what goes in it beyond the platform fragments.
- `Hazards` narrows again: only what an assistant cannot find by looking. Whether a `.git` exists is
  visible, so it no longer qualifies. Most components will delete the section.
- Folder naming is documented in the root `README.md`, where somebody creating a project will read
  it, rather than inside a blueprint comment. Hyphens or underscores; a space costs a pair of quotes
  in every shell command forever.

### Added

- `<SESSION_NOTE>` in the project blueprint: where to start a session so every component in the
  registry resolves, for projects whose components sit on different sides of a mount boundary. Not
  visible in any file and not inferable from one.

### Removed

- Every description of contents, from all three blueprints. An assistant can look.
- `Development Environment` and the platform, environment and URL fields with it.
- `Scope Ownership`, `Workstreams`, and the separate `Project Overview` and `Project Scope` sections,
  which merge into one short statement of what the project is and does not cover.
- The `.docs/` inventory from the component blueprints.

The text that ships into an adopted project falls from 166 lines to 88: a project scope of 33 lines,
a repository component of 25, an asset component of 30. The setup procedure falls from 320 lines to
145, because an interview cannot be longer than the fields it fills.

---

## [0.3.0] - 2026-08-22

Version `0.3.0` removes more than it adds. The framework had grown for a week until its own author
was reluctant to change it, and the cut brings it back to the four jobs it exists for. See
[decision 0003](.docs/decisions/0003-cut-the-framework-to-four-jobs.md).

### Added

- `blueprints/setup/`: prompts that adopt a blueprint by interview instead of by hand. A shared
  `procedure.md` and three thin entries, one per scope, each carrying the address of the framework
  and of every folder involved. The same file attaches a component on day one and two years later.
- `Environment hazards` in the Assets Blueprint, and a `Handling Rules` section that admits an
  exception for a subfolder holding worked code.
- A third state for the `Production` line: a component whose output somebody else deploys elsewhere.
  It writes `none` and names the handoff without naming the destination, because an address in a
  field called Production reads as a target however the prose around it is worded.
- A rule against spaces in the folder names that make up a project's path, and a note that the
  project's name and its folder need not match.
- A project scope prompt in the cold start check. The component prompt asks about a parent, a
  boundary and an unreachable parent, none of which exist at a project scope, so running it there
  returned three non-answers and measured nothing.

### Changed

- The two component kinds are told apart by what an assistant will mostly do in the folder, change
  things or find them and leave them as they are. The old rule sorted by content, "anything that is
  not a codebase", and broke on the first folder of source kept without version control.
- `<PROJECT_WIDE_CONCERNS>` now always opens with whether the request falls inside the project at
  all. No component can answer that, and without it a request the project excludes arrives looking
  like ordinary technical work. This is the one change in the release with a measured before and
  after: the same task, refused after the edit and started before it.
- Platform fragments are trimmed on adoption rather than copied in full. A rule survives if it can
  fire on work done from this folder.
- A component nested inside its project scope writes `../` and no local path at all.
- The structure check no longer fails a check that asks whether something is absent. Its evidence is
  the search that returned nothing.

### Removed

- All version counters. `Project Version`, `Repository Version`, `Component Version` and
  `Parent Project Version` are gone, along with the obligatory sweep of every component whenever the
  project document changed. A component now records `Parent checked`, the date it was last read
  against the parent, and compares it with the parent's `Last Updated`.
- `Sources of Truth` from both component blueprints, and most of `Project-Wide AI Principles` from
  the project blueprint. Both restated behaviour a competent assistant already has.
- Half of `Change Principles` and most of `Verification`. What survives is the part that is not a
  default: change only what the task needs, remove only your own dead code, reproduce a bug before
  fixing it.
- `Environment access` from the Repository Blueprint. Two paragraphs that never changed an outcome.
- `Development Environment` from the Repository Blueprint. Platform, environment and local URL are
  read off the files, and the parent registry already records the platform and the deployed location
  of every component. `Environment hazards` becomes `Hazards` and narrows to what no file shows and
  no tool catches, which for most repositories is nothing at all.
- `Change Principles` from the Repository Blueprint. The six lines that survived the first cut moved
  up to `Decision Rules` in the project blueprint, under a subsection for components holding code, so
  a new code component inherits them instead of carrying its own copy.

The text that ships into an adopted project falls from 272 lines to 166, and a component entry
point from 100 lines to 45.

---

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
