# Prediction: a project scope's address is required, and the interview asks for it

**Written:** 2026-09-03, before the edit and before any run of the changed text.
**Subject:** [`blueprints/setup/interview.md`](../../blueprints/setup/interview.md) — the third
sub-bullet under "The address", replaced. Nothing else in the file's instructions changes, and the
four questions are not touched.

---

## The facts this rests on, established in this working tree rather than from the report

**The defective instruction.** `interview.md:33-34`, third sub-bullet under "The address":

> - If there is no copy of this folder anywhere off this machine, the address is `0007`'s fourth
>   form: `none`, with the reason. Never a blank, and never a local path in the address slot.

**That value is what a component copies.** `procedure.md:136-137` — the stubs *"carry the parent's
address, copied from the parent's own text rather than retyped"* — and `procedure.md:159-160`,
*"Nothing else in the parent changes when a component is attached"*.

**And it cannot pass the row that reads it.** `structure-check.md:83-86`, row 8, admits three forms
for the parent address and ends *"A bare local path fails"*. `component/README.md:42` defines
`<CANONICAL_PROJECT_SCOPE_ADDRESS>` with the same three: *"a full URL, an account-relative location
in a synced store, or `../` when the project scope contains this folder"*. So a scope adopted with
the fourth form yields a component that passes row 8 by no value it can write, and the attach is
forbidden from repairing the parent.

**`0007` does not authorise the fourth form for a project scope.** Read in full in this tree. Its
title is *"A component with no address says so"*; its Decision binds the form to `structure-check`
**11**, the registry row, which is `structure-check.md:92`, *"Project scope only. Every block in the
components registry…"*; its Consequences state the asymmetry outright at lines 75-79 — *"**A
component with no address is still a component.** The gap runs one way… What is missing is only the
walk downward, from the parent to that component."* Nothing in it reaches a scope's own address.

**Two parties settle the scope half positively.**
[`0001`](../decisions/0001-project-scope-need-not-be-a-repository.md):25 — *"A project scope may live
anywhere it has an address that resolves from outside the machine it sits on."* And
[`../audits/structure-check-rows.md`](../audits/structure-check-rows.md):63, on row 8: *"`0001`
decides that a project scope may live anywhere 'it has an address that resolves from outside the
machine it sits on', so a scope may not be addressless and there is no fourth form for a parent.
Three is right"* — marked *"Yes, and now settled"*.

**The branch this repair uses is already in the file and is unreachable.** `interview.md:27` —
*"**The address** — derived, and only by the two rules below. If neither yields a value, ask for
it."* The third sub-bullet always yields a value, so no run can reach that clause.

**`0014` states the rule being removed, and this is disclosed rather than worked around.**
[`0014`](../decisions/0014-the-razor-runs-over-the-questions-one-at-a-time.md):42-48 gives the
derivation in its Decision section and ends *"with neither, the answer is `0007`'s fourth form,
`none` with the reason, never a blank and never a local path in the address slot."* Its table at
line 34 also carries the only hedge in that table, `Address | asked | **usually seen** | proposal,
with a fallback`. So one accepted decision does say what this release removes. `0014`'s file is not
edited; the clause is named and displaced by the record this release writes, and `0014`'s measured
properties are untouched — **four questions, never five** (line 70) and fidelity 1.000 (line 67)
both survive, because no question is added, removed or reworded.

**Why the third branch must ask rather than propose, from `0014`'s own criterion.**
[`0004`](../decisions/0004-documents-carry-what-cannot-be-seen.md) is *propose what can be seen, ask
only what cannot*, and `0014`:25 judges each question by *"could an assistant that read the folder
have proposed this?"* On the first two branches the address is in the folder. On the third there is
nothing in the folder to read, because there is no copy anywhere to name. So the third branch is the
"ask" side of `0004`, and this repair removes `0014`'s hedge rather than reversing its method.

**No fifth question, and no merge.** `0014`:70 carries **four questions, never five** across sixteen
pre-registered runs; a fifth would make that false. `0014`:16-18 records the complaint that produced
the audit — the owner *"asking why he was being asked things the assistant was standing next to"* —
and a standing question about the address would ask the majority about a value the assistant is
standing next to. The ask therefore lives on the branch where nothing is there to see.

**The running session cannot supply the explanation.** `interview.md:18-20` and `procedure.md:77-80`
both forbid it: *"Do not introduce them, gloss them, add clarifications, or add questions of your
own."* So the explanation exists only as text in this file, on this branch.

**`procedure.md` defines no gate for an answer that stops adoption, and this release does not build
one there.** Read in full. Step 1:33 stops when the framework is unreachable, and Step 2 item 2
(line 44) stops when the folder already holds a `PROJECT.md` — both before the interview. For a
value that does not arrive, the defined path is the opposite of a stop: Step 5:103 admits
*"unknown"* as a provenance and Step 8:183 reports *"which answers stayed unknown"*. The stop this
release needs is therefore written into `interview.md`, bounded to this one value, and the absence in
`procedure.md` is stated rather than filled, because Step 7 has eight unclosed defects and nothing
goes into that file in this release.

## What ships

`interview.md`'s third sub-bullet under "The address" is replaced. It stops instructing the fourth
form, it carries the explanation the person reads, and it names what qualifies, what does not, and
that setup stops. The word for the fourth form is not written in the replacement, so no session can
echo it from this file.

