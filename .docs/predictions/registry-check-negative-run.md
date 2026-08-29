# Prediction: the negative run of `registry-check`

**Written:** 2026-08-29, before the defect is planted and before the run.  
**Subject:** `blueprints/checks/registry-check.md` as committed in `49b25dd`, the repaired prompt.  
**Scope under test:** `WordPress 7`, with one line deliberately broken.

Both previous runs audited a scope believed correct, which shows only that the check does not
obstruct a good document. This is the half that asks whether it catches anything.

---

## The single variable

One line of `WordPress-7/PROJECT.md`, inside the `WordPress 7 Engine` registry block.

**Before, line 72:**

```text
Local path: `~/Projects/Development/wordpress-7`
```

**After:**

```text
Local path: `~/wordpress-7`
```

Nothing else changes. This reproduces the defect that actually occurred on 2026-08-25, when the
Engine moved and its registry block went on naming the old path, which `structure-check` passed twice
because the path is well formed and its check 12 only asks what form a path is written in. `~/wordpress-7`
does not exist on this machine; `~/Projects/Development/wordpress-7` does.

The line is restored immediately after the run, and the restoration verified.

**A confound, named in advance rather than removed.** The session note at lines 55–56 of the same
document still says `~/Projects/Development/wordpress-7`, so the correct path remains elsewhere in
the file the tool is reading. Removing it would make two edits and stop being one variable. Leaving
it is also the better test: improvisation is now a known behaviour of this tool, observed twice on
check 7, and a check that only works when nothing nearby contradicts the broken line is not a check.

---

## Predicted result per numbered check

| Check | Component | Predicted | Predicted reason |
| --- | --- | --- | --- |
| 1 | WP Themes | pass | Unchanged. Relative address `wp-themes/` resolves and the folder is there. |
| 1 | **Engine** | **fail** | The address is not a path, so the locating line is the local path beneath it, and no folder exists at `~/wordpress-7`. |
| 2 | WP Themes | pass | Unchanged. |
| 3 | WP Themes | pass | Unchanged. |
| 4 | WP Themes | pass | Unchanged. Resolves `../` to this folder. |
| 5 | WP Themes | n/a | Unchanged. No override named, none present. |
| 6 | WP Themes | pass | Unchanged. Absence evidenced by a listing. |
| 2–6 | **Engine** | **unpredictable, and that is the finding** | The prompt never says what happens to rows 2 to 6 when row 1 cannot find the folder. Cascade of some kind is expected, fail or n/a, and whichever it does is a defect in the prompt's silence rather than a fact about the scope. |
| 7 | (read set) | pass | Only folders the registry named, plus the scope root, should be opened. |

**Final line:** `Failed rows: N` with N at least 1.

## What counts as the negative half passing

Three things together, and all three are required:

1. The Engine's check 1 row **fails**.
2. It **names the reason**: the folder is not at the path the registry declares. A bare "fail" with
   no located-path evidence does not count.
3. **Nothing correct fails.** Every `WP Themes` row comes back exactly as it did in the repaired run.

## What would falsify the check rather than the scope

**The Engine's check 1 row passes or returns n/a.** Two specific routes, both plausible:

- **The n/a clause stretches.** Check 1 says a component "whose address is a URL or a synced-store
  location, with no local path line and no folder you can reach, is n/a rather than a failure". The
  Engine's address is `none. No copy of this folder exists off this machine.`, which is neither of
  the two named forms, and it does have a local path line, so the clause should not apply. If the
  tool applies it anyway, the fourth address form is uncovered by check 1 and the check has a hole
  exactly where `0007` put a new form.
- **The tool locates the folder from the session note.** If check 1 passes because the correct path
  was found elsewhere in the document, the check does not own its own locating rule, and the row is
  reporting on the tool's resourcefulness rather than on the registry.

If either happens, the check fails its own purpose on the one defect it was written for, and the
right response is to fix check 1 rather than to explain the result.

**A third outcome worth naming:** if the tool locates the Engine at its real path after the registry
sent it elsewhere, **check 7 should fail**, because that folder is not the one the registry named. A
run where check 1 passes and check 7 also passes means the two rows disagree and neither noticed.

