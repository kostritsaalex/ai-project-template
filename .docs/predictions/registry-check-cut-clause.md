# Prediction: the cut clause changes nothing

**Written:** 2026-08-29, before the run.  
**Subject:** `registry-check.md` with the sentence restating row 1's three cases removed.

**What this run is for.** It is the first controlled measurement of the second razor on a check
rather than a judgement. `0008` says a rule earns its place only if an assistant would do otherwise
without it, and every application of it so far has been settled by reading, including the reading
that cut this clause. Here the claim can be measured, and the arm is already built.

---

## The variable

The prompt differs from the one that produced
`.docs/runs/2026-08-29-registry-check-5-unreachable.log` by exactly this, and by nothing else:

```text
-   row as the reason. That covers every outcome above except a confirmed folder, whether this row
-   failed, or was n/a for a component not yet attached, or was n/a for an address that never claimed
-   the folder was on this machine. They are not failures: nothing is wrong with stubs nobody could
-   read, and a folder that does not exist will satisfy an absence check for no useful reason.
+   row as the reason. They are not failures: nothing is wrong with stubs nobody could read, and a
+   folder that does not exist will satisfy an absence check for no useful reason.
```

The plant is the same as that arm's: the Engine's address replaced by
`https://github.com/kostritsaalex/wordpress-7-engine`, its local path line deleted. Restored and
verified after.

Two baseline logs exist for this arm and agree with each other on every row, which is what makes a
single run here worth something.

## The prediction, which is my own claim stated so it can fail

Every row identical to both baselines: `WP Themes` pass, pass, pass, pass, n/a, pass; the Engine n/a
on row 1 for a URL address with no reachable folder, and n/a on rows 2 to 6 with each evidence naming
row 1; check 7 pass listing two folders; **`Failed rows: 0`**.

## What would falsify it

- **Any Engine row that is not `n/a`.**
- **Any row whose evidence stops naming row 1** as the reason for its silence.
- **The same verdicts reached by visibly different reasoning.** This is the outcome to look for
  hardest and the easiest to score wrong. A clause can change how a tool arrives somewhere without
  changing where it arrives, and `0008` cuts on behaviour, not on verdicts. If the table agrees and
  the evidence column has changed in kind — a different basis for the n/a, a reason invented where
  one was quoted, hesitation where there was none — then the clause was doing work and the
  prediction is wrong however green the table looks.

Verdict comparison is not enough for this run. The evidence column of all three logs gets read
against each other, line by line.

## If it fails

The clause goes back, and `0.9.2` records that `0008` was applied by reading and overturned by
running. That is worth more than the clause.
