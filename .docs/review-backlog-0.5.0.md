# Review backlog, 0.5.0

Two external reviews of `ai-project-template` at `v0.5.0`, plus a verification pass over every claim
in them. Dated 2026-08-23.

> **Worked through on 2026-08-24 and released as `0.6.0`.** Every row marked Now is done. The rows
> about the `Assets` posture were settled the other way: the postures now carry one rule between
> them, recorded in
> [decision 0006](decisions/0006-the-postures-carry-one-rule-between-them.md). The scope criterion
> was rewritten around the three states a project passes through rather than around component count.
>
> Still open, and unchanged by that release: the third check, the second razor for rules, where
> platform rules live, splitting `<SESSION_NOTE>`, tightening `structure-check` 11 against the exact
> registry text, separating "cannot find" from "cannot open" in the stub, and the breaking tests.
> `platforms/wordpress.md` is still broken and still waiting on the platform question.

Every row was checked against the files rather than against the review text. Where a reviewer was
wrong, the row says so and gives the measurement that settled it.

**Sources in the table**

- `[R1]` first review, the line-by-line one
- `[R2]` second review, the architectural one
- `[V]` found during verification, in neither review

**Priority**

| Level | Meaning |
| --- | --- |
| Now | Cheap text fix that catches a real error. No architecture involved. |
| Release | Needs a decision or a test before it can be written. |
| Later | Cosmetic, or a question worth deferring. |
| No action | Verified and rejected. Kept so it is not raised a third time. |

---

## The table

