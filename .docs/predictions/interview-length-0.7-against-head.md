# Pre-registration: does the framework produce the interview's length, or does the reader?

**Written 2026-08-29, before any arm is run. Committed before the first run.**

---

## The question

The interview the owner refused on 2026-08-29 was 937 words. The interview he accepted at `0.7.0`
he recalls as four or five questions with answer options. Measurement on 2026-08-29 established
that the framework's setup path grew **four non-blank lines** between those two versions, that the
framework ships **no interview text at all**, and that the same harness — Claude Code — rendered
both.

So the length is produced by something. Two candidates, and they are separable with the harness
held constant:

**The framework.** `0.10.0` and `0.10.2` added 23 lines to `blueprints/project/README.md` about the
two default principles, and `0.10.0` simultaneously told the assistant to offer them **aloud**. That
is the only place in four releases where the framework put justification directly in the path of
something a tool was instructed to speak. If that is the cause, an interview generated from the
`0.7.0` tree is materially shorter than one generated from `HEAD`.

**The reader.** Claude Code is a harness, not a reader. The model under it can change without the
name changing, and a week passed. Five topics and a style paragraph work only as well as whoever
renders them.

This is the second instance of the worry `0008` already carries — a rule recorded as a prediction
about a model rather than a property of a rule — and it belongs beside the first.

## Why this is worth two runs rather than an argument

The `+23 lines` claim was written on 2026-08-29 as an explicit hypothesis and marked as one. Acting
on it without running it is the state principle 6 exists to prevent, and the whole of 2026-08-29
was spent cataloguing what happens when a fix is written while composing the thing that carries it.

## The arms

**Arm A: the framework at `v0.7.0`,** run from a git worktree at that tag, created with
`git worktree add <scratch>/arm-a-v0.7.0 v0.7.0`. A worktree rather than four copied files,
deliberately: the hypothesis is about `blueprints/project/README.md`, so the arm has to carry the
whole framework at that tag and not the setup folder alone.

**Arm B: the framework at `HEAD`,** the working repository. `HEAD` is `7e7f8df` and includes the
one-clause `procedure.md` repair committed today as `3363d09`.

`blueprints/setup/new-project.md` is **byte-identical between the two tags**, confirmed by
`git diff v0.7.0 HEAD -- blueprints/setup/new-project.md` returning empty. So the prompt pasted into
both arms is the same text, differing only in the framework path it names. That is the control.

## The scope both arms meet

A scratch folder built for this run, deleted afterwards. Not ArtGlina, not any real project, and
never written to. **Running this against ArtGlina would consume the blind adoption that three
provisional releases are waiting on.**

```text
scope/
  storefront/          package.json (astro), src/nav.js, public/index.html
  catalogue-photos/2026/   a.jpg b.jpg c.jpg
  supplier-notes/      kilns.md glazes.md
```

Identical for every run, verified by `find -type f | sort | xargs md5sum | md5sum`, which is
`47809391e908d576d7fae6d9657e7e31` at the time of writing and is re-checked after every arm.

## How each arm is run

`claude -p`, a fresh non-interactive session per run, four runs total. Writing tools are disabled
with `--disallowedTools "Write,Edit,NotebookEdit"` so no run can write into the scope even if it
tries to continue past the questions. **That flag is a deviation from an ordinary adoption and it is
identical across arms**, so it cannot produce a difference between them; it is recorded because an
unrecorded deviation is how a control stops being one.

Each run's raw stdout is committed verbatim to `.docs/runs/`.

## Repeats, and why

Two runs per arm. By [`handover.md`](../handover.md): repeat the run whose evidence is an absence,
not the one whose evidence is a quotation. **Length is not quoted from any document — it is produced
by wording — so nothing in the output self-verifies it and a single run of each arm settles
nothing.**

## The measures, fixed before the runs

Not impressions. Four numbers per run:

1. **Total words** in the assistant's output.
2. **Words in the question block** — from the first numbered question to the last, excluding the
   Step 2 look report and everything before it.
3. **Question count** — top-level numbered questions put to the person.
4. **Words per question** — measure 2 divided by measure 3.

