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
