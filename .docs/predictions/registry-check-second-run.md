# Prediction: the second run of `registry-check`

**Written:** 2026-08-29, after the repair and before either arm is run.  
**Subject:** `blueprints/checks/registry-check.md` as repaired, against the same prompt as committed
in `381b200`.  
**Scope under test:** `WordPress 7`, unchanged since the first run and believed correct.

The first run's predictions are in
[`registry-check-first-run.md`](registry-check-first-run.md). This file exists for the reason that
one did, and for a second reason the first run supplied: a mechanism was predicted correctly and its
inventory wrongly, and only a written prediction makes that difference visible afterwards. Without
one, both halves get remembered as "predicted".

---

## The control, and why there is one

**Both arms run: the repaired prompt, and the original prompt again.**

The repaired prompt alone cannot separate a repair from variance. This project already records that
two runs of one prompt differ, from the setup run that offered a WordPress fragment once and not the
next time. If the three failing rows now pass, that is consistent with the repair and also consistent
with a run that would have passed anyway.

So the original prompt is run a second time, unchanged, on the same scope. If its three failures
reproduce, the repair has something to have fixed. If they do not, the first run's failures were at
least partly variance, and every claim resting on them weakens — including two of the three
pre-registered predictions that were scored as confirmed.

That is the arm most likely to be uncomfortable, which is why it is written down before either runs.

---

## Predictions, repaired arm

**R1. Check 6 passes both components, evidenced as an absence.** The absence paragraph is restored,
so the expected evidence is of the form "listed the root of wp-themes, no PROJECT.md", with no quote.
*Fails if* either row still returns "no evidence", or passes while quoting something irrelevant.

**R2. Check 4 passes `WP Themes`, and the evidence says what `../` resolved to.** The row now
instructs resolution and the prompt now says resolving is computing. The Engine's row continues to
pass as a string match.
*Fails if* `WP Themes` still fails, or passes without stating what the path resolved to, which would
mean the row was satisfied by assertion.

**R3. Check 7 comes back as one row with "(read set)" in the Component column,** listing every folder
opened and classifying each. This is the prediction I hold most loosely: the per-component table
format is stated three lines above it, and format instructions tend to win over exceptions to them.
*Fails if* the tool emits per-component rows for check 7 anyway.

**R4. The final line reads "Failed rows: 0".**
*Fails if* it says "Failed checks", or gives a number that disagrees with the table.

## Predictions, control arm

**C1. The original prompt fails check 6 on both components again,** for the same reason. This is the
defect with the clearest mechanism and the one I expect to be deterministic.

**C2. The original prompt fails check 4 on `WP Themes` again,** and passes it on the Engine.

**C3. Check 7 passes again, by some improvisation, not necessarily the same one.** The first run
reached for `PROJECT.md` line 45. A second run may reach for something else or exempt the root
silently. I predict a pass and I do not predict the route, and if the route differs that is itself
worth recording: an ill-specified row produces a different repair each time and a green result every
time.

---

## What no run here can settle

**Check 7's pass carries no information about check 7.** Its subject is the tool's own behaviour, and
a tool that stays inside the read set produces a pass whether the row is well specified or badly
specified. The first run proved that: the row was broken and it passed. Nothing in a positive run
distinguishes a working check 7 from a decorative one, and the only thing that would is a run where a
tool genuinely reads outside the set, which cannot be induced honestly.

This is the sharpest limit on the whole check and it is not fixable by wording.

**The negative half is still unrun.** A scope broken on purpose, in a fresh session, to see whether
check 1 and check 4 catch what they exist for. Neither arm here does that. Both arms audit a scope
believed correct, which tests only that the check does not obstruct a good document.
