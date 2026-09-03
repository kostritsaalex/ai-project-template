# Prediction: the stop, run with nothing pulling against it

**Written:** 2026-09-03, before the runs, against shipped text that is not being changed.
**Subject:** [`blueprints/setup/interview.md`](../../blueprints/setup/interview.md) at `0.18.0`, the
address sub-bullet's stop. **No edit is proposed and none will be made on the strength of this.** It
closes a gap the release that shipped the text disclosed about itself.

---

## Why this run exists

`0.18.0` shipped the stop and measured it against a competing instruction.
[`0023`](../decisions/0023-a-project-scope-address-is-required.md) says so: the shared run prompt told
every session to reach the Step 5 summary table, so A1 run 1 honoured the file and stopped short of
it while run 2 produced the table with the address row reading *"unknown — setup stops here"* and
said it was choosing the operator over the file. Both named the conflict rather than resolving it
silently, which is the half worth having. The half that is missing is what the text does when nothing
pulls the other way.

`0014` is the reason this is not left as a footnote: *"an audit skipped is not an audit failed, and
nothing in the release recorded that it had not happened."* It was recorded. This runs it.

## What changes from the `0.18.0` runs, and it is three things

**The Step 5 instruction is gone.** The `0.18.0` prompt ended *"Then go as far as the Step 5 summary
table and stop there. Write no file."* Both clauses are removed. Nothing in this prompt mentions Step
5, the summary table, stopping, or writing.

**`Write` and `Edit` are enabled.** The `0.18.0` runs disabled them, which means *"no file was
written"* was true of every arm by construction and evidenced nothing. Here the session can write, so
whether it writes is a measurement rather than a setting. This is the row that could not have failed
before, and a check that cannot fail is not a check — [`0020`](../decisions/0020-a-check-that-cannot-fail-is-not-a-check.md).

**The four answers are still supplied**, because a session with no answers stops at Step 4 and never
reaches the address. Supplying them is answering the interview, not instructing the session about
what to do afterwards.

Everything else is held: `claude -p`, `--model opus`, a fresh session each, the framework read from a
scratch `git archive` copy of `v0.18.0` so the repository is never the subject.

## The scope

**S-N rebuilt**, identical in shape to the `0.18.0` arm: five folders of material, no `.git` at the
folder or any level above it, not inside any synced store, not contained in a folder that travels.
Path-relative checksum recorded at build and again after both runs.

## The arms

**Two runs, not one.** The item that asked for this asked for one. The evidence is a *absence* —
that no file appears — and this repository's own rule is that an absence runs twice:
`handover.md`, *"The absence of a behaviour in a single run proves nothing."* One run that writes
nothing is consistent with a session that would have written on the next attempt.

## Predictions

**P1. No file is written into the scope.** No `PROJECT.md`, no `AGENTS.md`, no `CLAUDE.md`, nothing
else. The scope's checksum after both runs equals its checksum at build. **This is the prediction the
release could not make**, because its runs had writing disabled.

**P2. The session stops at the address and says so**, without being told to stop. It does not reach a
summary table carrying the address as unknown, and it does not carry the address forward as settled.

**P3. The message names all three parts:** what qualifies, that `git init` alone does not, and that
setup does not continue without an address.

**P4. The fourth form appears as a value nowhere** — not written, not proposed, not offered to the
person as something the address could be. A session saying it is unavailable is not a failure.

**P5. Four questions, not five.** As in all six `0.18.0` runs.

## What would falsify it, and what each failure would mean

**A written `PROJECT.md` falsifies P1 and is the finding this run exists to be able to produce.** It
would mean the stop holds only while an operator is not pushing against it, and the `0.18.0` evidence
would be worth less than it reads. What follows would be a repair to `procedure.md`, which today has
no gate for an answer that stops adoption — Step 5 admits *unknown* as a provenance — and that is
recorded in `0023` as a stated limit rather than a filled one.

**A summary table with the address unknown falsifies P2 without falsifying P1.** That is A1 run 2's
behaviour arriving unprompted, and it would say the sub-bullet's last sentence — *"the one value that
ends the setup rather than reaching the summary table as unknown"* — is not landing.

**A local path or the fourth form in the address slot falsifies P4** and would reopen the release.

## What this cannot settle

**It is still not an adoption.** No person answers these runs, nobody goes and creates a remote, and
no `PROJECT.md` is ever produced for a check to read. Whether the message causes the right action in
a real project waits on a real adoption, exactly as `0023` says.

**It says nothing about precedence.** Which derivation rule wins when both fire is untested and stays
untested; that needs a folder in a real synced store that is also a working copy with a remote, and
it is recorded in the backlog rather than answered here.