## Re-run rule, fixed in advance

A single run does not settle a row. If the result disagrees with this prediction on any row, that arm
is run again before anything is concluded, and both runs are committed. This rule exists because the
control arm of the second run overturned a confirmation that had rested on one observation.

---

# Outcome

**Run:** 2026-08-29, repaired prompt, scope with the single planted line. Run twice, per the re-run
rule fixed above, though no firmly predicted row disagreed: the control arm of the second run had
already shown that agreement on one run can be luck as easily as disagreement. Logs are
`2026-08-29-registry-check-3-negative.log` and `-repeat.log` in [`../runs/`](../runs/). Everything
above this line was written before the defect was planted and is unedited.

## The negative half passes, on all three criteria

**1. The Engine's check 1 row failed, in both runs.**

**2. It named the reason, in both runs, with the resolution shown.** From the first:

> not a relative path, so line 72 used: "Local path: `~/wordpress-7`"; resolved to
> `/home/kostritsaalex/wordpress-7` ($HOME=/home/kostritsaalex); `test -d` returned MISSING. No
> visible text in PROJECT.md says this component is not attached yet.

It quoted the address line to justify falling through to the local path line, resolved the tilde and
said what it resolved to, probed the result, and closed off the one escape clause the row allows.

**3. Nothing correct failed.** Every `WP Themes` row came back exactly as in the repaired positive
run, in both negative runs.

**Neither falsification route was taken.** The n/a clause did not stretch to cover the `none` address
form. The session note, still carrying the correct path two dozen lines above, was not used to
rescue the row. The check owned its own locating rule, which was the thing most in doubt.

So `registry-check` catches the defect it was written for, on the naturally occurring instance that
motivated it, reproducibly.

## The cascade is real, unstable, and worse than predicted

Rows 2 to 6 for the Engine were pre-registered as unpredictable, on the grounds that the prompt never
says what happens to them when row 1 cannot find the folder. That silence is now measured.

First run: all five failed with a bare `no evidence`. Repeat: four failed with `no evidence` plus a
reason, and **check 6 passed**, on this evidence:

> Ran `test -e /home/kostritsaalex/wordpress-7/PROJECT.md`, returned "no PROJECT.md".

A folder that does not exist contains no `PROJECT.md`. The statement is true, the row is green, and
it means nothing whatever. `Failed rows` came back 6 in one run and 5 in the other, on an identical
prompt against an identical scope.

This is the same defect class as the check 6 intermittency in the control arm, and this is its
sharpest instance: a row with no basis for a verdict, forced to produce one, produces a different one
each time and sometimes a nonsensical one. One planted defect produced one true finding and five
derived rows of noise, which on a scope with six components would be one finding and twenty-five.

The repair is a rule the prompt did not have: **when check 1 fails for a component, rows 2 to 6 for
that component are `n/a`, evidenced by naming check 1 as the reason.** They are not failures. Nothing
is wrong with stubs nobody could read.

## What this run still does not settle

Check 4 has never failed on a real defect. Its only failures were the false ones from comparing `../`
as text, now repaired. A scope whose components point at a parent that has moved has not been built,
and that is the other thing this check claims to catch.

Check 7 remains untestable by any honest run, as the second pre-registration said: a tool that stays
inside the read set passes it whether the row is well specified or not.

## Correction to this file's header, added 2026-08-30 review

The section describing the variable says the planted defect "reproduces the defect that actually
occurred on 2026-08-25". The date is wrong and so is the implication. What happened on 2026-08-25 was
a deliberate break during the `0.7.0` validation, when the Engine's block was rewritten to
`Address: ~/wordpress-7` to test `structure-check` 11. The real staleness is a different event: the
folder moved at some unrecorded time and the block was found naming the old path on 2026-08-29.

The sentence also implied `structure-check` had passed a stale path twice. It had not. It passed that
block twice on 2026-08-25, when the path was still correct.

The predictions above are unedited and were unaffected by this: the variable planted was the same
either way. The error was in the account of where the defect came from, and it is the class of defect
this repository has spent two sessions cataloguing, found by reading the artefact back.
