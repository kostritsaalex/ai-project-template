# Handover

What the sessions that built `0.5.0` through `0.7.0` knew and the rest of the repository does not
say. Written 2026-08-25, when the work moved from a cloud assistant reading the Windows checkout to
an assistant running inside WSL.

**Tonight's state, 2026-08-29:** three releases are provisional and cannot be validated, because the
only instrument is an adoption and the adoption has been refused twice. Do not treat the volume of
work in the log as progress until that is resolved. The plan in `backlog.md` starts with a measurement
and explicitly forbids repairing the interview before it is reported.

State and open work are in [`backlog.md`](backlog.md). Why the framework is shaped as it is, in
[`decisions/`](decisions/). This file holds method, calibration and the facts of the move.

---

## How this project works

**Nothing enters a blueprint without being run.** Principle 6 is not decoration. Every rule in the
framework that survives was either measured or observed on a real project, and the ones that were
argued for and never run are the ones that turned out wrong. The four preserve rules on the `Assets`
posture shipped for two releases without ever being used once, and when the posture was finally run
they turned out to describe a folder that does not exist.

**Test a check both ways round.** A positive run says only that the check does not obstruct a correct
document. Whether it catches the thing it was written for is shown by breaking the document
deliberately and running again in a fresh session. `0.7.0` taught `structure-check` 11 what a valid
address is, and the negative run is what proved it: the block was rewritten to
`Address: ~/wordpress-7`, the check failed that row and nothing else, and it named the reason. Do not
accept a check as working on a positive run alone.

**Repeat the run whose evidence is an absence, not the one whose evidence is a quotation.** How many
times an arm needs running is not a matter of caution, it follows from what the row had to do to
produce its answer. A failing row's evidence is self-verifying: both stub lines quoted, the path they
resolved to, the differing segment named. None of that can be produced without looking, so one run
settles it. A pass can be produced by not looking, and an `n/a` paragraph more easily still, which is
why every `n/a` behaviour this framework has shipped was run twice and why check 6 flipped between
runs for a week before anyone noticed. Spend the repeat where the evidence is silence.

**Every change carries at least one control that is not derived from the hypothesis.** The
pre-registered arms come out of the same understanding that produced the change, so they test
whether the change does what its author meant. They cannot test whether its author meant the right
thing, and that is the failure that keeps happening here. Before running, name a case the change
would break **if the understanding behind it were wrong** — a case its predecessor covered, an input
the new shape has no reason to handle, the same question asked from the other side — and run it
alongside the registered arms.

This is not caution, it is the only arm with a record. Two changes running, the unregistered control
found a real defect in the repair *after every pre-registered arm had held*: `0019`'s first shipped
command skipped a non-version changelog heading and compared against the release below it, and
`0020`'s first version resolved both sides to bare filenames and lost coverage its predecessor had.
Five times in this project's log a check's defect has surfaced that way rather than by review, and
none of the five came from the arms that were written down first.

**Disclose it like any other run.** A control found this way goes in the report as unregistered, with
what it broke, and the prediction file is not edited afterwards to make it look foreseen.

**A correct repair still costs something, and the cost lands where nothing counts.** Every change
made on 2026-08-29 was defensible and most had a run behind it. Each also added justification, which
is what a careful repair does. The sum was an interview the owner refused to answer, saying
initialization had degraded even as consistency improved.

Ask of a repair not only whether it is right but **where its weight lands and whether anything
measures that place.** The shipped-line metric covers what an adopted project carries. Nothing covers
the check prompts, and nothing covers the setup path, and both grew all week. A reason for a rule
always looks like it belongs beside the rule, which is why justification accumulates in exactly the
documents no measurement protects.

**Judge by the artefact, not the report.** Three times during the `0.6.0` validation a report ending
in "Failed checks: 0" contained a detail that does not exist: folders listed in a directory that
holds none of them, and a claim about the contents of a file that says no such thing. None changed a
verdict. All three were caught only by opening the files.

