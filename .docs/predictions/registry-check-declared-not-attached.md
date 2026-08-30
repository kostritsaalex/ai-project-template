# Prediction: declared, not attached is a second non-attached outcome

**Written:** 2026-08-30, before the edit and before any run.
**Subject:** `registry-check.md` row 2, gaining a clause for a component whose folder exists and
whose stubs do not.

**What this run is for.** `registry-check` produced 7 failed rows against the ArtGlina scope on
2026-08-30, a scope `structure-check` passed 14 of 14 the same day. Two components declared, both
folders present, neither carrying stubs, because the interview says naming a component does not
attach it. The failures were pre-registered before that run and it matched them, so the check is
behaving exactly as written and the writing is what is wrong.

---

## What the reading found, stated before the edit so the edit can be judged against it

The check recognises exactly one non-attached state. Row 1's clause — *"Unless this row confirmed
the folder exists, rows 2 to 6 for that component are n/a and name this row as the reason"* — is the
only cascade in the prompt and fires only on a folder row 1 could not confirm.

**That clause is not attached to the wrong condition.** A missing folder does make all of rows 2 to
6 unevaluable, row 6 included: a folder that does not exist satisfies an absence check for no useful
reason, which is the defect `0.9.1` collapsed three cases into one condition to repair. Rewriting it
would break what it correctly covers.

**The rows that depend on the stubs are 3, 4 and 5, not 2 to 6.**

| Row | Reads a stub | ArtGlina, both components |
| --- | --- | --- |
| 1 folder exists | no | pass |
| 2 folder holds both stubs | no — it is the row that discovers the state, evidenced by a root listing | **fail** |
| 3 both stubs name the component | yes, quotes the naming line from each | **fail** |
| 4 both stubs give the parent address | yes, quotes the address from each | **fail** |
| 5 overrides agree in both directions | yes, both halves | n/a, and only because no override file happened to be present |
| 6 folder holds no PROJECT.md | no, tests one path | pass |

So the missing outcome belongs on row 2, where its evidence is already gathered, and cascades to 3
to 5. Row 1 is not touched.

## The variable

One clause, added to row 2 of the prompt and nowhere else. Row 1's cascade, row 6, row 7 and the
other two checks are unchanged.

```text
   Both present is a pass. Exactly one present fails, and say which is missing: a component half
   attached is a defect.
   Neither present, in a folder row 1 confirmed, is not a failure. That component is declared, not
   attached: the registry names it and nothing in its folder points back. This row is n/a and says
   so, and rows 3 to 5 for that component are n/a naming that outcome as the reason. Row 6 still
   runs and still returns a verdict, because it does not read a stub.
```

## The predictions, one per arm, written so each can fail

**Arm 1, the ArtGlina scope, unmodified, read-only.** `Artglina UA` and `Artglina Sandbox`:
row 1 pass, row 2 **n/a naming declared, not attached**, rows 3, 4 and 5 **n/a naming that same
outcome**, row 6 pass. Row 7 is out of this change's scope and its result is recorded, not predicted.
**Failed rows: 0**, excluding row 7.

**Arm 2, negative control, missing folder.** A scratch scope, one declared component's folder
deleted. That component: **row 1 fail**, rows 2 to 6 **n/a naming row 1**, not naming declared, not
attached. The intact component keeps arm 1's shape.

**Arm 3, negative control, real defect under the new outcome.** A scratch scope where one component
has both stubs written and its registry heading then made to disagree with the naming line in those
stubs. That component: row 2 pass, **row 3 fail**. The new clause must not reach it, because its
stubs are present.

## What would falsify each

- **Arm 1.** Any row 2, 3, 4 or 5 that is not n/a. Any n/a whose evidence names row 1, or names
  nothing, rather than naming the new outcome. Row 1 or row 6 going silent — they do not read a stub
  and must still return a verdict, and an n/a there means the new clause swallowed more than it was
  given.
- **Arm 2.** The cascade firing with the wrong reason. If a deleted folder produces "declared, not
  attached" instead of naming row 1, the two outcomes have merged and the check now reports a broken
  registry as a normal early state. That is the failure that would make this change worse than the
  defect it repairs.
- **Arm 3.** Row 3 passing, or any row going n/a. A component with stubs present is checked in full,
  and if the new outcome reaches it the clause is keyed on the wrong fact.

## The cost, named now rather than after

A component that was attached and then had both stubs deleted becomes indistinguishable from one
that was never attached, and reports n/a where it used to report fail. The registry carries no field
saying which, so no row can tell them apart. Row 2's evidence still prints the listing that shows no
stubs, and the n/a names the outcome in words rather than passing silently.

