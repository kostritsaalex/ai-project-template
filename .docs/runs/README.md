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

All three ran against the `WordPress 7` scope at `OneDrive, Projects/Development/WordPress-7`, from
inside WSL, with the Engine's folder granted to the session because it sits outside the scope's
filesystem.

Checksums at commit time, so a later edit is detectable:

```text
b67b4df0208b0a9461f18e77871858e7  2026-08-29-registry-check-1-original.log
cf722de35201272594e2f9b27cd9a778  2026-08-29-registry-check-2-repaired.log
6bdd042245658a913d25c0aadaf40d8c  2026-08-29-registry-check-2-control.log
```

## What they are evidence for

The scoring of two pre-registrations,
[`registry-check-first-run.md`](../predictions/registry-check-first-run.md) and
[`registry-check-second-run.md`](../predictions/registry-check-second-run.md). Read those for what
was predicted; read these for what happened.

The single most consequential line across the three is in the control log: check 6 passes there and
fails in the first log, on a byte-identical prompt against an unchanged scope. That pair is the whole
evidence for the limit now stated in
[`blueprints/checks/README.md`](../../blueprints/checks/README.md), that an under-specified row
returns a confident table either way.