`interview.md:27` is **not** edited. Determined from the text rather than assumed: *"the two rules
below"* already counts the two rules that derive, both of which are unchanged, and the third
sub-bullet was always the neither-case. What changes is that *"If neither yields a value, ask for
it"* becomes reachable and true. No file contradicts either clause.

Two edits in `.docs/` ride with it: `architecture.md:76` gains the qualification `:83` already
carries, and `backlog.md` loses one void item and gains two records. Neither causes the release —
`release.md`:14, *"A change under `.docs/` never causes a release"* — and both are accounted for in
the changelog entry because `release.md` V1 requires every file in the diff to be.

## The scopes

Three, all scratch, all deleted afterwards, none of them a real project. Checksums are
path-relative — `( cd "$SCOPE" && find . -type f | sort | xargs md5sum | md5sum )` — after the
recipe defect of 2026-08-29, when hashing absolute paths made a rebuilt-identical scope fail its own
verification.

| | Shape | Address situation |
| --- | --- | --- |
| **S-N** | Five folders, material only, no code | **Neither rule fires** — no git, no store, no containing folder that travels |
| **S-BOTH** | Three folders, mixed | **Both rules fire** — inside a simulated store *and* a git working copy with a remote |
| **S-STORE** | Three folders, mixed | Inside a simulated store, nothing else |

**The simulated store is a declared deviation, carried forward unchanged.** A symlink inside the
scratch directory stands in for `~/OneDrive`, because writing test folders into the owner's real
synced store would push them to his cloud. The rule under test is *"the local path resolves inside a
synced store"*, and the simulation satisfies it.

**The confound found on 2026-08-29 is inherited and is not in this release's causal path.** That
experiment recorded that a real `~/OneDrive` on the machine means a session may read the store from
the real path rather than from the simulation. It bears on S-STORE's *derivation*, which this change
does not touch, and not on S-N, which has no store to confound.

## The arms

Four runs. `claude -p`, `--model opus`, a fresh session each, `Write`/`Edit`/`NotebookEdit`
disabled, identical across arms, against a scratch copy of the framework so the repository is not
read as the subject. Answers to the four questions are supplied in the prompt so each session reaches
the Step 5 summary table, where the address is settled or asked; the ten runs before 2026-08-30 that
stopped at Step 4 measured neither.

| Arm | Scope | Framework | Runs |
| --- | --- | --- | --- |
| **A1** | S-N | `HEAD` + the replaced sub-bullet | **2** |
| **C1** | S-BOTH | Same | 1 |
| **C2** | S-STORE | Same | 1 |

**A1 runs twice because its evidence is partly an absence.** Two of its three criteria are that
something does not appear.

## Registered arm A1

A folder with no remote, outside any synced store, not contained in a folder that travels. All four
must hold in both runs:

1. **The address is asked for**, not proposed and not settled in the summary table.
2. **The fourth form's word appears nowhere** in anything the run produces — not in a document, not
   in the summary table, and not offered to the person as a value the address could take. Mentioning
   that it is unavailable is not a failure; offering it is.
3. **The message names all three parts:** what qualifies, which is a git remote that has been pushed
   to or an account-relative location in a synced store; that `git init` alone does not qualify; and
   that setup does not continue without an address.
4. **No local path is written into the address slot**, which is the defect `structure-check` 11 was
   written for.

**What would retract the change:** either A1 run producing the fourth form as a value, or a run that
asks for the address without naming what qualifies. The first would mean the text did not land; the
second would mean it asks a person a question they cannot answer, which is worse than the defect.

## Controls, not derived from the hypothesis

**C1. A folder that is both inside a synced store and a git working copy with a remote.** Both
derivation rules yield a value and **no line in the file says which wins**. This change has no reason
to handle that case, which is why it is the one to watch. Predicted: the session proposes one of the
two, names its rule, and does not ask — because `:27`'s ask branch is for *neither* rule firing, not
for both. **A run that asks here is a real finding against this edit**, and it is the shape the edit
could plausibly cause: a sub-bullet that ends in an ask, read as the general fallback. Recorded
either way; nothing about the precedence question is repaired in this release.

**C2. A folder inside a synced store and nothing else.** The unaffected majority. Predicted: the
address is proposed as `OneDrive, <path within the store>` in the summary table; **nothing is asked
about the address**; the words *remote*, `git init` and *setup does not continue* do not reach the
person; and there are **four questions, not five**. A repair that starts lecturing the unaffected
path has failed even if A1 passes, and this is the arm that says so.

## Not measured here, and disclosed rather than deferred quietly

**Nothing measures the setup path.** `interview.md` is setup text and is not shipped into an adopted
project, so the shipped-line metric does not see this growth. That is a reason for care rather than
for comfort, and it means the length of the replacement is judged by reading and by nothing else.

**No adoption follows an A1 run to the end.** These runs reach Step 5 and stop. Whether a person who
reads the message goes and creates a remote, and whether the adoption then completes correctly, is
not observed here and waits on a real adoption. The stop is therefore shipped as text whose *effect*
is unrun, which is defect 2 of the attach's nine — *"The shipped procedure was unrun text"* — in its
weaker form, named here rather than left to be noticed.

**The gap this leaves open, stated as a limit rather than as a repair.** If a person supplies nothing,
`procedure.md` Step 5 admits the value as *unknown* and no check validates a scope's own `Address:`
line against the address forms. `registry-check` row 4 reads that line, but only as a comparison
target. So the stop rests on the interview text alone, and a session that ignores it is caught by
nothing until a component is attached and `structure-check` row 8 fires on the stub. That is the
consequence row 8 still catches, and it is the reason row 8 is not touched.
