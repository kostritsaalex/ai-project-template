# Prediction: check 4's negative half, both branches

**Written:** 2026-08-29, before either arm is planted.  
**Subject:** `registry-check.md` check 4 as shipped in `0.9.3`.

**Why this exists.** `0.9.3` shipped a row that had been made stricter and had never been seen to
fail. Its two runs were positive, on an unmodified scope, and by this project's own rule a positive
run says only that the check does not obstruct a correct document. The three falsifiers registered
for those runs all asked *which line the evidence cites*; none asked whether the row catches a wrong
parent address, which is the defect it exists for.

The `0.9.0` changelog already recorded that check 4 has never failed on a real defect. That is still
true, and this is the run that changes it or does not.

**New in these arms: the plant is in a component's stubs, not in `PROJECT.md`.** Every previous plant
edited the registry. These edit the thing the registry is checked against, which is the other half of
the comparison and has never been the broken side.

---

## Arm A — the relative branch

`wp-themes/AGENTS.md` and `wp-themes/CLAUDE.md`, line 11 in each.

```text
before:  ../
after:   ../../
```

Both stubs, because a scope that moved leaves both stale; changing one would plant a different defect,
two stubs disagreeing, which is not what this arm tests. `../../` resolves to the folder above the
scope, `.../Projects/Development`, which is a real folder and not this one — so the row must fail on
the comparison rather than on a path that does not exist.

**Predicted:** row 4 fails for `WP Themes`, the evidence quotes both stub lines, gives the path
`../../` resolved to, and says that it is not this folder. Every other row unchanged from the
positive runs, both Engine rows included. `Failed rows: 1`.

## Arm B — the string branch

`~/Projects/Development/wordpress-7/AGENTS.md` and `CLAUDE.md`, line 12 in each.

```text
before:  OneDrive, Projects/Development/WordPress-7
after:   OneDrive, Projects/Archive/WordPress-7
```

One path segment, which is how a moved scope actually differs. Both stubs, for the same reason as
Arm A.

**Predicted:** row 4 fails for `WordPress 7 Engine`, the evidence quotes the stub line and
`PROJECT.md` line 39, and names the mismatch. Every other row unchanged, both `WP Themes` rows
included. `Failed rows: 1`.

## What counts as the negative half passing

For each arm: row 4 fails for the planted component, the evidence points at the differing text, and
nothing else fails.

## What would mean the row is now too strict rather than right

- **Any row other than 4 failing.** The plant touches an address line and nothing else. Row 3 reads a
  different line of the same file; rows 1, 2, 5, 6 and 7 do not read these files at all. A failure
  elsewhere means the row's strictness has spread.
- **A failure whose evidence cannot point at the differing text.** A row that fails without showing
  what differs is a row that has stopped being checkable, which is worse than one that misses.
- **Arm A failing on "path does not exist".** `../../` resolves to a real folder. If the evidence says
  the path is missing rather than that it is the wrong folder, the row is testing existence, which is
  row 1's job, rather than agreement.

## Restoration

Four stub files are backed up with checksums before anything is planted. Each arm is restored and
verified byte-identical before the next is planted, and the whole set verified at the end.

## Re-run rule

Any row disagreeing with this prediction gets that arm run again before anything is concluded.
