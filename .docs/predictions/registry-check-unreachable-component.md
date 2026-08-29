# Prediction: a component the registry never claimed was on this machine

**Written:** 2026-08-29, before the change is planted and before the run.  
**Subject:** `registry-check.md` with row 1's cascade rewritten from an enumeration to one rule:
*unless this row confirmed the folder exists, rows 2 to 6 are n/a and name this row.*

**Why.** The cascade shipped in `0.9.0` fired on one of row 1's three outcomes. The other two, a
component not yet attached and a component whose address is a URL or synced store with no reachable
folder, left rows 2 to 6 with no folder to read and no rule telling them to stay silent: the exact
pathology the cascade was written for, one branch over in the same row. ArtGlina declares
`artglina-ua` as a GitHub URL and meets it on its first run.

The fix replaces three cases with one condition rather than adding a fourth clause.

---

## The variable

`WordPress-7/PROJECT.md`, the `WordPress 7 Engine` block. Its address becomes a plausible repository
URL and its local path line goes, which is what a component hosted off this machine actually looks
like.

**Before, lines 71–72:**

```text
Address: none. No copy of this folder exists off this machine.
Local path: `~/Projects/Development/wordpress-7`
```

**After, line 71:**

```text
Address: https://github.com/kostritsaalex/wordpress-7-engine
```

One variable, expressed in two lines, in the same way the path plant was: the component stops being
one this machine holds. No invented material beyond the URL itself. Restored and verified after.

## Predicted

| Check | Component | Predicted |
| --- | --- | --- |
| 1 | WP Themes | pass |
| 1 | Engine | **n/a**, on the URL branch: a repository address, no local path line, no reachable folder |
| 2–6 | Engine | **n/a**, all five, each naming row 1 |
| 2, 3, 4, 6 | WP Themes | pass |
| 5 | WP Themes | n/a |
| 7 | (read set) | pass, and it should list only the scope root and `wp-themes` |

**Final line: `Failed rows: 0`.**

## The too-wide outcome, registered as the real risk

`Failed rows: 0` is the correct answer here and is also the danger. On this scope it is honest,
because `WP Themes` was genuinely audited and passed. On a project whose components all live off this
machine, the same rule produces a table of nothing but `n/a` and a `Failed rows: 0` that reads as a
clean pass while having audited nothing at all.

That is not a defect the run can show, because this scope has a local component. It is a consequence
of the rule, it is honest, and a reader meeting a green table has no way to tell the two apart. **If
the run confirms the rule behaves as predicted, this belongs in "What this check cannot see" in those
words** — not left for somebody to discover the day a green table means nothing.

## What would falsify the fix

- **Any Engine row coming back `fail`.** Nothing is wrong with that component. A failure would mean
  the rule reads "unreachable" as "broken", which is the error the `0.7.0` work spent a decision
  avoiding: a component with no copy off this machine is a component, not a defect.
- **Any `WP Themes` row turning `n/a`.** Its row 1 confirms a folder, so nothing licenses silence in
  its column. Suppression spreading to an audited component is worse than the noise this replaced.
- **Check 7 listing a folder for the Engine.** There is no folder to open. If it appears, the tool
  went looking beyond the read set.

## Re-run rule

As before: any row disagreeing with this prediction gets the arm run again before anything is
concluded.
