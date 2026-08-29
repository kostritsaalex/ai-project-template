# Prediction: a deleted override, against both checks

**Written:** 2026-08-29, before the plant.  
**Subjects:** `structure-check` row 10 and `registry-check` row 5, run against the same folder.

## Why, and a correction to the premise

The audit ranked `structure-check` row 10 first, and leaned on `registry-check` 5 catching the same
defect in both directions. Before leaning on it, the logs were read.

**Across fifteen logs, `registry-check` row 5 has never returned a pass.** Thirteen runs give `n/a`
for both components. Two give `n/a` and `fail` — the two `3-negative` runs, where the Engine's folder
could not be found and every row below check 1 failed with "no evidence". Those were the cascade
defect, since repaired into `n/a`, not the row doing its job.

So the count is: **0 pass, 2 fail from a defect now fixed, 28 n/a.** The bidirectional behaviour row 5
was written for has never been observed once. It is a claim about a row, not a property of one, and
the audit rested an argument on it.

## The variable

One folder, one edit, both checks run against it.

`wp-themes` currently holds two stubs and no override, and its stubs name none. The plant gives it an
override and then removes the file, leaving the stubs naming it — the half-done state this project
produced for real on 2026-08-29 and repaired as one operation.

```text
wp-themes/AGENTS.md   + This folder also sets rules of its own. Read `REPOSITORY.md` as well.
wp-themes/CLAUDE.md   + This folder also sets rules of its own. Read `REPOSITORY.md` as well.
wp-themes/CLAUDE.md   + @REPOSITORY.md
wp-themes/REPOSITORY.md   — not created
```

Both stubs, and the import, because that is what a component that had an override and lost it
actually looks like. No `REPOSITORY.md` is written at any point, so nothing has to be deleted and
nothing of the component's real content is touched.

## Predicted

**`registry-check` row 5: fail**, for `WP Themes`, saying which half is missing — the stubs name
`REPOSITORY.md` and the file is not there. Every other row unchanged, `Failed rows: 1`.

This is the row's first non-cascade verdict other than `n/a` in sixteen runs, and the first evidence
that it does what it claims.

**`structure-check` row 10: n/a**, or a pass. Either is the defect. The row reads "If `REPOSITORY.md`
or `ASSETS.md` is present … If neither file is present, this check is n/a", and neither is present,
so the row is not licensed to look at the stubs at all. A tool following it returns `n/a` on a
component whose stubs point at a file that does not exist.

Also predicted for that run: **row 4 fails**, because the plant makes the two stubs differ — only
`CLAUDE.md` carries the `@REPOSITORY.md` import, and row 4 excludes "any line beginning with the at
sign", so the two prose sentences match and the import is excluded. **On reflection row 4 should
pass.** Recorded as the prediction I am least sure of, and a failure there would mean row 4's
exclusions do not work as read.

## What would falsify each

- **`registry-check` 5 returning `n/a` or passing.** Then it does not catch the defect either, the
  audit's argument collapses in both directions, and two checks share one blind spot rather than one
  covering the other. This is the outcome that would matter most and it is not unlikely, given the
  row has never been seen to do anything.
- **`structure-check` 10 failing.** Then the row is better than its wording and the audit over-read
  it, and what needs explaining is how a tool got from "if neither file is present, n/a" to a failure.

## Restoration

The two stub files are snapshotted with checksums before the plant, restored from that snapshot
rather than retyped, and verified byte-identical afterwards.

## Re-run rule

By the rule recorded in `handover.md` today: repeat the run whose evidence is an absence. A `fail`
carrying a quotation is self-verifying and runs once. An `n/a` or a pass is produced as easily by not
looking, so if either check returns one, that arm runs again before anything is concluded.

---

# Outcome

**Run:** 2026-08-29. `registry-check` once, `structure-check` twice under the repeat rule, since its
result for row 10 is an absence.

**`registry-check` row 5: fail, as predicted, and its first real verdict.**

> Both stubs name REPOSITORY.md — AGENTS.md (wp-themes) line 16 … CLAUDE.md (wp-themes) line 16 …
> Missing half: the file. Tested wp-themes/REPOSITORY.md — does not exist.

It named which half was missing, quoted both stubs and probed the path. In sixteen runs this row had
returned `n/a` twenty-eight times and `fail` twice from a cascade defect; this is the first time it
has done the thing it was written for. The audit's argument rested on a claim about the row, and the
claim turns out to be true.

**`structure-check` row 10: `n/a`, twice, as predicted.**

> neither REPOSITORY.md nor ASSETS.md is present in the folder root

The row is not licensed to look at the stubs when neither file is present, so it did not, on a
component whose stubs point at a file that does not exist. The defect is confirmed exactly as the
audit read it out of the wording.

## What was not predicted, and it changes the ranking

**Row 13 failed, in both runs, and caught the defect row 10 missed.**

> `REPOSITORY.md` — AGENTS.md:16 / CLAUDE.md:16 "This folder also sets rules of its own. Read
> `REPOSITORY.md` as well." … the file is not in the folder root (`.vscode`, `AGENTS.md`,
> `CLAUDE.md`, `homecare-of-baltimore`) and neither stub says in visible text that it does not exist
> yet

`Failed checks: 1` in both runs. So **`structure-check` does catch a deleted override**, and the
audit was wrong that this is a blind spot. It is a mis-routed verdict: the row that ought to own the
defect abstains, and a different row picks it up.

And it picks it up *because of the property the audit criticised*. Row 13 was ranked sixth with the
complaint that its positive definition, "any other file or folder they say is here", is unbounded and
leaves the tool to decide what counts. That unboundedness is exactly what let it treat a stub's
mention of `REPOSITORY.md` as a pointed-to location. The row's looseness is load-bearing.

**Row 4 passed**, and the prediction for it was muddled: the paragraph first said it would fail, then
corrected itself to a pass before the run. The pass is right and the evidence shows why — the
at-sign exclusion works as written, quoting `CLAUDE.md:18 @REPOSITORY.md` as excluded. A prediction
that argued with itself is not a prediction, and it is recorded as such rather than counted.

## What this settles

- `registry-check` 5 does what it claims. Demonstrated once, on evidence that is a quotation.
- `structure-check` 10 does not, and the wording predicted it exactly.
- `structure-check` as a whole is not blind to this defect, so row 10's rank of first overstates the
  consequence. What it costs is a verdict in the wrong place, not a miss.
- Row 13's unbounded definition is a strength here and a weakness elsewhere. Both readings are now
  evidenced, and any change to that row has to keep this behaviour.