Measure 2 is the primary one. Measure 1 includes the look report, whose length is a property of the
scope folder rather than of the framework, and the folder is held constant but the reporting of it
is not.

Reported as the mean of the two runs per arm, with both raw values shown, because a spread wider
than the between-arm difference is itself the finding.

## The predictions, with thresholds named in advance

**P1. If the framework caused the growth:** arm B's question-block word count exceeds arm A's by
**25% or more**, and **40% or more of the absolute difference** falls in the principles question.

**P2. If the framework did not cause it:** the two arms differ by **less than 10%** on the
question block.

**P3. Between 10% and 25%, or 25%+ without the principles concentration, is indeterminate**, and
is to be reported as indeterminate rather than argued into one of the other two. Naming this band
in advance is the point of writing this down: it is the outcome most easily talked into whichever
answer the session prefers afterwards.

**P4. Question count is roughly equal across arms**, within one question, because the topic list is
unchanged between the tags — five topics at both. If arm A produces materially fewer questions, the
framework's five topics are not what determined the question count in either arm, and that is a
finding about the topic list rather than about length.

**P5. Neither arm writes anything into the scope folder.** The checksum is unchanged after all four
runs.

## What each outcome means for the proposal in front of the owner

The proposal is to ship the wording of the questions as text, the way `blueprints/checks/` ships
prompts, and to keep generating everything the look produces.

**P1 confirmed** — the framework is a contributing cause. Shipping the wording fixes part of it and
the `project/README.md` principles block needs its own repair, because a shipped script does not
stop a tool from reading a blueprint README aloud.

**P2 confirmed** — the framework is not the cause and the reader is. This **strengthens** the
proposal rather than weakening it: if five topics produce a 937-word interview under one model and
a short one under another, then specifying the wording is the whole answer and not half of it. It
also means the `+23 lines` hypothesis was wrong, and the entry recording it in
[`backlog.md`](../backlog.md) says so.

**P3** — no redesign is justified on this evidence alone, and the next step is a third variable
rather than a script.

## What would make this run worthless

Stated in advance so it cannot be decided afterwards:

- Either arm writing into the scope, or the checksum changing between runs.
- A run that stops before asking any questions — for example by refusing to reach the framework
  path — which measures access rather than length. Such a run is discarded and re-run, and the
  discard is recorded here.
- The two runs within one arm differing by more than the difference between the arms. That does not
  invalidate the run; it is reported as the result, and the result is that this measurement cannot
  separate the two causes at this sample size.

---

# Results, scored 2026-08-29, after all four runs

Four runs, `claude -p`, `--model opus`, fresh session each, logs committed verbatim as
`.docs/runs/2026-08-29-interview-length-{a1,a2,b1,b2}.log`.

## Validity, checked before anything was interpreted

- **P5 holds.** Scope tree checksum `47809391e908d576d7fae6d9657e7e31` before and after all four
  runs. Nothing was written.
- **No run was discarded.** All four reached the framework, read the blueprint, and stopped at the
  questions.
- **The within-arm spread does not swamp the difference.** Arm A's two runs differ by 39 words on the
  question block, arm B's by 12; the between-arm difference is 114. The run is valid by the criterion
  set in advance.

## The four measures

| | total words | question block | questions | words / question |
| --- | --- | --- | --- | --- |
| A run 1 | 520 | 354 | 7 | 50.6 |
| A run 2 | 585 | 393 | 7 | 56.1 |
| **Arm A mean** | **552.5** | **373.5** | **7.0** | **53.4** |
| B run 1 | 676 | 494 | 7 | 70.6 |
| B run 2 | 658 | 482 | 7 | 68.9 |
| **Arm B mean** | **667.0** | **488.0** | **7.0** | **69.7** |

Question block: **+114.5 words, +30.7%.**

## Scoring

**P1 is not confirmed, and it fails on its second half.** Arm B exceeds arm A by 30.7%, which clears
the 25% threshold. But the principles question accounts for **24.0%** of the absolute difference
(32.0 words to 59.5, +27.5 of 114.5), against a threshold of 40%. The difference is spread rather
than concentrated: principles +27.5, where-it-lives +21.5, boundary +8, name +4, what-it-is +0.5,
and **components −25**, arm B's component question being shorter than arm A's.

