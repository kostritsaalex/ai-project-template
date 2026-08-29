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
