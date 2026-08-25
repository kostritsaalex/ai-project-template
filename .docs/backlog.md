# Backlog

Working backlog for `ai-project-template`.

Last updated 2026-08-25, after the `0.6.0` validation run and the fixes it produced.

---

## Where we are

`0.6.0` is written across the working tree, validated, and ready to commit.

The WordPress 7 project was reset to bare folders and re-adopted from scratch on `0.6.0`, then the
Engine component was reset a second time and re-attached against the fixed blueprints.

| | structure-check | cold-start |
| --- | --- | --- |
| Project scope | 14/14 twice before the fixes, 14/14 after | 5/5 before, 5/5 after |
| WP Themes | 14/14, two tools | 5/5 |
| WordPress 7 Engine | 14/14 before the fixes, 14/14 after | 5/5 |

Five structure checks, five cold starts, no failures anywhere. Two behavioural tests beyond them:

**The cut-off.** With the scope folder moved out from under it, the Engine reported the failure before
answering anything, found the folder at its new path, refused to open it citing the stub's own "do
not proceed on guesses", and named what it could not know.

**The task instead of questions.** Asked in one line to set up a staging deployment, it opened the
parent across the mount boundary, quoted the exclusions line, refused to build, and said that moving
the boundary is an edit to `PROJECT.md` and the owner's decision.

Proven for the first time in this run: the `Assets` posture end to end, the override path, `AGENTS.md`
as the entry stub, and the accepted risk from `0005`.

**All eleven fixes were re-validated by the second attach.** Step 2 reported the platform-code item
in the ownership language; the interview stayed at two questions; the agent noticed the parent had no
session note, explained why it correctly had none before, and added one; it referred to the symlink
line by its new name, the path note; the rewritten WordPress fragment applied with no improvisation
and the core rule stayed out of `Local rules`.

---

## Now

Empty. The address question was settled in `0.7.0` by
[decision 0007](decisions/0007-a-component-with-no-address-says-so.md): a fourth form saying plainly
that no address exists, a check that requires one of the four, and the session note raised to a
precondition.

Not yet run against a live setup. Nothing in `0.7.0` has been through a structure check or a cold
start, because `WordPress 7` was already in the shape it prescribes. The first real test is either a
`structure-check` on that scope, which should now exercise the new check 11 wording against the
Engine's `Address: none` block, or the next project adopted from scratch.

---

## Release

**Where platform rules live.** They follow from a platform, not from a folder, which is the shape
`0005` used to move the preserve rules into the registry. There is no mechanism, so a fragment gets
copy-pasted into every WordPress component and nothing owns it. Candidate split: the shape of such a
rule is generic and can sit as a prompt in the `REPOSITORY.md` comment, while the WordPress instance
stays in the fragment. Supporting evidence from the run: the agent generalised the ownership axis to
third-party plugins by itself, writing a bullet the old fragment did not contain, and that bullet is
now the fragment's first line.

**A second razor, for rules.** The razor in `0004` cuts facts. Rules are invisible by construction,
so nothing constrains them. Candidate test: a rule earns a document only if an assistant would do
otherwise without it. Eight of the nine bullets in the Engine's `REPOSITORY.md` are ordinary
WordPress practice, which makes that folder the place to settle it: one task with the file and one
without, judged by the work.

**The third check.** Walk the registry from `PROJECT.md`, open each component's stubs, compare the
parent address and the component name against the block. Registry to disk only. Done by hand twice in
this run, which is what caught the session note and the address wording.

**A posture can go stale.** It is settled by whether platform code sits in the folder, and that can
change: a parent theme, a vendored dependency or a generated directory arrives and the word should
flip. Nothing notices.

**When a nested component earns its place.** Worth two stubs and a registry block only when it
carries something the folder would not otherwise have: a posture different from the one it inherits,
or an override of its own. `new-component.md` runs the interview either way. An override **adds** a
rule the project does not state; it does not contradict one.

**Component cold start question 3 loses its edge when an override exists.** The question exists so
the answer can only come from the parent. A component with its own rules can answer from the folder
and prove nothing. On the Engine the agent put the registry first and named both sources, so this is
a risk rather than an observed failure.

