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
| `2026-08-29-registry-check-7-row4-comparand.log` | `registry-check.md` at `0.9.3`, check 4 rewritten to name which line it compares against | Does the row ask one question | **No plant.** The scope discriminates as it stands: one component carries `../`, the other the synced-store address verbatim | 2026-08-29 |
| `2026-08-29-registry-check-7-row4-comparand-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |
| `2026-08-29-registry-check-8-row4-negative-relative.log` | `registry-check.md` at `0.9.3` | Check 4's negative half, relative branch | **Planted in a component's stubs, not in `PROJECT.md`.** `wp-themes/AGENTS.md` and `CLAUDE.md` line 11, `../` to `../../`, in the scope's own filesystem under OneDrive on the Windows side | 2026-08-29 |
| `2026-08-29-structure-check-1-deleted-override.log` | `structure-check.md` at `0.9.3`, component variant | **First `structure-check` log in this repository.** A deleted override: both `wp-themes` stubs name `REPOSITORY.md`, and no such file exists | Planted in the component's stubs; restored after | 2026-08-29 |
| `2026-08-29-structure-check-1-deleted-override-repeat.log` | Same | Repeat, because row 10's result is an absence | Same | 2026-08-29 |
| `2026-08-29-structure-check-2-row4-positive.log` | `structure-check.md` with row 4 rewritten to name its comparison | Row 4 positive, no plant | `wp-themes` correct | 2026-08-29 |
| `2026-08-29-structure-check-2-row4-positive-repeat.log` | Same | Repeat, a pass being evidence of an absence | Same | 2026-08-29 |
| `2026-08-29-structure-check-2-row4-negative.log` | Same | Row 4 negative | One word changed in `wp-themes/AGENTS.md` only, deliberately not the naming line; restored after | 2026-08-29 |
| `2026-08-29-registry-check-9-deleted-override.log` | `registry-check.md` at `0.9.3` | The same planted folder, seen from the scope | Same | 2026-08-29 |
| `2026-08-29-registry-check-8-row4-negative-string.log` | Same | Check 4's negative half, string branch | **Planted in a component's stubs, not in `PROJECT.md`.** The Engine's `AGENTS.md` and `CLAUDE.md` line 12, one path segment changed, in the WSL filesystem | 2026-08-29 |
| `2026-08-30-interview-length-a1.log` | Framework at `v0.7.0`, from a git worktree at that tag | Arm A, first run | **Not a check run and not a real project.** A scratch scope built for this experiment and deleted after: `storefront/` (astro `package.json`, `src/`, `public/`), `catalogue-photos/2026/` (three empty `.jpg`), `supplier-notes/` (two `.md`). Never written to; tree checksum `47809391e908d576d7fae6d9657e7e31` verified unchanged after all four runs | 2026-08-30 |
| `2026-08-30-interview-length-a2.log` | Same | Arm A, repeat | Same scope, unchanged | 2026-08-30 |
| `2026-08-30-interview-length-b1.log` | Framework at `HEAD` = `7e7f8df`, which is `0.10.2` plus the one-clause `procedure.md` repair `3363d09` | Arm B, first run | Same scope, unchanged | 2026-08-30 |
| `2026-08-30-interview-length-b2.log` | Same | Arm B, repeat | Same scope, unchanged | 2026-08-30 |

Fifteen of these ran against the `WordPress 7` scope at `OneDrive, Projects/Development/WordPress-7`, from
inside WSL, with the Engine's folder granted to the session because it sits outside the scope's
filesystem.

**Two of these logs were produced by planting in a component's stubs rather than in `PROJECT.md`.**
Every other plant edited the scope document; the row-4 negative arms edited the thing the registry is
checked against, which is the other side of the comparison. A reader comparing these logs to the
earlier ones would otherwise assume the scope document was the broken thing. The four stub files
across two filesystems were snapshotted with checksums before anything was planted, each arm's pair
restored from that snapshot rather than retyped, and all four verified byte-identical afterwards.

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
e1588659e9633cd23a01e751ed882ee0  2026-08-29-registry-check-7-row4-comparand.log
11d6e5eadeb66b33f9cfc0d4ab367c6e  2026-08-29-registry-check-7-row4-comparand-repeat.log
43d5cce31488a7574bf09b029e7b79cc  2026-08-29-registry-check-8-row4-negative-relative.log
4c13e40c9817e3ff4e7d20703e1c30c2  2026-08-29-registry-check-8-row4-negative-string.log
4d0eb949757a7e9165333018697010be  2026-08-29-registry-check-9-deleted-override.log
f3bc602e06e2650ab4a21cc7449a352a  2026-08-29-structure-check-1-deleted-override.log
10ee2c1eb867132b3635fda4efe6a974  2026-08-29-structure-check-1-deleted-override-repeat.log
45fa11257420e2f0726c2b12f7f4d7aa  2026-08-29-structure-check-2-row4-positive.log
6b121ec91c4b55d2bcc51b0d6586dfc0  2026-08-29-structure-check-2-row4-positive-repeat.log
c3b8f56af7b03aa64eb4291eecb45889  2026-08-29-structure-check-2-row4-negative.log
ecc4170878cb75d120a0fa9711f21ac6  2026-08-30-interview-length-a1.log
c411a8a2c6f93934360288239c487558  2026-08-30-interview-length-a2.log
80c4c47ded6f9ca5d0b46569bbba7d8b  2026-08-30-interview-length-b1.log
f65aca1671634a46eead89db142bb645  2026-08-30-interview-length-b2.log
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

---

## The four interview logs are a different kind of run, and the index should say so

Every other log here is a **check** run against a real project scope. The four
`2026-08-30-interview-length-*` logs are **setup** runs against a scratch folder, and what they
record is a question block rather than a verdict table. They were produced by `claude -p`, one fresh
non-interactive session each, with `Write`, `Edit` and `NotebookEdit` disabled so no run could write
into the scope — a deviation from an ordinary adoption, identical across both arms, recorded in
[`../predictions/interview-length-0.7-against-head.md`](../predictions/interview-length-0.7-against-head.md).

The prompt was `blueprints/setup/new-project.md`'s own paste block with the two addresses filled in.
That file is **byte-identical between `v0.7.0` and `HEAD`**, so the two arms' prompts differ in
exactly one line, the framework path.

They are evidence for two things. The pre-registered one is length, and it came out indeterminate by
the thresholds set in advance. The one nobody registered is worth more: **arm A run 1 and arm B run 2
each asked a question the setup procedure explicitly forbids**, and they are different questions in
different versions. `a1` asks whether `.docs/` exists while stating in the same sentence that it does
not — a question about something it had already read. `b2` asks the person for each component's
posture, which Step 4 says in as many words is not a question and must be proposed. Two violations of
two named rules in four runs, on both sides of four releases.
