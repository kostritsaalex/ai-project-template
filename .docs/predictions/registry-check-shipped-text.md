# Prediction: the negative half against the shipped text

**Written:** 2026-08-29, before the run.  
**Subject:** `blueprints/checks/registry-check.md` as it stands after `0.9.0`, plus the check 6
rewrite. This text has never been run. The negative runs used a prompt that differs from it by the
three lines making rows 2 to 6 `n/a`, and by check 6's old wording.

**Why this exists.** `0.9.0` shipped a check whose prompt no run had ever used, which is the state
principle 6 exists to prevent. `0.9.0` stands as provisional until this run.

**Scope:** `WordPress 7`, with the same single line planted as in
[`registry-check-negative-run.md`](registry-check-negative-run.md): the Engine's registry local path
set to `~/wordpress-7`, a folder that does not exist. The variable is unchanged, so this file is
short.

---

## Predicted

**Check 1, Engine: fail.** Same reason as both previous negative runs, quoting the address line,
falling through to the local path line, resolving it and reporting the folder missing.

**Rows 2, 3, 4, 5, 6 for the Engine: `n/a`, all five,** each naming check 1 as the reason. This is the
new rule and the whole point of the run. In the two runs of the old text these came back as five
fails, and as four fails plus a nonsensical pass.

**Every `WP Themes` row unchanged:** 1 pass, 2 pass, 3 pass, 4 pass, 5 n/a, 6 pass. Check 6's evidence
should now be a single probe of one path rather than a folder listing.

**Check 7: pass.** One row, `(read set)`.

**Final line: `Failed rows: 1`.** One planted defect, one verdict.

## What would mean the n/a clause is too wide

**`WP Themes` rows turning `n/a`.** Its check 1 passes, so nothing licenses n/a anywhere in its
column. If the clause bleeds into a component whose folder was found, it is suppressing real
verdicts, which is worse than the noise it replaced: noise is visible and suppression is not.

**Check 7 turning `n/a`.** It is not in the 2-to-6 range and does not depend on check 1. If it goes
n/a, the clause is being read as "anything downstream of a failure", which would let one broken
component silence the audit of the read set.

**`Failed rows: 0`.** The planted defect must still produce exactly one failure. A count of zero
would mean the n/a rule swallowed check 1 itself, and the check would have been repaired into
uselessness — the one outcome that would be worse than the noise it was written to remove.

## Re-run rule

As before: any row disagreeing with this prediction gets the arm run again before anything is
concluded.

---

# Outcome

**Run:** 2026-08-29, twice. Every prediction confirmed, both times, on every row. Logs
`2026-08-29-registry-check-4-shipped.log` and `-repeat.log`. Everything above this line was written
before either run.

Check 1 failed the Engine in both, quoting line 71 to justify falling through to line 72, expanding
the tilde, and reporting the folder missing. Rows 2 to 6 for the Engine came back `n/a` in both, all
five, each naming row 1. Every `WP Themes` row was unchanged, and check 6's evidence is now a single
probe: "Tested the single path `.../wp-themes/PROJECT.md` with `test -e`: ABSENT." Check 7 passed as
one row. `Failed rows: 1` in both.

None of the three too-wide outcomes occurred. No correct component's row turned `n/a`, check 7 did
not, and the count did not fall to zero.

**One planted defect, one verdict, in both runs.** The old text produced six failures in one run and
five plus a nonsensical pass in the other, on the same defect. The comparison is in
[`../runs/`](../runs/): four logs, two prompts, one scope state.

**`0.9.0` is no longer provisional.** The text that shipped has now been run against the defect the
check exists to catch, twice, and behaves as specified.

**The check 6 rewrite is not isolated by these runs, and an earlier version of this section said it
was.** The pair differs from the previous pair by two changes at once, the cascade and the rewrite.
Check 6 came back `n/a` for the Engine in both, which the cascade decided rather than the rewrite,
and `pass` for `WP Themes` in both, where the absence half of the evidence rule had already been
restored in `49b25dd`. So the row's stability here is not attributable to the rewrite.

What the pair supports is narrower: the shipped text as a whole behaved as predicted, twice. The
rewrite stands on its reasoning, that a row asking for one fact should take one probe, and not on a
measurement. Isolating it would cost a run and is not worth one; saying it is not isolated costs a
sentence.
