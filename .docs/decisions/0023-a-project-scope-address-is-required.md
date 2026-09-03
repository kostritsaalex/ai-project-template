# 0023. A project scope's address is required

**Date:** 2026-09-03
**Status:** accepted

---

## Context

`interview.md` derived a project scope's address by two rules, and where neither fired it wrote
[`0007`](0007-a-component-with-no-address-says-so.md)'s fourth form: *"the address is `0007`'s fourth
form: `none`, with the reason."*

**`0007` does not say that.** Its title is *"A component with no address says so"*. Its Decision binds
the form to `structure-check` **11**, which opens *"Project scope only. Every block in the components
registry…"* — a rule about component blocks, written into the scope's registry. Its Consequences state
the asymmetry outright: *"**A component with no address is still a component.** The gap runs one
way… What is missing is only the walk downward, from the parent to that component."* Nothing in it
reaches a scope's own address.

**The consequence was a scope that could not produce a valid component.** `procedure.md` Step 7 has
the stubs *"carry the parent's address, copied from the parent's own text rather than retyped"*, and
ends *"Nothing else in the parent changes when a component is attached"*. `structure-check` row 8
admits three forms for that stub value and fails a bare local path; `component/README.md`'s
`<CANONICAL_PROJECT_SCOPE_ADDRESS>` defines the same three. So a scope adopted with the fourth form
gave its components a stub address that passes row 8 by no value they can write, and the attach was
forbidden from repairing the parent. The person was left mid-setup with a failing check and no
document naming the way out.

**Two parties had already settled the scope half, positively.**
[`0001`](0001-project-scope-need-not-be-a-repository.md): *"A project scope may live anywhere it has
an address that resolves from outside the machine it sits on."* And
[`../audits/structure-check-rows.md`](../audits/structure-check-rows.md) on row 8, marked *settled*:
*"a scope may not be addressless and there is no fourth form for a parent. Three is right."*

**And the branch this needed already existed, unreachable.** `interview.md`'s address bullet has read
*"If neither yields a value, ask for it"* since `0.12.0`. The third sub-bullet always yielded a value,
so no run could reach the clause.

## Decision

**A project scope's address is required, always. The fourth form is for components only.**

Where neither derivation rule fires, the interview asks. It does not propose, does not write a blank,
does not write a local path, and does not reach the summary table with the row marked unknown.

**The asking branch carries the explanation itself, because no session may add one.**
`interview.md` and `procedure.md` Step 4 both forbid it — *"Do not introduce them, gloss them, add
clarifications, or add questions of your own"* — so an explanation that is not in the file cannot
exist at runtime. The text names what qualifies, which is a git remote that has been pushed to or an
account-relative location in a synced store; what does not, which is `git init` alone, per `0007`'s
*"Local version control and reachability are separate questions, and only a remote answers the
second"*; and that setup stops until the folder has one.

**No fifth question, and no merge into an existing one.** [`0014`](0014-the-razor-runs-over-the-questions-one-at-a-time.md)
judged each question by `0004` — *could an assistant that read the folder have proposed this?* — and
the address is in the folder on both derivation branches and absent from it on the third. So the ask
belongs on that branch and nowhere else. A standing question would ask the majority about a value the
assistant is standing next to, which is the complaint that produced `0014`, and it would falsify its
measured *"**Four questions, never five**, on three scopes"*.

**This narrows `0014` and does not reopen it.** `0014`'s Decision restates the derivation and ends
*"with neither, the answer is `0007`'s fourth form, `none` with the reason"*; its table carries the
only hedge in it, `Address | asked | **usually seen** | proposal, with a fallback`. That clause is
displaced by this record. `0014`'s file is not edited, its method is the method used here, and its
measured properties are untouched: no question is added, removed or reworded, so *four questions,
never five* and its fidelity result both stand. **What this removes is the hedge, not the razor** —
seen, propose; not seen, ask.

**The deferred alternative was rejected.** Letting the fourth form stand while a scope has no
components would make `Address: none` mean *"unreachable, accepted cost"* on a component and
*"nothing needs to reach me yet"* on a scope, with nothing in the document saying which reading
applies.

## What carried this, and what did not

**Six runs**, pre-registered before the edit existed in
[`../predictions/the-scope-address-is-required.md`](../predictions/the-scope-address-is-required.md);
five registered, one added mid-experiment and labelled as such. All six logged under
[`../runs/`](../runs/README.md).

