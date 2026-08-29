# Pre-registration: does a sharper rule stop the posture flipping?

**Written 2026-08-29, before any arm is run. Committed before the first run.**
**`blueprints/` is held. Every arm runs against a scratch copy and touches nothing in the
repository.**

---

## Which of the two remedies this run tests, stated first

There are two remedies and they are **sequential, not alternatives to be weighed side by side.**

1. **Sharpen the rule and re-run.** If a clearer statement of the ownership axis removes the flip,
   the names are survivable and nothing else changes.
2. **Only if the flip survives, reopen the names.** Expensive in the way this framework hates: every
   registry block in every adopted project, and a word that appears in the shipped documents.

**This run tests remedy 1 and only remedy 1.** It is written down because a run that could be read
as evidence for either is a run that will be. **A pass here says nothing about whether the words are
good words** — it says the rule can carry them. A failure is what promotes the naming question, and
nothing short of a failure does.

## What happened, and why it is not merely an under-specified proposal

`2026-08-29-audit-gB1.log` and `-gB2.log`. Identical framework, identical folder, identical supplied
answers. `gB1` proposed `Repository. Things get changed here…`; `gB2` proposed `Assets. Live
material…`.

**`Assets` is right.** The axis is whether a platform or framework updates the folder wholesale, not
whether the folder holds code. The evidence is not only the rule but the framework's one adopted
registry: **`WP Themes`, a folder of theme source code, is `Assets`**, and `WordPress 7 Engine`, a
WordPress installation, is `Repository`.

**This is the trigger condition on a watch item open since 2026-08-24.** The naming question was
closed that day with *"If a second instance appears, reopen."* The first instance was the owner
reading `Repository` as a storage arrangement — his words, calling a theme folder `Assets` partly
because *"a repository is technically out of place here because we host this on OneDrive."*

**This is the second, and it came from the reader the words are written for.** A tool saw source code
in a git working copy and wrote `Repository`, where the rule says the answer is `Assets`. So the
evidence is no longer that one proposal is under-specified. It is that **the words mislead, from two
independent readers, one human and one not, pulled in the same direction by the word rather than the
rule.**

## What the observation is and is not

**The flip is one pair.** Two runs disagreeing on identical input is exactly what a repeat is for,
and it is enough to establish the defect. **It is not enough to say how often it happens, and it is
not reported as a frequency.** No rate is claimed here, and none should be quoted from this file.

## The sharpened rule

`new-project.md` currently says: *"A folder holding code that a platform or a framework updates takes
`Repository`. Anything else takes `Assets`."* The candidate replacement states the axis, names the
common trap, and gives the discriminating question:

> **The word is settled by one question: does this folder contain code that something other than a
> person replaces wholesale — a platform, a framework, a package manager, a generator?**
>
> If yes, `Repository`. If no, `Assets`.
>
> **A folder of your own source code is `Assets`, even when it is a git repository.** The word
> `Repository` is not about version control and not about where the folder is stored. It marks a
> folder whose contents an updater owns, so that hand edits to that code would be overwritten. The
> framework's own adopted registry has a folder of theme source code carrying `Assets` for exactly
> this reason.

## The arms

Three scratch scopes, one of each kind, so the rule is tested for correctness and not only for
stability.

| | Folder | Correct word | Why |
| --- | --- | --- | --- |
| **K-own** | Own source in a git working copy, no vendored or platform code | **`Assets`** | The flip case. Nothing replaces this code but a person |
| **K-platform** | A platform installation — `wp-admin/`, `wp-includes/`, `wp-content/themes/` | **`Repository`** | An updater replaces core wholesale |
| **K-material** | Photographs and documents, no code at all | **`Assets`** | The easy case, present so a rule that answers `Assets` to everything is visible |

| Arm | Framework | Runs |
| --- | --- | --- |
| **H** | `HEAD` at `0.11.0`, current wording | 2 per scope, 6 |
| **J** | `HEAD` + the sharpened rule in `new-project.md` and `procedure.md` | 2 per scope, 6 |

Twelve runs. Answers supplied so each reaches the Step 5 summary table, where the posture is
proposed. `claude -p`, `--model opus`, fresh session each, writing disabled. Arm H is the before, on
the same three scopes and the same day, so the comparison is not carried from another experiment.

## What a fixed rule has to do, registered before the run

Both, and the second matters more:

**S1. Stable.** The same word on the same folder across a pair, on all three scopes.

**S2. Correct.** The right word on a folder of each kind: `Assets` on K-own, `Repository` on
K-platform, `Assets` on K-material.

**A rule that is stable and wrong is worse than one that flips**, because nothing downstream would
notice. A pair that agrees on `Repository` for K-own is a **failure**, not a pass, and it is the
outcome most easily mistaken for success by reading the stability column alone.

## Predictions