The stronger variant exists and is not taken here: require `PROJECT.md` to say in visible text that
the component is not attached, which is the condition row 1 already honours for a missing folder.
ArtGlina's registry does carry such a sentence. It is not taken because the blueprint only
encourages that sentence and does not supply it, so a correct new project whose owner omitted it
would fail, and because it is a second variable.

---

# Outcome

**Run:** 2026-08-30, five sessions against the shipped `0.14.0` text, prompt pasted from the file's
raw text in every one. **All three predictions hold.**

## Arm 1 — ArtGlina, real and unmodified

Predicted: rows 1 and 6 pass, rows 2 to 5 `n/a` naming declared, not attached, `Failed rows: 0`.

Observed, [`runs/2026-08-30-registry-check-10-artglina.log`](../runs/2026-08-30-registry-check-10-artglina.log):
exactly that, for both components. Row 2's evidence is the full root listing with *"Neither AGENTS.md
nor CLAUDE.md present: declared, not attached"*; rows 3, 4 and 5 read *"No stubs to read: check 2
returned n/a (declared, not attached)"*. Row 1 pass, row 6 pass. **`Failed rows: 0`**, against 7 on
`0.13.0`. Row 7 passed, which was recorded and not predicted.

The scope's three root files were checksummed before the first run and verified byte-identical after
the last. Nothing was written.

**One deviation worth recording, in the first of the two runs.** The session sandbox refused `ls`
outside its own directory, so row 2 answered by probing four paths instead of listing the root — the
right verdict on evidence the row does not ask for. The repeat granted the two registry-named folders,
which is exactly the declared read set, and got the listing. Both logs are kept. The verdicts are
identical; only the evidence differs, and the difference is environmental rather than a property of
the clause.

## Arm 2 — negative control, missing folder

Predicted: row 1 fail, rows 2 to 6 `n/a` **naming row 1**, not naming the new outcome.

Observed, [`runs/2026-08-30-registry-check-11-missing-folder.log`](../runs/2026-08-30-registry-check-11-missing-folder.log):
row 1 fail — *"`test -d` returned artglina-ua: NOT PRESENT. No visible text in PROJECT.md says this
component is not attached yet"* — and rows 2 to 6 all `n/a` reading *"Row 1 did not confirm the folder
exists, so this row is n/a per row 1."* **No row named declared, not attached.** The intact component
in the same table took the new outcome. **`Failed rows: 1`.**

**The two cascades are visibly separate in one table**, which is what this arm existed to establish.

**The first attempt at this arm failed for the wrong reason and was rebuilt.** With the components
outside the session's directory, row 1 failed on *blocked access* rather than an observed absence —
the predicted verdict on evidence that does not demonstrate it. Kept as
[`runs/2026-08-30-registry-check-11-missing-folder-blocked.log`](../runs/2026-08-30-registry-check-11-missing-folder-blocked.log)
rather than discarded.

**One deliberate plant beyond the deleted folder**, in both attempts: ArtGlina's sentence *"Neither
component is wired to this scope yet"* was removed from the scratch copy. That sentence is row 1's own
pre-existing exception, which turns a missing folder into `n/a`, and leaving it in would have tested
that clause rather than this one.

## Arm 3 — negative control, real defect under stubs that are present

Predicted: row 2 pass, row 3 fail, the new clause not reaching that component.

Observed, [`runs/2026-08-30-registry-check-12-stubs-present-defect.log`](../runs/2026-08-30-registry-check-12-stubs-present-defect.log):
row 2 pass (*"Listed root of artglina-ua: AGENTS.md, CLAUDE.md. Both stubs present"*), **row 3 fail**,
quoting the heading `## Artglina UA Site` against both stubs' `Artglina UA`. Rows 4 and 6 pass, row 5
`n/a` on its own terms. **`Failed rows: 1`.**

**The table carries both behaviours at once**: one component attached and broken, one declared and not
attached, each row reaching the right one. That is the strongest of the three results, because a
clause keyed on the wrong fact would have had to reach across.

## What was not tested

**Exactly one stub present.** The clause fails that case and says which stub is missing, and no arm
ran it. It is a third negative control and it was not pre-registered, so it is named here rather than
claimed.

**Whether the evidence wording holds under a sandboxed session.** In the first arm 1 run, rows 3 to 5
named row 2 and the fact rather than the outcome by name. The clause says *"naming that outcome as the
reason"*, and four of the five logs do name it. This is a wording drift of the kind the cut-clause run
warned about, not a verdict difference, and it is recorded rather than repaired.