**A1, twice, all four criteria.** The address is asked for. **The fourth form's word appears in
neither run as a value** — every `none` in both logs is Step 2 reporting no parent claim, or question
3's own verbatim *"or say none"*. Both messages name what qualifies, that `git init` alone does not,
and that setup stops. No local path reaches the address slot.

**The control carried more than the arm did.** C2 is the unaffected majority — a folder in a store
and nothing else — and the point of it was that nothing should change. Nothing did: the same address
proposed in the table, nothing asked, four questions in every run. But the same scope run against
`0.17.0` **offered the fourth form on a project scope unprompted** — *"If it lives nowhere off this
machine, the correct value is `0007`'s fourth form — `none`, with the reason"* — on the arm this
change was not even aimed at. That is the defect reproduced in the wild, and it is absent from both
`0.18.0` runs. The before-run was not pre-registered; it was added after C2's first run and is
reported as added.

**One registered word reached the person, and it is reported rather than buried.** C2's first run
wrote *"Not a git working copy, so the remote rule does not fire"* in the address row's source
column. One instance in three C2-family runs, in a clause naming which rule fired, which the file
requires of every proposal; the two rules it names are untouched here. No rate is claimed.

**A1's two runs diverge on the stop, and the cause is the harness.** The shared run prompt told every
session to reach the Step 5 table. Run 1 honoured the file and stopped before it; run 2 produced the
table with the row reading *"unknown — setup stops here"* and said it was choosing the operator over
the file. **Both named the conflict rather than resolving it silently.** The stop was therefore tested
against a competing instruction rather than in isolation, which is a limit of the evidence.

**C1 could not reach its own question.** It was built so both derivation rules fire at once, a case no
line settles. The session rejected the simulated store by checking the machine's real `~/OneDrive`,
so it derived from the remote alone and precedence went untested. What C1 establishes is what it
watched for: the new ask branch did not leak into a case where a rule fires.

**Nothing measures the setup path.** `interview.md` is not shipped into an adopted project, so the
shipped-line metric does not see this growth. The length of the replacement is judged by reading and
by nothing else.

## Consequences

**`procedure.md` has no gate for an answer that stops adoption, and this release did not build one.**
Its defined stops — Step 1 for an unreachable framework, Step 2 for a folder that already holds a
`PROJECT.md` — both sit before the interview. For a value that never arrives the defined path is the
opposite of a stop: Step 5 admits *unknown* as a provenance and Step 8 reports which answers stayed
unknown. The stop is written into `interview.md`, bounded to this one value, and Step 7's eight
unclosed defects are the reason nothing was added to that file here.

**So the stop rests on the interview text alone.** No row anywhere validates a project scope's own
`Address:` line against the address forms; `registry-check` row 4 reads it, but only as a comparison
target. A session that ignores the stop is caught by nothing until a component is attached, and then
by `structure-check` row 8 on the stub. **That is why row 8 is not touched** — it still catches the
consequence, and the audit settled its three forms correctly.

**No check row is added and none is widened.** `structure-check` row 8 keeps three forms, row 11
keeps four, and `component/README.md`'s placeholder keeps its three. Each was already right; what was
wrong was the value the interview handed them.

**`architecture.md` gains the qualification it was missing.** Its line *"A location on one person's
machine is not an address in any of these senses. Write the fourth form instead"* was unqualified,
four lines above a paragraph already saying the fourth form is what *a component* carries. It now
says which scope it addresses.

**One backlog item is void and deleted.** Attach defect 6 held that row 8 was too narrow. The repair
was upstream of it and row 8 was right. Its number is held rather than reused, because `0022`, the
`0.17.0` changelog entry and two predictions cite these defects by number and a renumbering would
make all four false.

## Origin

**Decided by the owner, 2026-09-02.** A fifth interview question was considered the same day and
rejected on `0014`'s own grounds. The deferred alternative — letting the fourth form stand while a
scope has no components — was rejected in the same decision.

Two things this session found while applying it, recorded as found rather than as anyone's. That
`0014`, not only `0007`, states the rule being removed, which is why this record names the clause it
displaces instead of leaving two documents to disagree. And that `interview.md:27`'s *"ask for it"*
already said the right thing and had been unreachable since `0.12.0`, so the repair restores a branch
rather than inventing one.