| Item | Verdict | Priority |
| --- | --- | --- |
| `[R1]` `platforms/wordpress.md` is broken. It says to fill a `Platform Principles` section and a `<PLATFORM_PRINCIPLES>` placeholder; `REPOSITORY.md` 0.5.0 has `Local rules` and `<LOCAL_RULES>`. Header still reads `For: Repository Blueprint 0.2.0` (`wordpress.md:4,7,8`) | Agreed, verified. Fixing the headings alone is treating the symptom: the fragment rotted because platform rules have no owner. Mark it stale now, fix properly once the platform question is settled | Now |
| `[R1]` `procedure.md:41` promises "four things" and lists five. The fifth is the newest and the one that gets dropped | Agreed. One word | Now |
| `[R1]` `register` against `registry`. The two entry documents use a word the blueprints do not | Agreed, different counts: `README.md` uses `register` 7 times, `.docs/architecture.md` 6 times, and both also use `registry` once. The split runs inside each file, not only between files | Now |
| `[R1]` The line counts disagree: 33 in decision 0005, 40 in `README.md`, both about 0.5.0 | **Wrong.** Measured: the `PROJECT.md` skeleton is 33 non-blank lines, `AGENTS.md` 3, `CLAUDE.md` 4. 33 + 7 = 40. One metric, no conflict. What is broken is a term: `.docs/architecture.md:95` defines the entry point as `PROJECT.md` alone, and `README.md:113` uses the same word for all three files | Release |
| `[R1]` The `Assets` posture forbids reorganizing, renaming and moving, and says nothing about editing a file in place | Agreed, and the hole is worse than described. "Find them and leave them as they are" lives in `README.md` and `.docs/architecture.md`, neither of which ships. What ships is the registry line (`blueprints/project/PROJECT.md:119`), and it carries four rules about organization only | Now |
| `[R1]` The registry repeats the preserve sentence in every asset block. Principle 5 broken inside one file | Partly. The fact holds. The proposed fix (define the postures once in the section header, leave one word in the block) moves the rule away from where it is read. Cheaper: tighten `structure-check` 11 to compare the exact text instead of checking that a word is present | Release |
| `[R1]` "Say so and stop" plus a private repository means a component that must refuse everything, forever | Partly, overstated. The stub also carries a local path, which usually resolves. The real defect is narrower: the stub does not separate "cannot locate the parent" from "located it, cannot open it from here", and `stop` blocks reading and questions as well as changes. Their fix (bind `stop` to changes) is right | Release |
| `[R1]` Add a third check: walk the registry, open each component's stubs, compare the parent address and the component name against the registry block | Agreed on the check, not on its target. The second hole they name, a folder on disk that appears in no registry, was closed by definition in `0005:53`: an undeclared folder is not a component. The check runs in one direction, registry to disk | Release |
| `[R1]` The razor cuts facts and cannot cut rules, so the registry will grow. The guard sentence sits in a comment that adoption deletes (`blueprints/project/PROJECT.md:136`) and in decision `0005:99`, which nobody reads at setup | Agreed, and this is the most valuable thing in either review. Their fix (promote the sentence to `README.md` and `.docs/architecture.md`) is weak: it draws a line between reaching a component and working inside one, which is not a test of whether a rule earns a document at all. A second razor is needed. Candidate: a rule belongs in a document only if an assistant would do otherwise without it. That is a hypothesis, and "The stronger version" in `cold-start-check.md:149` is the instrument that decides it | Release |
| `[R1]` The rule "one component means no project scope" (`blueprints/project/README.md:14`, `new-project.md:43`) is refuted by this repository, which has zero components and keeps `PROJECT.md` | Agreed, and it costs more than they say. In 0.4.0 a component had an entry point of its own, so a boundary could go there. 0.5.0 removed it, so a one-component project with no scope has nowhere at all to write `SCOPE_EXCLUDES`, which `0004:39` calls the only rule in the framework with a measured before and after. Rewrite the criterion: a scope is needed when there is more than one place, **or** a project boundary to record | Now |
| `[R1]` A component has no provenance. `Derived from` exists on the project scope and on an override, and stubs carry nothing, so components built before 0.5.0 cannot be found | Disagreed on the remedy. Putting metadata back into a shipped file is what `0002` and `0003` cleaned out. Old stubs are findable with `git grep` on the fixed sentence, since the text is identical everywhere. What is worth writing down is the asymmetry itself: `PROJECT.md` is maintained by a person and dated, a stub is fixed text | Later |
| `[R1]` Question 4 of the component cold start collapses into question 3 for a `Repository` component with no override | Partly. The only answer left is a project principle, and the question does not say so | Later |
| `[R1]` `<SESSION_NOTE>` (`blueprints/project/PROJECT.md:99`) holds two unrelated things: where to start a session, and what makes the local path true | Agreed. Split into two placeholders | Release |
| `[R2]` Dogfooding argues with the rule. The architecture says a scope exists for the registry and a project with one place does not need one; this repository applies the blueprint to itself and writes "This project has none" | Agreed, same item as the `[R1]` row above. Their proposed wording is softer than what is needed: the rule itself should change, not only its phrasing | Now |
| `[R2]` "The root holds those three and nothing else" (`blueprints/project/README.md:32`) reads as a ban on `README.md`, `LICENSE` and ordinary project files | Agreed, and this repository breaks the sentence as written. Narrow it to "no second AI entry point in the root" | Now |
| `[R2]` Do not widen the binary posture. Run one real mixed component first, editable source material next to heavy immutable assets, and see whether an override covers it | Agreed. This does not conflict with the `Assets` fix above: that one repairs text, it does not add a third posture | Release |
| `[R2]` Test whether an account-relative address (`OneDrive, Projects/...`) actually resolves for different agents | Agreed. The string is human-readable and nothing can `cd` into it; what resolves is the local path hint beside it. The risk is an agent treating the account-relative form as a path. Measure it with the cold start check rather than describing it in one more page of rules | Release |
| `[R2]` Add no new concepts. The next value is breaking tests: Windows/WSL/synced drive, with and without an override, nested, and a deliberately unreachable parent | Agreed, and this is the strongest single item in either review | Now, as the plan |
| `[R2]` Praise: the framework's own `AGENTS.md` and `CLAUDE.md` closed the old dogfooding problem | Partly disagreed. Both adapters carry a rule about `blueprints/` (`AGENTS.md:7`), and `blueprints/project/README.md:106` forbids exactly that: "The adapters redirect and stop." The rule is also redundant under the razor, since every file in `blueprints/` carries a visible notice at the top | Now |
| `[V]` `structure-check` 10 requires an override to carry "no claim about whether things are changed or kept here", and `REPOSITORY.md:15` and `ASSETS.md:15` state it in their headers | A false positive waiting to happen, the same shape as the check 4 story already recorded in `structure-check.md:130`. Fix the sentence, not the check: say where the posture is stated without repeating it | Now |
| `[V]` `blueprints/project/README.md:32` says "Components go in subfolders, each with its own entry point" | Stale since 0.5.0, where a component has no entry point. It sits next to the sentence `[R2]` flagged, so both get fixed in one edit | Now |
| `[V]` `checks/README.md:36` and `structure-check.md:165` call "a component that exists on disk and appears in no registry" an uncovered gap | Wording from 0.4.0. It contradicts the definition in `0005:53` and it is what aimed the proposed third check at the wrong target | Now |
| `[V]` The project scope root has no posture. An undeclared folder takes the posture of the component containing it, and folders in the scope root are contained by no component | A hole in the model, already patched by hand: the rule about `blueprints/` in this repository's adapters exists because of it | Release |
| `[V]` Platform rules have nowhere to live. "Never modify WordPress core or third-party plugin code" follows from the platform, not from a folder, and gets copy-pasted into every WordPress component | This is the argument `0005` used to move the preserve rules into the registry, applied one step further. It is also why `wordpress.md` fell three versions behind: nothing owns it | Release |
| `[V]` The metric behind 22, 33 and 40 lines is written nowhere | Non-blank lines, summed across the files of a scope. The next person to measure will get a different number and think something drifted | Later |