**Posture against exclusions, still uncaught, three instances.** A folder can carry a posture and be
full of material the project says it does not cover. The sharpest instance: `wp-themes`'s cold start
quoted "work here as the task requires" and "this project does not cover production sites and client
work" in the same answer, about the same folder, and saw no tension. Half of that was repaired on the
project side by naming what falls inside; the framework still has no mechanism to notice the shape.

**A check's evidence is not self-validating.** Three times in the run a passing report contained a
detail that does not exist: one tool listed `.agents`, `.codex` and `.git` in two different folders
that hold none of them, and a task run claimed `REPOSITORY.md` notes that nothing is deployed, which
it does not. None changed a verdict. Check 6 invites this by asking for a full listing when the fact
it needs is whether `PROJECT.md` is present.

---

## Recorded, not tasks

**Measured before and after, on the project boundary.** With the boundary written as "not decided
yet", two tools independently answered the boundary question by quoting a sentence about a component
not being *attached*. The boundary was written, one variable changed, and the re-run quoted it
correctly. An absent boundary is a decoy rather than a hole.

**The sentence naming what falls inside earned its place.** Added to WordPress 7 the same day, it was
picked up on the next cold start as the "inside" half of the boundary question, where the previous
answer had been thin.

**"Do not proceed on guesses" does real work.** The cut-off run is the evidence. One observation with
no control: no run was made without the line.

**The stub's stop is not too blunt.** Formerly a task. The cut-off run produced exactly the behaviour
the task was meant to produce, so it is a watch item now.

**Attachment status is visible and belongs in no document.** After the sentence about it was removed
as registry duplication, a cold start answered "listed but not attached" by looking at the disk. No
hole appeared, which is the razor working. Small tension worth watching: the cold start prompt says
to use only the files, and some questions are legitimately answered by looking.

**Runs vary on the same prompt.** The first attach of the Engine offered "use the WordPress platform
fragment" as an interview option; the second, on the same prompt and folder, did not. Recorded
because it means the absence of a behaviour in one run proves little.

**A false error is not a reason to retry a write.** An `ENOENT` came back from an edit that had in
fact applied. The agent read the file rather than trusting either the error or a retry, which is why
nothing was written twice. Verified independently: one session note, one path note, one Engine block.

**The naming question, closed but worth watching.** The pair stays, decided 2026-08-24. Hours later
the owner's reasoning for calling a theme folder `Assets` included "a repository is technically out
of place here because we host this on OneDrive", the storage-based reading the names invite. If a
second instance appears, reopen.

**The framework's own local path had the defect check 14 exists to catch.** `PROJECT.md` gave
`~/Repositories/ai-project-template` with nothing saying what holds it up. That form resolves on the
Windows side and not inside WSL, which is why every prompt this session used
`/mnt/c/Users/kostr/Repositories/...` instead. Fixed on 2026-08-25 by naming both forms. Check 14
would not have caught it: it is `n/a` when a document says nothing about its path, so silence passes.

**A platform fragment now carries a version tied to a blueprint version.**
`platforms/wordpress.md` is the first file in the framework with `For: Repository Blueprint 0.6.0`
in its header. If fragments multiply, somebody has to revisit them each release, and no mechanism
will remind them.

---

## Plan for the session after this one

`0.6.0` is merged to `main`, tagged and pushed. Two commits: the release, then "Fix eleven defects
found validating 0.6.0". Working tree clean. Nothing is half-done.

**Start here: run `0.7.0` against something.** A structure check on the `WordPress 7` scope is the
cheapest test: check 11 now has to accept `Address: none. No copy of this folder exists off this
machine.` and would have to reject a bare local path in that slot. Nothing in `0.7.0` has been run.

**Then: ArtGlina.** Still on the pre-`0.5.0` shape, never migrated. It is the
only project with a real `Assets` component holding material rather than code, so it is where that
posture gets its second test and where the assets override may get its first real case. Expect the
`Unsorted/` folder to be the interesting one.

**Kept for when the mood is right: the second razor.** The Engine's `REPOSITORY.md` now holds nine
bullets, eight of which any competent WordPress assistant follows unprompted. One task with the file
and one without, judged by the work, settles whether rules need a razor of their own.

**Do not start with:** a full framework re-read, or another validation run. `0.6.0` was validated
end to end today and nothing in it is suspected.
