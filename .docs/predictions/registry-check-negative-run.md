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
