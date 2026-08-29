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

---

# Outcome

**Run:** 2026-08-29, both arms, same scope, control prompt verified byte-identical to the first run's.
Everything above this line was written before either arm ran and is unedited.

## Repaired arm: `Failed rows: 0`

**R1 confirmed.** Check 6 passed both components, evidenced as an absence: "Listed root of wp-themes,
no PROJECT.md". No quote, no "no evidence".

**R2 confirmed.** Check 4 passed `WP Themes`, and the evidence states the resolution: "resolved from
`.../WordPress-7/wp-themes` to `.../WordPress-7`, which is this folder — compared as a location". The
Engine passed as a string match, naming that it was compared as text.

**R3 confirmed,** and it was the prediction held most loosely. Check 7 came back as a single row with
`(read set)` in the Component column, listing all three folders opened and classifying each.

**R4 confirmed.** `Failed rows: 0`.

## Control arm: the first run's failures did not all reproduce

**C1 refuted.** Check 6 **passed** both components under the original, unrepaired prompt, evidencing
the absence itself: "`ls -la` on `wp-themes/` lists ... no PROJECT.md among them". The first run
failed both rows with "no evidence" on the identical prompt and the identical scope.

So the defect is real by reading — the absence paragraph genuinely was missing — and its effect is
intermittent. **P2 was scored as "confirmed, exactly the predicted mechanism" on a single
observation that does not reproduce.** The prediction identified a real hole in the prompt; the run
that appeared to confirm it could have gone either way, and the confirmation was worth less than it
was recorded as being. This is the specific error the pre-registration exists to make visible, and it
was mine.

**C2 confirmed.** Check 4 failed `WP Themes` and passed the Engine again, on the same reasoning:
"The two texts differ". Deterministic across two runs, so P3 stands on evidence rather than luck.

**C3 confirmed, and the route repeated.** Check 7 passed again, again citing `PROJECT.md` line 45,
this time saying it outright: "Not a component; it is the scope's own root, named at PROJECT.md line
45". The prediction declined to name the route and the route was identical, which strengthens the P1
diagnosis rather than weakening it: the row does not produce a random repair, it reliably produces
the same one, and reliably returns green.

**Found by the control, not predicted.** The original prompt's final line came back `Failed checks: 1`
this time, counting checks, where the first run answered `Failed checks: 3`, counting rows. The same
instruction, the same scope, two different readings. The ambiguity the first run exposed is now
demonstrated rather than inferred.

## What the two arms together say

The three rows that failed in the first run break down into one deterministic defect (check 4), one
intermittent one (check 6), and one that never failed at all and passes by being repaired (check 7).
All three were worth fixing. Only one of them had the evidence its scoring claimed.

**The larger finding, and it is not about this check.** `blueprints/checks/README.md` says the
structure check is mechanical, and that "every row is a quote you can open and verify, so its result
does not depend on the tool's judgment". These runs show the limit of that claim. Where a row is
fully specified the result is stable; where a row is under-specified the tool silently supplies the
missing rule, differently on different runs, and returns a confident table either way. An
under-specified row is judgment wearing mechanical clothes, and nothing in the output distinguishes
the two. That applies to every check in this folder, not only to this one.

## Still unrun

The negative half. Both arms audited a scope believed correct, which shows only that the check does
not obstruct a good document.