**P2 is not confirmed.** 30.7% is far outside the 10% band.

**P3 is the outcome.** This is exactly the case P3 named — 25% or more without the principles
concentration — and it is reported as indeterminate because that is what was written down before the
run. **No redesign is justified by this measurement alone.** The `+23 lines` hypothesis is not
refuted and is not supported; what it predicted was concentration, and the difference is distributed
across five questions instead.

**P4 holds exactly.** Seven questions in every one of the four runs, both arms. The refused ArtGlina
interview also asked seven. Five topics have produced seven questions in three independent
conditions, which is a more stable number than anything else measured here.

## The finding that was not pre-registered, and it outweighs the one that was

**Arm B's question block is 488 words. The refused ArtGlina interview's was 633.** Same framework
version, same harness, same model, four days apart, different folder: **+145 words, +29.7%.**

So the variation *within* one version of the framework, across two folders, is **larger than the
difference between the two versions** that four releases separate.

**That comparison carries two confounds and both are named here rather than in a footnote.**

*The folder.* ArtGlina had a real symlink, a real business behind it and more for Step 2 to find than
a scratch tree of empty `.jpg` files.

*The instruction, and this one was not disclosed when finding 1 was first written.* Roughly 120 of
ArtGlina's 937 words are the "traces of an earlier arrangement" paragraphs, and they exist because
the reviewer's prompt told that session to stay blind and to report any trace it met without using
it. **That is neither the framework's prose nor the tool's initiative — it is a one-off instruction
present in that run and absent from every arm here.** Arm B's preamble on a neutral folder is 179
words against ArtGlina's 299, and this instruction accounts for most of a 120-word gap.

Correcting for it does not erase finding 1, because the 120 words sit in the preamble and finding 1
is measured on the question block, which is 633 against arm B's 488. It does mean the *total*-word
comparison between ArtGlina and arm B is not a comparison of two interviews, and it should not be
quoted as one. Recorded because an undisclosed instruction inside one arm is the same class of defect
as an undisclosed deviation, and this repository has spent two days on that class.

But the
question block is supposed to be folder-independent. That is the entire basis of the propose-what-can-
be-seen split: a question survives into the interview precisely because no amount of looking answers
it. A question block that moves 30% between two folders on one version is measuring something it was
designed not to measure.

## The second unregistered finding: both versions broke their own stated rules

Two of the four runs asked a question the procedure explicitly forbids, one in each arm.

**Arm A, run 1, question 7:** *"Do `.docs/` and `.docs/decisions/` exist or are they planned? Neither
is there now."* It answers its own question in its second clause. Step 4's list of things to avoid
names this one: *"A question about something you can read. Read it."*

**Arm B, run 2, question 7:** *"Posture per component. For each folder you name: does a platform or
framework update it wholesale?"* Step 4 says of the posture, in as many words, *"The posture is not
one of them"*, and tells the assistant to propose it from what it saw.

**Neither version enforces its own rule, and the rules broken are the two written most explicitly.**
This was not predicted, it appeared in half the runs, and it is a stronger argument for shipping the
wording than the length number is: a fixed script contains a question or it does not, and `grep`
settles it. A topic list plus four prohibitions did not settle it in either version.

## What this changes about the proposal

The proposal — ship the wording of the questions, keep generating everything the look produces —
**is not carried by the pre-registered measure**, which came out indeterminate and must be reported
that way.

It is carried by the two findings nobody registered: the question block varies 30% across folders on
one fixed version, and two of four runs asked a forbidden question. Both are variance in the thing the
proposal proposes to specify. Neither was arranged, and the second was found by reading the artefacts
rather than the numbers, which is this repository's own stated method.

**Recorded as a caution about this run's own status.** An experiment whose registered prediction came
out indeterminate, and which is then argued from its unregistered observations, is the exact shape
this repository warns about. The mitigation is that both unregistered findings are quotations from
committed logs rather than counts computed after the fact, and either can be checked by opening the
files. They are offered as observations needing their own test, not as a result this run established.