---

## Now, as a checklist

One pass over the text, roughly an hour, no architecture touched.

- [ ] `blueprints/setup/procedure.md:41` four to five
- [ ] `register` to `registry` in `README.md` and `.docs/architecture.md`
- [ ] Add editing to the `Assets` posture line, in `blueprints/project/PROJECT.md:119`, `blueprints/setup/procedure.md:150` and `blueprints/assets/README.md:45`
- [ ] Rewrite the "one component means no scope" rule in `blueprints/project/README.md:14` and `blueprints/setup/new-project.md:43`
- [ ] `blueprints/project/README.md:32`, both the absolute sentence and the stale "own entry point"
- [ ] Reword the override headers, `REPOSITORY.md:15` and `ASSETS.md:15`, so `structure-check` 10 cannot fail a correct file
- [ ] `checks/README.md:36` and `structure-check.md:165`, drop the "component not in the registry" framing
- [ ] Decide what happens to the `blueprints/` rule in the root adapters: move it into `PROJECT.md`, or delete it as visible
- [ ] Mark `platforms/wordpress.md` as stale until the platform question is settled

## Release, and what blocks each

Two questions block most of this, and both are settled by running something rather than by arguing.

**Where do platform rules live?** They follow from a platform, not from a folder, which is the same
shape as the preserve rules. Until this is answered, `platforms/` is a copy-paste library with no
owner, and the fragment will rot again.

**Is a second razor needed for rules?** The first one cuts facts. Rules are invisible by
construction, so nothing constrains them. Candidate test: a rule earns a document only if an
assistant would do otherwise without it. Run one WordPress task with the fragment and one without,
and judge by the work rather than by the report. `cold-start-check.md:149` already describes the
method.

Everything else in Release: the third check (registry to disk only), splitting `<SESSION_NOTE>`,
tightening `structure-check` 11, separating "cannot find" from "cannot open" in the stub, the
`entry point` term in `README.md:113`, the missing posture of the scope root.

## Breaking tests, before any of it

`[R2]` is right that this comes first. The matrix worth running: Windows/WSL, a synced drive, a
component with an override, one without, a nested component, and a parent made deliberately
unreachable. If 0.5.x survives that without new entities, the core is stabilizing.

## No action

- The 33 against 40 line counts. Measured, they agree.
- Provenance in the stubs. `git grep` answers the question the metadata would.