**Judging by the artefact means judging whether the artefact works.** A sharpening of the rule
above, and it cost an experiment to learn. On 2026-08-30 four arms were asked to change the sender on
a WordPress install's outgoing mail. Three registered the correct filters and **shipped code that
could not run**: the tree's `wp_mail()` ignored those filters, in a file all four had read. Only the
fourth checked whether its own fix could take effect, and it was the arm a file-level scoring would
have marked as the violation.

**A diff in the right files is not work.** Where a run's verdict turns on what it produced, the
verdict has to include whether the thing functions, and that is a different act from reading the
diff. The same run also showed the cost of not doing it: the naive scoring pointed at the opposite
conclusion from the correct one, in the direction most flattering to the framework.

**Two runs of one prompt differ.** The same attach prompt, on the same folder, offered a
"use the WordPress platform fragment" option once and not the next time. The absence of a behaviour
in a single run proves nothing.

**A decision that changes a rule gets a record.** `decisions/` is newest last, one file per decision,
and superseded records are marked rather than deleted. Each carries what the decision cost, stated
plainly, including risks accepted with no mitigation.

**An `Origin` section names the channel, not the author.** The framework is reviewed by a second
assistant whose prompts reach a working session through the owner. From inside the session, a message
may be his own words, the review's relayed, or both, and nothing distinguishes them. So a record
attributes the *decision* to the owner, who makes it, and describes everything else as having arrived
rather than as belonging to someone: "arrived with the review", "this session added". Where the
session can point at evidence for authorship it may say so; otherwise it may not.

This is the same discipline `git log -S` enforced on a claim about a past run. A sentence about who
established what is a claim like any other, and writing it from memory is how a false one gets in.
`0001` through `0009` predate this and name people for reasoning that came by that route. They stand
as written.

**The backlog has three sections and they mean different things.** `Now` is what has a quote behind
it and needs no decision. `Release` needs a decision or an experiment. `Recorded, not tasks` is
evidence worth keeping that nobody has to act on.

---

## Where the evidence is thin

Everything the framework knows about filesystem boundaries, path notes and session notes comes from
one project, one machine and one person, running Windows with WSL. macOS with a network volume is
expected to behave the same way and has never been tried. This is said out loud in
[`architecture.md`](architecture.md) so a reader can weigh it.

The `Assets` posture has been run end to end exactly once, on a folder of WordPress theme sources.
No project has yet used it for the case it was written for, a folder of photographs, documents and
business material. ArtGlina is that project and is still on the pre-`0.5.0` shape.

The assets override, `ASSETS.md`, has never been used at all.

---

## The move

The framework was worked on through a checkout on the Windows side, at
`~/Repositories/ai-project-template` as Git Bash resolves it. It now lives inside WSL at
`~/Projects/Frameworks/ai-project-template`.

`PROJECT.md` was corrected to that path on 2026-08-29. The new location is native to the WSL
filesystem, so nothing holds the path up but the filesystem itself, and the path note explaining the
old arrangement was deleted rather than rewritten. That is the framework's own rule about local paths
applied to itself.

**Both copies still exist as of 2026-08-29.** The Windows one, at
`/mnt/c/Users/kostr/Repositories/ai-project-template` read from this side, is a complete checkout with
its own `.git`. It is no longer the one being worked in and it is not the one `PROJECT.md` describes.
Until it is removed the two will drift.

---

## Two things that bit repeatedly

**The Engine and its scope have confusable names.** The `WordPress 7 Engine` is a WordPress
installation in the WSL home filesystem, at `~/Projects/Development/wordpress-7` since it moved on
2026-08-29. `WordPress-7` is the project scope in a synced store on the Windows side. Confusing them
cost time twice in one session, both times when a listing looked wrong and was in fact showing the
other folder. The Engine's old path, `~/wordpress-7`, still appears in `0007` and in the record of
the negative check run; there it is history rather than a location, and nothing resolves at it now.

**`\\wsl.localhost\...` is not an address and barely a path.** It reaches the WSL filesystem from
Windows, and on any other machine it resolves to that machine's WSL and returns a different folder
rather than an error. It was rejected as an address form in `0007`, it broke a tool in one session,
and the desktop bridge refuses UNC paths outright.
