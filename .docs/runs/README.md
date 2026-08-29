# Run logs

Raw output of check runs, committed verbatim and never edited. Formatting, stray wording and all.

They are here because a conclusion that rests on an artefact needs the artefact to still exist. On
2026-08-29 a finding about `registry-check` was disputed against a two-row summary of a table that
actually had three rows, and the row carrying the finding was the one the summary had dropped. It was
settled by opening the raw log and by nothing else. That log was in `/tmp` at the time.

A paraphrase of a run is not the run. If a log and a summary disagree, the log is right.

---

| File | Prompt version | Arm | Scope state | Date |
| --- | --- | --- | --- | --- |
| `2026-08-29-registry-check-1-original.log` | `registry-check.md` as committed in `381b200`, before any repair | First run, as written | `WordPress 7`, believed correct: registry paths repaired earlier the same day, Engine override and its stub lines removed the same day | 2026-08-29 |
| `2026-08-29-registry-check-2-repaired.log` | `registry-check.md` as committed in `49b25dd`, after both repair passes | Second run, repaired prompt | Same scope, unchanged since the first run | 2026-08-29 |
| `2026-08-29-registry-check-2-control.log` | `registry-check.md` as committed in `381b200`, verified byte-identical to the first run's prompt | Second run, control: the original prompt again | Same scope, unchanged since the first run | 2026-08-29 |
| `2026-08-29-registry-check-3-negative.log` | `registry-check.md` as committed in `49b25dd` | Negative half, first run | Same scope with **one line deliberately broken**: the Engine's registry local path set back to `~/wordpress-7`, a folder that does not exist. Restored immediately after, verified byte-identical to the copy taken before planting | 2026-08-29 |
| `2026-08-29-registry-check-3-negative-repeat.log` | `registry-check.md` as committed in `49b25dd` | Negative half, repeat of the same arm | Same broken scope, unchanged between the two runs | 2026-08-29 |
| `2026-08-29-registry-check-4-shipped.log` | `registry-check.md` as shipped in `0.9.0` plus the check 6 rewrite, a text no earlier run had used | Negative half against the shipped text | Same planted defect, restored after | 2026-08-29 |
| `2026-08-29-registry-check-4-shipped-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |
| `2026-08-29-registry-check-5-unreachable.log` | `registry-check.md` at `0.9.1`, row 1's cascade collapsed from three cases to one condition | A component the registry never claimed is on this machine | Engine's address replaced by a repository URL and its local path line deleted; restored after | 2026-08-29 |
| `2026-08-29-registry-check-5-unreachable-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |
| `2026-08-29-registry-check-6-cut-clause.log` | `registry-check.md` at `0.9.2`, differing from the `0.9.1` prompt by exactly the cut restatement clause | The second razor measured on a check: does removing a clause that prescribes nothing change anything | Same plant as run 5, restored after | 2026-08-29 |
| `2026-08-29-registry-check-6-cut-clause-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |

All eleven ran against the `WordPress 7` scope at `OneDrive, Projects/Development/WordPress-7`, from
inside WSL, with the Engine's folder granted to the session because it sits outside the scope's
filesystem.

**These files need an override to be committed at all.** A global `*.log` ignore excluded all five
silently on the first attempt, and the commit went through carrying this index and none of the files
it describes. The repository's `.gitignore` now negates it. If a log added later does not appear in
`git status`, that is why, and `git check-ignore -v` on the file will name the rule.

Checksums at commit time, so a later edit is detectable:

```text
b67b4df0208b0a9461f18e77871858e7  2026-08-29-registry-check-1-original.log
cf722de35201272594e2f9b27cd9a778  2026-08-29-registry-check-2-repaired.log
6bdd042245658a913d25c0aadaf40d8c  2026-08-29-registry-check-2-control.log
f05464775dff20994c5dc5806fdb18f7  2026-08-29-registry-check-3-negative.log
38b7e3e0dfa615069558410b7b817e8d  2026-08-29-registry-check-3-negative-repeat.log
c060bcecf5e18b3ab770524b2bcdba06  2026-08-29-registry-check-4-shipped.log
c889c6f6960f8d82debaa20e393d709e  2026-08-29-registry-check-4-shipped-repeat.log
65b0ddf0ca1b124524710595d7f25b20  2026-08-29-registry-check-5-unreachable.log
605d88261b6ebfd8a79012ffb5f7dc9e  2026-08-29-registry-check-5-unreachable-repeat.log
515cf7ea5dd5a319e77992b38e977581  2026-08-29-registry-check-6-cut-clause.log
d8dd1ebd4b577c9fc1feb8e965684f8b  2026-08-29-registry-check-6-cut-clause-repeat.log
```

## What they are evidence for

The scoring of three pre-registrations,
[`registry-check-first-run.md`](../predictions/registry-check-first-run.md) and
[`registry-check-second-run.md`](../predictions/registry-check-second-run.md) and
[`registry-check-negative-run.md`](../predictions/registry-check-negative-run.md). Read those for
what was predicted; read these for what happened.

Two pairs carry most of the weight.

The control against the first log: check 6 passes in one and fails in the other, on a byte-identical
prompt against an unchanged scope. That pair is the whole evidence for the limit now stated in
[`blueprints/checks/README.md`](../../blueprints/checks/README.md), that an under-specified row
returns a confident table either way.

The two negative logs against each other: check 1 fails identically in both, which is the check doing
the job it exists for, while the rows downstream of it disagree between the runs. In the repeat,
check 6 **passes** for a component whose folder does not exist, on the reasoning that a missing
folder contains no `PROJECT.md`. That is true and worthless, and it is the clearest single artefact
of a row being forced into a verdict it has no basis for.
