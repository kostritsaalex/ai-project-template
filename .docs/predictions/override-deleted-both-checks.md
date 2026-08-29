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
