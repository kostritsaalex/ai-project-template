# 0025. A decisions folder belongs to a declared component

**Date:** 2026-09-05
**Status:** accepted as a rule. The one check question it owes is not written, so nothing
enforces it yet, and it does not reach `blueprints/` until that question exists and has run.

---

## Context

`blueprints/project/PROJECT.md` sends project-wide decisions to `.docs/decisions/` in the scope
and adds: *"Anything affecting one component only belongs to that component."* It then names no
folder inside a component, and nothing else does either. So a decision about one plugin has a
rule sending it somewhere and no somewhere to be sent to.

**The rule this repository already has.** `.docs/architecture.md`: *"Being a component is a
decision written into the registry rather than a property of what sits on disk."* A folder
nobody declared is not a component; it is files, taking the posture of whatever contains them.
Nothing about a folder's contents promotes it.

**What the checks already do, corrected.** `structure-check` row 13 carries no scope-only
label, so it runs on a component too: every location the folder's documents point to must
exist or be declared absent in visible text, and *a decisions folder* is named in that row
explicitly. Row 10 already requires both stubs to point at `REPOSITORY.md` or `ASSETS.md` by
name where one is present. So the mechanism for enforcing this exists and has nothing to bite
on, because a component's two stubs point at nothing but the parent.

`cold-start-check` is the gap. Its project-scope prompt asks, as question 4, for the decisions
folder or the visible statement that there is none. Its component prompt has no counterpart.

## Decision

**A folder nobody declared a component has no decisions of its own.** The existing rule with
one clause added, and no new concept enters the framework.

**Wanting a decisions folder is a valid trigger for declaring a component.** Promotion costs
two stubs and one registry block, about 22 non-blank lines by the metric in `README.md`. That
cost is the filter: a folder worth recording lasting decisions about is worth an entry in the
registry, and a folder not worth 22 lines was not going to carry decisions either.

**Until promotion, a record about a subfolder is written in the nearest declared scope's
decisions folder.** The lazy path is a path and not a dead end, which is what
[`0026`](0026-a-record-carries-its-subject-only-when-the-folder-cannot.md) exists to make
workable.

**A promoted component states the rule in its override, not the folder.** The folder is visible
to anyone who opens the component, so naming its existence is writing the visible and `0004`
forbids it. What is not visible is the rule: that decisions about this component are recorded
here rather than in the parent. That sentence is what the override carries, and having it is
what makes such a component a component with something to say about itself, which is the only
thing an override is for.

## Options considered

| Option | What it buys | What it costs and how it fails | Decision |
| --- | --- | --- | --- |
| Promotion trigger plus the lazy path | No new concept; enforcement rides on rows 10 and 13, which exist; the registry keeps describing the whole project | Friction at the moment of writing, which is when a rule is most easily ignored. Fails if nobody ever promotes anything and the trigger turns out to be decoration | **Chosen** |
| A decisions folder allowed in any folder | Zero friction; the record goes where the work is | Documentation appears outside the registry, invisible to all three checks. Fails silently and permanently, which is the defect class this record was written to close | Rejected |
| Everything stays in the scope forever | Simplest rule; one folder, one sequence | Decisions about a plugin accumulate in a folder that is not about the plugin, and nothing carries them when the plugin moves. Fails slowly, by the scope becoming a dump | Rejected |

## Consequences

**Friction lands at the worst possible moment, deliberately.** The wish to record arrives while
someone is inside the folder and wants to write now, and the rule can send them to the registry
first. That is the filter working, and it is also the likeliest way this rule gets ignored. The
lazy path is what keeps the cost of complying low enough to be paid: nobody has to promote
anything to write the first record.

**One check question is owed, and until it exists nothing enforces this.** The component prompt
of `cold-start-check` needs the counterpart of its scope question 4. Without it a component can
carry decisions no reader is ever asked to find. `structure-check` needs nothing, which was not
obvious and was established by reading row 13 rather than assumed.

**The format decision is independent.** No check reads inside a record, so
[`0024`](0024-a-decision-record-names-its-options-and-its-revisit-trigger.md) and this record
can ship in either order or alone.

**Recovery if the trigger proves wrong.** The clause is additive: withdrawing it leaves every
record where it already sits, in the scope, which is where they would have been anyway. Nothing
has to move back.

**Prediction, registered before the rule is used.** Promotion will fire rarely, because "affects
one component only" is rarer in practice than the wording suggests. A choice such as a custom
table instead of postmeta touches the plugin, the site running it and the backup procedure, so
by the test in `0024` it stays in the scope. The expected outcome is that most records keep
living in the scope under `0026`'s naming, and promotion happens for a handful of folders that
genuinely have lives of their own.

**Revisit trigger.** The first promotion that happens under this rule, or twelve months with
none. Twelve months with none says the second clause is decoration and should be cut.

## Origin

Proposed by the owner in a working session, in response to a gap surfaced in that session by
reading `PROJECT.md` against the component rows of `structure-check`. The owner's formulation
was that a folder worth its own decisions is a folder worth declaring. The override route, the
correction that row 13 already covers the location, and the prediction are the session's and
were argued after the proposal. An earlier claim in that session that two check rows were owed
was wrong and is corrected above.