**Q1.** Arm H flips or errs on **K-own** in at least one run — reproducing the finding. If arm H is
stable and correct across all six, the `gB1`/`gB2` pair was not reproducible and this whole item is
downgraded to a single unexplained divergence.

**Q2.** Arm J satisfies **S1 and S2 on all three scopes.** That is the pass condition and remedy 1
succeeds.

**Q3.** If arm J fails S1 on K-own — still flipping under a clearer rule — **remedy 2 is promoted**
and the naming question reopens with two instances behind it.

**Q4.** If arm J satisfies S1 but fails S2 anywhere, the rule is stable and wrong. **That is the
worst outcome and it is registered as a failure**, not as a partial pass.

**Q5.** No scope is written to; all three checksums unchanged.

## What this cannot establish

Whether `Repository` and `Assets` are the right words. Only whether the rule can be stated so they
are applied correctly. **A pass leaves the naming question exactly where 2026-08-24 left it, with two
instances recorded against it rather than one.**

And it cannot establish a rate. One pair flipped; twelve runs will say whether a sharper rule holds,
not how often the old one failed.

---

# Results, scored 2026-08-29

**Deviation from the registered design, recorded before the result.** The arms table above says two
runs per scope, twelve runs, with the three folder kinds as three separate scopes. **What was run is
one scope containing all three folders as declared components, three runs per arm, six runs and
eighteen posture judgements.**

The change was not deliberate and is not neutral. It is stronger in one way — each run judges all
three kinds, so a rule that answers the same word to everything is visible inside a single run rather
than across three — and weaker in another: three folders in one registry give a run the chance to
reason comparatively, which three isolated scopes would not. **A run that sees an obvious
`Repository` beside a doubtful folder has help that a real adoption of a single-component project
would not give it.** That cuts against arm J, which passed, so it does not manufacture the result;
it does mean arm J's pass is on the easier of the two designs, and the isolated-scope version is
still unrun.

Recorded rather than quietly re-labelled, because a design changed between registration and running
is the thing a pre-registration exists to make visible.

Six runs, logs `2026-08-29-posture-{h,j}{1,2,3}.log`. Each run proposed a posture for all three
folders, so eighteen posture judgements.

| | K-own `tidewatch` | K-platform `riverside-site` | K-material `harvest-archive` |
| --- | --- | --- | --- |
| **correct** | `Assets` | `Repository` | `Assets` |
| **H** (current) run 1 | **`Repository`** ✗ | `Repository` ✓ | `Assets` ✓ |
| **H** run 2 | **`Repository`** ✗ | `Repository` ✓ | `Assets` ✓ |
| **H** run 3 | **`Repository`** ✗ | `Repository` ✓ | `Assets` ✓ |
| **J** (sharpened) run 1 | `Assets` ✓ | `Repository` ✓ | `Assets` ✓ |
| **J** run 2 | `Assets` ✓ | `Repository` ✓ | `Assets` ✓ |
| **J** run 3 | `Assets` ✓ | `Repository` ✓ | `Assets` ✓ |

**Q2 passes. Arm J satisfies S1 and S2 on all three scopes.** Stable across every pair and correct on
a folder of each kind. **Remedy 1 succeeds and the naming question is not promoted.**

**Q3 not reached.** No flip survived the sharper rule, so renaming is not on the table. The naming
watch item stays open with two instances against it and no third.

**Q5 holds.** All three checksums unchanged.

## Q1 held, and it held harder than predicted — which changes what the defect is

Q1 predicted arm H would "flip or err on K-own in at least one run". **It erred in all three, and it
did not flip at all.** The current wording produced `Repository` for a folder of the project's own
source, consistently, with reasoning that never touched the axis: run 1 gave *"posture proposed from
your description of it as the tide tool"* — a description of what the folder is for, not of who
replaces its contents.

**So the flip understated the problem.** The `gB1`/`gB2` pair was read as instability: a proposal that
differs between runs. These three runs say the current rule is **stably wrong** on this folder kind,
and that `gB2`'s `Assets` was the framework getting it right by accident rather than the baseline it
sometimes departs from.

**That is exactly the shape registered as Q4 and named as the worst outcome** — *"a rule that is
stable and wrong is worse than one that flips, because nothing downstream would notice"* — and it
turns out to describe the shipped behaviour rather than a risk of the repair. Registering it in
advance is what makes it visible now; the stability column alone would have read as three consistent
answers.

**The correction is quotable.** Arm J run 1: *"Settled: your own tide-tool source. A folder of your
own source code is `Assets` even when it is a git repository, and this one is."* The sentence added
to the rule is the sentence the run gives back.

## What this does not establish

Whether `Repository` and `Assets` are the right words. It shows the rule can be stated so they are
applied correctly, and **it leaves the naming question where 2026-08-24 left it, with two instances
recorded against it rather than one.**

And it is not a rate. Three runs per arm on one folder of each kind says the sharpened rule holds
here; it does not say how often the old one failed, and no frequency is claimed.
