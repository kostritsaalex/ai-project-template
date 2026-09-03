# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
where practical.

## [0.18.0] - 2026-09-03

**A project scope's address is required, and where it cannot be derived the interview asks for it.**
See [0023](.docs/decisions/0023-a-project-scope-address-is-required.md).

### Fixed

- **`blueprints/setup/interview.md` stops writing `0007`'s fourth form into a project scope.** The
  third sub-bullet under "The address" instructed it whenever neither derivation rule fired.
  [0007](.docs/decisions/0007-a-component-with-no-address-says-so.md) does not say that: its title is
  *"A component with no address says so"*, its Decision binds the form to `structure-check` **11**,
  the registry row, and its Consequences state the asymmetry — *"**A component with no address is
  still a component.** The gap runs one way."*
- **What it broke was the component, not the scope.** `procedure.md` Step 7 has a component's stubs
  carry *"the parent's address, copied from the parent's own text rather than retyped"* and ends
  *"Nothing else in the parent changes when a component is attached"*, while `structure-check` row 8
  admits three forms for that value and `blueprints/component/README.md`'s
  `<CANONICAL_PROJECT_SCOPE_ADDRESS>` defines the same three. A scope adopted with the fourth form
  could give its components no stub address that passes row 8, and the attach was forbidden from
  repairing the parent.
- **The branch that replaces it already existed and was unreachable.** `interview.md` has read *"If
  neither yields a value, ask for it"* since `0.12.0`, and the sub-bullet always yielded a value.
  That line is unchanged; what changed is that a run can now reach it.
- **The asking branch carries its own explanation**, because `interview.md` and `procedure.md` Step 4
  both forbid a session from adding one — *"Do not introduce them, gloss them, add clarifications, or
  add questions of your own"*. The text names what qualifies, that `git init` alone does not, per
  `0007`'s *"Local version control and reachability are separate questions"*, and that setup stops.

### Removed

- **The fourth form as an option for a project scope**, which is the rule this release exists to
  remove. It remains the rule for a component block, unchanged, in `structure-check` 11 and
  `architecture.md`.
- **Attach defect 6 in `.docs/backlog.md`, deleted.** It held that `structure-check` row 8 was too
  narrow at three forms. The repair was upstream of it and row 8 was right. **Its number is held
  rather than reused**, because [0022](.docs/decisions/0022-the-attach-commits-what-it-wrote.md), the
  `0.17.0` entry above and two predictions all cite these defects by number, and renumbering would
  make four documents false.
- **And what it did not remove, said plainly.** `interview.md` grows by twenty-two lines, and this
  release is a net addition to that file. The growth is in setup text, which is not shipped into an
  adopted project, so **the shipped-line metric does not see it** — re-measured at 40 and 22,
  unchanged. That is a reason for care rather than comfort: nothing measures the setup path.

### Not touched, deliberately

- **`structure-check` row 8, row 11, and `component/README.md`'s placeholder.** Three forms, four
  forms and three forms are each correct; `.docs/audits/structure-check-rows.md` settled row 8 on
  [0001](.docs/decisions/0001-project-scope-need-not-be-a-repository.md) — *"a scope may not be
  addressless and there is no fourth form for a parent. Three is right"*. **No check row is added and
  none is widened.**
- **The four questions.** No fifth, no merge, no rewording, so
  [0014](.docs/decisions/0014-the-razor-runs-over-the-questions-one-at-a-time.md)'s measured *"four
  questions, never five"* and its fidelity result both stand. `0014` does state the rule this release
  removes, at its Decision section; that clause is displaced by `0023`, its file is not edited, and
  the record says so rather than leaving two documents to disagree.
- **`procedure.md`.** It defines no gate for an answer that stops adoption — Step 5 admits *unknown*
  as a provenance — and Step 7 has eight unclosed defects. The stop is written into `interview.md`,
  bounded to the one value, and the gap is stated in `0023` rather than filled.

### Measured

- **Six runs, five pre-registered before the edit existed** in
  [`.docs/predictions/the-scope-address-is-required.md`](.docs/predictions/the-scope-address-is-required.md),
  all logged under [`.docs/runs/`](.docs/runs/README.md). Arm A1 twice, control C1 once, control C2
  twice, plus one before-run added mid-experiment and labelled as added.
- **A1 passes all four criteria in both runs.** The address is asked for; **the fourth form's word
  appears as a value in neither log**; the message names what qualifies, that `git init` alone does
  not, and that setup stops; no local path reaches the address slot.
- **The control carried the release.** C2 — a folder in a store, the path this change must not touch
  — behaves identically before and after: same address proposed, nothing asked, four questions in
  every run. But the same scope run against `0.17.0` **offered the fourth form on a project scope
  unprompted**, on the arm this change was not aimed at. The defect is reproduced in the wild and
  absent from both `0.18.0` runs.
- **Disclosed against it:** one of three registered words reached the person in one of three
  C2-family runs, in a clause naming which derivation rule fired; A1's two runs diverge on the stop
  because the shared run prompt told every session to reach the Step 5 table, and both named the
  conflict rather than resolving it silently; and **C1 never reached its own question**, the session
  having rejected the simulated store and derived from the git remote alone.

### Also in this release, and none of it caused it

Per `release.md` step 0, a change under `.docs/` never causes a release. These ride with one that is
happening anyway, and are listed because step 7's V1 requires every file in the diff to be accounted
for.

- **`.docs/architecture.md`**: the line *"A location on one person's machine is not an address in any
  of these senses. Write the fourth form instead"* gains the qualification the paragraph four lines
  below it already carried, that the fourth form is what a component carries.
- **`.docs/backlog.md`**: attach defect 6 deleted; the new item above filed under `Now` and not
  scheduled; and four records added, of which two came out of this release's own runs — that
  `interview.md`'s two derivation rules test the shape of a path rather than whether the store
  resolves, **raised by the `0.17.0` before-run too, so it predates this change**, and that which rule
  wins when both fire is unsettled and C1 could not reach the question.
- **`.docs/runs/`**: six logs and their index rows, checksums and narrative.
- **The six blueprint `README.md` files** carry the `Framework Version` bump this release is, per
  `release.md` step 2. Only `blueprints/setup/` also moves its `Blueprint Version`, because
  `interview.md` is the one blueprint file that changed.

## [0.17.0] - 2026-08-30

**The attach commits what it wrote.** See
[0022](.docs/decisions/0022-the-attach-commits-what-it-wrote.md).

### Fixed

- **`blueprints/setup/procedure.md` Step 8 now asks for a commit**, of the files the session wrote and
  only those, in each folder it wrote into that is under version control. Nothing in the procedure had
  ever asked for one, and two live attaches on 2026-08-30 did not make one: on ArtGlina the stubs were
  committed by hand afterwards, outside the procedure, and on NorsePath `git status --short` in the
  component still printed `?? AGENTS.md` and `?? CLAUDE.md` after the attach, both checks and a
  behaviour test.
- **What it repairs is invisible to both shipped checks.** `structure-check` and `registry-check` read
  the working tree, where an untracked file reads exactly like a committed one. A clone of the
  component arrives with no parent pointer and a sweep of untracked files removes both stubs, with no
  row failing in either case.
- **A folder that is not under version control does nothing here**, and the instruction names no tool
  and no command. [0001](.docs/decisions/0001-project-scope-need-not-be-a-repository.md) admits a
  project scope that is not a repository, and
  [0007](.docs/decisions/0007-a-component-with-no-address-says-so.md) settles that local version
  control and reachability are separate questions.

### Where it went, and where it did not

- **Step 8, not Step 7**, decided on the four adoption READMEs. `component/README.md:114`,
  `project/README.md:152`, `assets/README.md:91` and `repository/README.md:104` all say *"Before
  committing, search for `<!--` and for `<` followed by a capital letter"*, and that search is Step 8's
  first instruction. A commit in Step 7 would run on the wrong side of it. Step 7 is also skipped for a
  project scope, which writes files into the same kind of folder and leaves them untracked the same
  way, and its *"attached when both halves are written"* is a definition this release does not reopen.
- **The session commits rather than reporting.** Step 8 already requires it to *"say which files you
  wrote or changed"*; both runs produced that report and the stubs stayed untracked in both, so
  reporting is the weaker form of an instruction that has already failed twice.

### Unchanged, and deliberately so

- **Step 7.** Not touched, including its definition of attachment and its registry example.
- **The eight other attach defects**, among them the competing four-step adoption procedure in
  `component/README.md` and the absence of any run log for an attach at all. All nine are recorded in
  `.docs/backlog.md`; this release repairs one.
- **Whether a component is a folder or a repository.** Committed stubs travel with every clone, which
  is the multiplication that question is about. It stays open, and this is the line that changes if it
  is ever settled the other way.

### Removed

- **Nothing, and this is the fourth release in a row that can say only that.** Principle 7 asks a
  release that adds to name what it removed in exchange. `procedure.md` goes from **128 to 132
  non-blank lines**. Nothing in the step became redundant, and taking something out would have meant
  repairing a second defect, which this release is not doing. The debt is four releases old and the
  queued subtraction pass over `blueprints/` inherits four more lines than it was promised.
- **The shipped-line metric is unmoved at 40 and 22**, re-measured rather than carried forward. This
  release touches the setup procedure, which the metric does not cover — the same gap the previous
  release stated as a number.

### On the evidence

**Two live instances and no run.** The defect has two instances a week apart in ecosystems that share
only this framework, and neither check can see either. The repair itself **ships unrun**: every arm
needs a fresh session against a scope, and the session that wrote the instruction cannot be one. That
is defect 2 of the nine — *"The shipped procedure was unrun text"* — repeated against principle 6, and
it is named here rather than left to be noticed. Pre-registered before the edit in
[`attach-commits-what-it-wrote.md`](.docs/predictions/attach-commits-what-it-wrote.md): three arms
including a negative half, and three controls not derived from the hypothesis — a project scope in a
folder with no version control, which must produce no action and no confusion; a repository holding
unrelated modified files, which tests *"and only those"*; and a session that cannot run commands,
which must not report a commit it did not make.

### Also in the range since `v0.16.0`, under `.docs/`, none of it causing this release

Step 0 says a change under `.docs/` never causes a release; these are named because one is happening
anyway, so that every file in the release's own diff is accounted for.

- **Three repairs to `release.md` step 7**, with their prediction files —
  [0019](.docs/decisions/0019-a-check-compares-fields-not-prose.md),
  [0020](.docs/decisions/0020-a-check-that-cannot-fail-is-not-a-check.md),
  [0021](.docs/decisions/0021-a-row-states-what-it-examined.md) — and the rule added to
  `.docs/handover.md` that every change carries at least one control not derived from its hypothesis,
  which is the rule this release's controls were written under.
- **Four run logs and the `runs/` index**, from the live adoption: a structure check, a registry
  check, the first cold start against a real adopted project, and one task run.
- **`.docs/backlog.md`**: the nine attach defects found by the two live attaches, an item on evidence
  that does not exhibit the criterion its row applies, and defect 8 now marked repaired here.

## [0.16.0] - 2026-08-30

**The delivery of the check's own text is not part of its read set.** See
[0018](.docs/decisions/0018-the-instrument-is-not-part-of-the-sample.md).

### Fixed

- **The read set governs what a check consults about the project under check.** Material that exists
  only because of how the check's own text reached the session is outside it: `registry-check.md`
  itself when the session was given its path instead of its text, and a harness's attachment or spool
  storage holding the pasted prompt.
- **The exemption covers the check's own instructions and nothing else.** A file of the project under
  check is judged by the read set exactly as before, wherever it sits, and so is every other file of
  this framework — the other checks, their README, the blueprints. Reading one of those is still a
  third-class read and still fails row 7.
- **Exempt is not invisible.** The exemption adds a **fourth class** to the three row 7 names, and
  requires the read to be listed and the file named. A rule that let the session drop it from the list
  would have attacked the one thing row 7 cannot see, which is a folder opened and left off.
- **Loading the check by giving its path is now a supported way of running it.** That was the
  operator's original mistake, and it was never a mistake about the project.

### Where this was written, and where it was not

- **The read set is declared per check, three times, and audited once**, established by reading the
  files rather than assumed. [0009](.docs/decisions/0009-a-check-declares-its-read-set-in-advance.md)
  states the rule but is a decision record no running session reads; `structure-check` declares one
  folder's root and **has no row that audits it**; `registry-check` declares its set and **row 7
  audits it**; `cold-start-check` declares none, because following the chain outward is what it
  measures.
- **The change went into `registry-check.md` alone.** In `structure-check.md` the same words would be
  a clause that **cannot execute** — its prohibition is real and breaks identically on a path load,
  but nothing there reports what was opened, so no output would differ. Available the day
  `structure-check` grows an audit row. `cold-start-check`'s analogous hazard is already covered under
  its own name, as a **hint**.

### Unchanged, and deliberately so

- **Row 7.** Not touched. **Weakening it was considered and rejected**, in three forms: permitting
  anything opened before the prompt was read, which would also cover a session that browsed the
  project first; dropping the *"without exception"* listing requirement, which the row's own text
  names as the failure it exists to catch; and making it advisory, which audits nothing. It has one
  confirmed true positive on its record, from `0.15.0`. **Adjusting an instrument immediately after
  its first correct reading is a failure already in this project's log.** The fourth class is added in
  the read-set declaration, and the row inherits it.
- **[0009](.docs/decisions/0009-a-check-declares-its-read-set-in-advance.md).** It says what kind of
  thing a read-set declaration is, and that is unchanged: the set is still computable from documents
  before any file is opened. `0018` says what the set is a set *of*.
- **The first line of `registry-check.md`, `checks/README.md`'s framing, and `release.md` V3.** Three
  separate changes, still in the backlog. `checks/README.md` moves here only in its two version lines.
- **No row added, none removed.**

### Removed

- **Nothing, and this is the third release in a row that can say only that.** Principle 7 asks a
  release that adds to name what it removed in exchange. The prompt block goes from **87 to 96
  non-blank lines**. Nothing in it became redundant: the read-set declaration bounds what is
  consulted, and the new paragraphs bound what counts as consulting. Named here rather than left to be
  noticed, and the debt is now three releases old.
- **The shipped-line metric is unmoved at 40 and 22**, re-measured rather than carried forward. This
  release touches a check prompt, which the metric does not cover — which is the debt above, stated as
  a number.

### On the evidence

**Two instances in two ecosystems, which is what made this a property of the check rather than an
operator's mistake.** Instance 1 is the operator's path-load run against ArtGlina, recorded under
`0.14.0` as deferred. Instance 2 is the operator's **Codex** run of the same shipped text, in an
ecosystem with **no knowledge of this framework**: rows 1 through 6 produced **identical verdicts**,
including *declared, not attached* and both cascade branches, and **row 7 failed** naming
`/home/kostritsaalex/.codex/attachments/<uuid>`, that harness's own spool for the pasted prompt, whose
contents the operator confirmed. Rows 1 to 6 agreeing across ecosystems is a second finding: the
check's text reads the same way outside the framework that produced it.

**Three runs against the edited text, one fresh `claude -p` session each, one pre-registration written
and committed before the edit existed**, in
[`.docs/predictions/registry-check-instrument-not-sample.md`](.docs/predictions/registry-check-instrument-not-sample.md).
The parent of both component folders was granted in every arm, and the whole framework repository in
the path-load arm, so the failing reads remained available throughout.

- **Arm 1, real ArtGlina, text pasted.** Rows 1 to 6 identical to `0.15.0`; **row 7 pass, three
  folders, no fourth**; `Failed rows: 0`. The change moves nothing when the delivery leaves no trace.
- **Arm 2, real ArtGlina, the check's path given and no text — the arm that decides.** Rows 1 to 6
  identical to arm 1; **row 7 pass, its evidence naming
  `…/blueprints/checks/registry-check.md` in full and classifying it as *"the check's own
  instructions, given as a path rather than text; fourth class, exempt, a pass"***; `Failed rows: 0`.
  **Not a silent pass**: the file is named, not dropped. Granted the whole framework repository, the
  session opened one file in it.
- **Arm 3, negative control, disclosed plant.** **Row 7 fail**, naming the planted folder in the third
  class; `Failed rows: 1`. The session recorded that it opened the folder *because the prompt's own
  closing line said to* — and still refused to exempt it, because it was project material and not the
  check's instructions. **Row 7 is not blind.**

ArtGlina was read-only throughout; its three root files were checksummed before and verified
byte-identical after, matching the `0.15.0` values. The scratch tree was deleted.

### Clauses that shipped without executing

- **The spool half of the exemption.** Three arms executed the **path** half. **Claude Code does not
  spool a pasted prompt to disk**, so the attachment-and-spool half cannot be run in this ecosystem at
  all — which is exactly why the second instance had to come from another one. **The operator's Codex
  re-run is the only thing that can execute it.** Until then, half of this change is argued rather
  than measured.
- **Row 5's probe clause, for the third release running.** No arm had an override file or a stub
  naming one, so row 5 was `n/a` in all three. Shipped through `0.15.0` and `0.16.0` unexecuted.

### What the operator's re-runs should produce

- **Claude Code, pasted:** arm 1. Row 7 **pass**, three folders, no fourth. `Failed rows: 0`. The
  fourth class may be mentioned and reported empty; that is not a failure, and it is what arm 1 did
  here against a prediction that expected silence.
- **Claude Code, path given:** arm 2. Row 7 **pass**, naming `registry-check.md`. `Failed rows: 0`.
- **Codex, pasted: row 7 should now pass.** Rows 1 to 6 unchanged from its earlier run. Row 7 should
  **list `/home/kostritsaalex/.codex/attachments/<uuid>` and classify it as the check's own
  instructions** — the fourth class, a pass — rather than as *"neither"*. `Failed rows: 0`. If it
  drops the folder from the list instead, the exemption reads as permission to stop reporting. If it
  still fails, the wording does not reach what that harness does, and the finding is the wording's.

## [0.15.0] - 2026-08-30

**One declared path, one command, in the rows of `registry-check` that probe the filesystem.** See
[0017](.docs/decisions/0017-a-probe-covers-one-declared-path.md).

### Fixed

- **A probe covers one declared path and no other.** The prompt's governing text now says it once:
  no command names two declared paths, no glob, brace expansion or wildcard whose resolution can
  reach outside the path it was pointed at, and **the parent directory of a declared path is not
  itself a declared path**.
- **The rows that probe a path say so at the moment they probe it.** Rows 1, 2, 5 and 6 each gained
  one clause. **Which rows those are was read off the prompt rather than assumed**: row 3 quotes
  stubs already in the read set, row 4 resolves and compares, row 7 opens nothing of its own. **The
  row that actually broke was row 1**, whose evidence in the `0.14.0` logs is *"listed it, the folder
  is there"*, once per component and once per command.

### Unchanged, and deliberately so

- **Row 7.** It was not defective. On 2026-08-30 it produced **its first true positive in its life**:
  the operator's fresh interactive run against ArtGlina failed it, naming
  `/home/kostritsaalex/Projects` — the common parent of both component paths, read because one
  command tested both. **Permitting parents of declared paths was rejected outright.** Adjusting an
  instrument immediately after its first correct reading is a failure already recorded in this
  project's own log. The procedure it measured changed; the instrument did not.
- **The read-set definition, the first line of `registry-check.md`, and `checks/README.md`'s framing.**
  Two further changes, each with its own run, both still in the backlog.
- **No row added, none removed.** Rows 3 and 4 are untouched.

### Removed

- **Nothing, and this is the second release in a row that can say only that.** Principle 7 asks a
  release that adds to name what it removed in exchange. This one adds five lines of governing text
  and four clauses; the prompt block goes from **80 to 87 non-blank lines**, the file from 170 to
  192. Nothing in it became redundant: row 6's *"Do not list the folder"* bounds the shape of
  evidence, not the reach of a command, and the two rules are independent. Named here rather than
  left to be noticed, and carried to the backlog as a debt, because check prompts are exactly the
  documents no metric protects.

### On the evidence

**Three runs against the edited text, one fresh `claude -p` session each, one pre-registration
written before the edit existed**, in
[`predictions/registry-check-one-path-one-command.md`](.docs/predictions/registry-check-one-path-one-command.md).
Every prediction held.

**The failure mode was available in all three.** Each session was granted read access to the parent
of the component folders, so the wide command that broke row 7 remained possible; the prompt is the
only thing that prevented it.

- **The real ArtGlina scope, unmodified.** Rows 1 to 6 identical to the operator's failing run, both
  components. **Row 7 pass**, three folders listed, no fourth. `Failed rows: 0`. Two separate
  listings in the evidence where the failing run had one. The scope's three root files are
  **byte-identical** before and after.
- **Negative control, disclosed plant.** One deliberate extra listing of a folder no registry line
  names. **Row 7 still fails and still names it.** The change did not make the row blind, which is
  the property it could have destroyed.
- **Negative control, a declared path two levels below an undeclared folder.** Reached and confirmed
  by **one command on the full path**; neither intermediate appears anywhere in the table. The
  plausible wrong repair — walk down confirming each level — would have failed row 7 twice.

Logs in [`runs/`](.docs/runs/), indexed with checksums. Scratch copies deleted.

**The shipped metric was re-measured and is unchanged at 40 and 22.** Nothing in
`blueprints/project/` or `blueprints/component/` was touched.

### The shape this is the third instance of

**A rule existed, was correct, and was written somewhere other than where it had to be obeyed.** The
prompt says to paste its text, and that instruction sits inside the file a session must open to read
it. The prompt said what a non-attached component is, and had no state for the one `0.13.0` made
normal. The prompt declares a read set, and the rows that act on it carried nothing at the moment of
acting. Row 7 caught the first and the third; six failed rows caught the second.

### Known, deferred, not fixed here

- **The check's own file is still outside its declared read set.** Loading it by path breaks the rule
  before the rule can be read. Its own change, its own run, and it is next.
- **The stale first line** of `registry-check.md` and of `checks/README.md`, deferred at `0.14.0` and
  deferred again for the same reason: it is a second variable.
- **Row 5's clause has never been executed.** No arm had an override file or a stub naming one, so
  row 5 was `n/a` in all three runs. Named rather than claimed.

## [0.14.0] - 2026-08-30

**Declared, not attached is a second non-attached outcome in `registry-check`.** See
[0016](.docs/decisions/0016-declared-is-a-second-non-attached-outcome.md).

### Fixed

- **`registry-check` no longer fails a correct newly adopted scope.** A component whose folder exists
  and whose two stubs are both absent is **declared, not attached**. Row 2 is `n/a` and says so, and
  rows 3 to 5 — the rows that read a stub — are `n/a` naming that outcome. Row 6 tests one path and
  reads no stub, so it still runs and still returns a verdict.
- **Exactly one stub present still fails**, and the row now says which one is missing. A component
  half attached is a defect under any reading.

### Unchanged, and deliberately so

- **Row 1's cascade.** *"Unless this row confirmed the folder exists, rows 2 to 6 ... are n/a"* is
  correct for the condition it covers and is not touched. The two outcomes now cascade differently,
  over different rows, each `n/a` naming its own reason. A deleted folder reporting *"declared, not
  attached"* would report a broken registry as a normal early state, and that is what negative
  control 2 was built to catch.
- **Row 7, the other two checks, and the structure of the file.** One condition changed, no row
  added.

### Removed

- **Nothing.** Principle 7 asks a release that adds to name what it removed in exchange, and this one
  removes nothing: it is six lines of prompt and three paragraphs of commentary, added to repair a
  check that fails correct projects. Named here rather than left to be noticed.

### On the evidence

**Five runs against the shipped text, across three arms**, one pre-registration written before the
edit existed, in
[`predictions/registry-check-declared-not-attached.md`](.docs/predictions/registry-check-declared-not-attached.md).
Every prediction held. Two arms were run twice — once because a sandboxed session could not produce
row 2's listing, once because a missing folder failed row 1 on blocked access rather than an observed
absence. Both pairs agree on every verdict; the second of each pair is the one whose evidence
demonstrates what the arm was for. All five logs are in
[`runs/`](.docs/runs/), indexed with checksums.

**The state this repairs did not exist in the corpus the check was built against.** `registry-check`
was written and validated nine times against `WordPress 7`, the framework's own subject, where every
declared component was already attached. **`0.13.0`'s interview made declared-and-unattached the
normal first state of a new project**, because naming a component does not attach it. ArtGlina was
the first adoption after that release and produced **seven failed rows on a scope `structure-check`
passed 14 of 14** — six of them from this cause, and the seventh from the read-set question deferred
below.

**A cascade condition is only as good as the cases in the corpus that could separate it from its
symptoms.** This one was written correctly and was still keyed on a symptom, because every run
happened on the one scope where the symptom and the condition coincide.

### Known, deferred, not fixed here

- **The first line of `registry-check.md` still says to run it *"after the components it declares
  have been attached"***, and `checks/README.md` says the same. That framing is now narrower than
  what the check does. Deferred knowingly: this release changes one condition, the file is not being
  rewritten otherwise, and a wording pass over two files is a second variable. Recorded in the
  backlog.
- **Row 7's failure on the ArtGlina run.** The operator loaded the check by path, so the session had
  to open `blueprints/checks/registry-check.md` to learn the procedure, and that file is outside the
  declared read set. The instruction to paste the text sits inside the file, reachable only after the
  rule has been broken. Its own change, its own run.

## [0.13.0] - 2026-08-30

**The boundary becomes agent boundaries.** See
[0015](.docs/decisions/0015-the-boundary-becomes-agent-boundaries.md), which supersedes part of
[0011](.docs/decisions/0011-the-boundary-is-a-closed-inclusion.md).

### Changed

- **`PROJECT.md` carries `Agent boundaries` instead of a closed inclusion** — anything an agent should
  never do here, each written as a prohibition in the owner's words. `<SCOPE_COVERS>` becomes
  `<AGENT_BOUNDARIES>`; the old name no longer described what goes there.
- **The interview asks it in his words**, with three examples from different categories so a reader
  sees the kind rather than a line to copy. Question 4 is his too: *"Which additional folders and
  repositories belong to this project? Main project directory doesn't count."*
- **Where nothing is forbidden, the section says so in visible text and is never deleted.** This is
  the branch [0010](.docs/decisions/0010-the-path-note-stays-optional.md) is about: silence reads as
  correct to every check.
- **The cold start check's rows are rewritten in both prompts.** The project prompt's question 2 and
  the component prompt's question 4 are the same question, and only one of them had ever been named
  in a change list.

### Fixed

- **A row wrong since `0.10.0`.** `cold-start-check.md`'s project-scope reading row still read *"one
  item from each list"*, the two-list wording from before the closed inclusion. Found on 2026-08-29,
  deferred knowingly because checks were out of scope, and repaired here rather than shipped wrong a
  third time — the file was being rewritten regardless, so this was the same edit surface rather than
  a passenger.

### Removed

- `0.10.1`'s scoring section for the derived half of the boundary question. **A prohibition list
  supports no derivation**, so that half is gone and the row now tests reading rather than reasoning.
  Declared in the check as a reduction in what it can see.

**The question block falls to 146 words**, from 175 at `0.12.0` and 235 in the draft this replaces.
**The first change to the interview in this sequence that cuts rather than adds**, and both shortened
questions are the owner's own wording. The shipped metric is unchanged at **40 and 22**.

### On the evidence

Eight runs, one pre-registration, every prediction held.

**The finding that decides this, and it was not known when `0011` was written.** The one measurement
justifying a boundary at all — an assistant refusing to build a staging deployment — **was taken on a
prohibition-shaped line**, and `WordPress 7` still carries it. **`0011` inverted the form and
inherited the evidence without re-taking it**, for three releases. So this is not a preference traded
against measured behaviour: it returns the line to the shape its evidence was gathered on.

**The empty case was the prediction that mattered and it held twice.** Both cold-start runs against a
document recording no prohibitions quoted the absence sentence *and* committed to asking, unprompted,
rather than treating the absence as permission.

**The cost, stated rather than traded away.** A prohibition list fails open: work nobody thought to
forbid is permitted. The required absence sentence answers that for an empty list and **a populated
list carries no such sentence**, so a project with three prohibitions and a fourth nobody thought of
behaves as `0011` warned. Accepted because the alternative was an invented closure, which fails in
both directions at once.

**The fixture is hand-written, not adopted**, registered as a limit before the runs. This measures the
check against a document. **`0.13.0` is provisional as the four before it are, and all five wait on
the owner's approval of the question set.**

### Also in this release, from `.docs/` and causing no version of their own

**A measured mitigation stopped working with nothing changed to make it stop.** `new-project.md`
records *"say what a component is before asking for the first one"* as measured; the sentence was in
question 4 and the owner named the project folder as a component anyway. `0008` says a rule's
justification can expire because it is a claim about a reader — **nobody had said the same about a
mitigation**, and the only instrument that caught it was the person it was written for doing the
thing it forbids.

## [0.12.0] - 2026-08-30

**Seven questions become four.** `0.11.0` shipped the interview as text and never ran the razor over
its contents. See [0014](.docs/decisions/0014-the-razor-runs-over-the-questions-one-at-a-time.md).

### Changed

- **The interview is four questions**: what the project is, its boundary, its principles, which
  folders are components. Each was judged against `0004` on its own — *could an assistant that read
  the folder have proposed this?* — which is the audit `0013` named as its basis and never performed.
- **The name and the address become proposals**, and **every proposal names its source in the
  assistant note.** The address rule is narrow because a wrong one is worse than a question: a
  synced-store root gives `OneDrive, <path within the store>`; a git remote gives that remote
  normalised to a URL with its scheme, and if it cannot be normalised to one of `0007`'s four forms
  the assistant **asks**; with neither, `0007`'s `none` form with the reason.
- **The boundary is answered in kinds of work, and the example now says so.** `restoration,
  photography and selling online`, not a list of folders.

### Removed

- **`<DOCUMENT_OWNER>`**, from the blueprint header, the placeholder table and the interview. It
  names a person to ask when a document is ambiguous, which is a convenience for a human reader; an
  assistant meeting an ambiguous `PROJECT.md` reports it and stops either way. **This is a reasoned
  cut recorded as reasoned rather than measured** — the only change here with no run behind it, and
  the first to revisit if a project needs the line.
- Three questions, and the apparatus that asked them.

### Fixed

- **`0011`'s worked example and the blueprint's placeholder table both taught the opposite of their
  own rule.** `0.10.0` inverted the boundary and changed the example from `hosting and deployment,
  mobile applications, accounting` — kinds of work — to `the main folder and the northwind-storefront
  repository` — places. It recorded the rule change and not the example change, and **every adoption
  for four releases followed the example**, answering the boundary with a folder list that duplicates
  the registry. Found by the owner as a feeling that two questions overlapped, and established in git.
- `release.md` V2, which contradicted step 1 in the same file: step 2 bumps `Framework Version` in
  every blueprint `README.md`, so every blueprint always appeared in V1's list and V2 read literally
  demanded that every `Blueprint Version` move. It now reads "changed in some file other than its
  `README.md`'s version lines", which is how every release had silently read it.

### Added

- `release.md` step 6 gains one exception: **a pre-registration committed between the work and the
  release is not squashed into it.**
- `handover.md`: **judging by the artefact means judging whether the artefact works.** A diff in the
  right files is not work.

**The shipped-line metric moves for the first time since `0.7.0`: 40 non-blank lines for a project
scope, 33 of them `PROJECT.md`, and 22 for a component.**

### On the evidence

Nineteen runs across three pre-registrations.

**Fidelity: zero added prose in every script run**, similarity 1.000 — eleven runs of the mechanism
now, four subjects, five scopes. **Four questions, never five**, on three scopes. **The address on all
three branches, twice each**, both git runs normalising the SSH remote and citing `0007` unprompted;
the registered falsifier did not fire, having fired once on this repository before shipping.

**The placeholder map was re-derived rather than assumed**, because it is what found the last gap:
eleven placeholders, four from questions, five from proposals, two read, all sourced in both runs.

**What did not carry this, named rather than left to disappear.** The claim that the question block
varies with the folder was this session's own best argument after an earlier experiment came out
indeterminate, and **a control arm refuted it at −3.5%.** The name proposal is justified by the razor
and not by a run, since nothing in a scratch run can observe an owner correcting a name.

**Fidelity, not sufficiency.** No run answered these questions and no `PROJECT.md` was produced.
**`0.12.0` is provisional, as `0.10.0` through `0.11.0` are, and all five wait on the owner's approval
of this question set rather than on scheduling** — he has cancelled every adoption until he has read
it and accepted it.

### Also in this release, from `.docs/` and causing no version of their own

A third shape of stale fact: **an example contradicting the rule it illustrates.** `0004` cuts facts
and `0008` cuts rules; an example is neither, and it can contradict its rule while both read correctly
alone. Its instrument is a reader, and nothing is being built for it.

The posture axis was reversed by the owner the same day and **is deliberately not in this release.** A
sharpened posture rule was measured and worked — the old wording proposed `Repository` for a folder of
own source in three of three runs, stably wrong — and was pulled, because it says the opposite of the
new axis and shipping then reversing it is churn. The axis change waits on whether the core rule earns
its place, which **two experiments failed to establish**, in opposite directions: one with an invalid
tree, one with a task that left no shortcut to take.

## [0.11.0] - 2026-08-29

**The interview ships as text.** The framework shipped no interview at all, and nobody had noticed.
See [0013](.docs/decisions/0013-the-interview-ships-as-text.md).

### Added

- `blueprints/setup/interview.md`. Seven questions and 217 words, asked verbatim. `procedure.md`
  Step 4 points at it and requires it unaltered. It exists because a topic list is a prediction about
  whoever renders it: the same five topics, under one harness four days apart, produced an interview
  the owner accepted and one he refused.
- A `Blueprint Version` for `blueprints/setup/`, which had never had one, so no release could record
  that it moved. It starts at `0.11.0` rather than pretending to a history it cannot evidence, the
  way `blueprints/checks/` started at `0.9.0`. The argument for leaving that folder uncounted was
  that nobody adopts anything out of it, and that stopped holding the moment it began shipping text
  a person reads.

### Changed

- **`procedure.md` Step 4 stops describing questions and starts pointing at them.** From 463 words to
  227.
- Two surviving fragments of the old boundary form, four releases after `0.10.0` inverted it. Step 4
  told the assistant to ask "what it does not cover" — **the exact question the owner refused in the
  first aborted adoption** — repaired alone in `3363d09` before this release was drafted. And the
  rule at the top of `procedure.md` still said documents carry "what the project does not do". The
  second was missed by the grep that found the first, which searched "does not cover" and "exclu".

### Removed

- **Step 4's apparatus for drafting questions**, which is dead once the questions are fixed: the
  five-topic sentence, "ask in one block", and the four-things-to-avoid list with its principles
  exception.
- The claim in `setup/README.md` that the interview asks for a component's posture. It has not since
  `0.6.0`; the assistant proposes it.

`blueprints/setup/` grows from 3900 words to 4121, +221. That is the exchange: the folder a person
never reads grows by 221 words so that the message a person does read falls from about 503 to 203.

The shipped-line metric is unchanged. **41 non-blank lines for a project scope and 22 for a
component**, as it has been since `0.7.0`. This release changes what a person is asked, not what an
adopted project carries.

### Also in this release, and not caused by it

- **`README.md` loses its blueprint version column**, in which two of four rows had gone stale by
  three releases. Each blueprint's own `README.md` carries its version; repeating them here was
  principle 5 doing what it says. Also repaired there: the claim that `blueprints/checks/` holds two
  checks, when it has held three since `0.9.0`, and a sixth surviving fragment of the pre-`0.10.0`
  boundary form.
- **`README.md` gains an upgrade answer**, in the `Status` section where somebody deciding whether to
  upgrade would meet it: what six releases from `0.8.0` to `0.10.2` bought an adopter, measured. One
  boundary sentence, one 50-line fragment removed, one new check. **It says plainly that the owner's
  hypothesis — that `0.7` was already enough — is confirmed except for `registry-check`.** Written
  2026-08-29 in `7e7f8df`, before this release was drafted.
- **`.docs/handover.md` and `.docs/backlog.md` carry the previous session's save-state**, committed in
  `02e7e75` after `v0.10.2` was tagged. It records the second aborted adoption. It changes no rule and
  causes no version, and it appears in this release's diff only because it landed between two tags.

### On the evidence

Fifteen runs, all logged in [`.docs/runs/`](.docs/runs/), four pre-registrations scored.

**What carried this.** Added prose measured at **zero words in four runs of the script across two
scopes**, similarity 1.000 each time, plus a fifth run of the exact released text with the same
result. The pre-registration named deletion of the draft as the response to failure, and named it
before the draft was written.

**What did not carry it, and it was this session's own best argument.** The claim that the question
block varies with the folder. A control arm on a deliberately different scope moved it by **−3.5%**,
inside the band pre-registered as weakening it. **That finding is marked down, and it is named here
rather than allowed to disappear between two documents.** The length experiment that preceded it came
out **indeterminate** and is evidence for nothing.

**Fidelity is not sufficiency.** Every run had writing disabled and stopped at the questions. Nobody
answered them and no `PROJECT.md` was produced. The six questions are proven to arrive verbatim; they
are **not** proven to be enough to write a complete document from. **So `0.11.0` is provisional in
exactly the way `0.10.0` through `0.10.2` are, and the ArtGlina adoption is the one instrument that
settles all four.**

**A placeholder map found a real defect in this tree before it was tagged, for two runs.** Every one
of `PROJECT.md`'s twelve placeholders needs a source: six come from questions, three from proposals,
two are read. **The twelfth, `<DOCUMENT_OWNER>`, had none** — no question asked it, it cannot be seen
in an empty folder, and `interview.md` listed it among the proposals while naming no source, unlike
the other three. Two sessions given the six answers, with no name anywhere in the prompt, both wrote
`Alex` and **sourced it differently**: one from the account identity, one **from the framework's own
`PROJECT.md`**. That second route writes `Alex` into the document of anybody who adopts this
framework, and it was right here only because the adopter and the framework's owner are the same
person. **So the interview is seven questions**, and the released text was run again to keep the
shipped bytes run bytes. The general rule it leaves: a proposal earns its place only if the
assistant note names where it comes from.

**A shipped script ships its defects with perfect fidelity.** The draft's question 5 named a summary
table "below" that is not below. Four runs reproduced the false clause four times, where an
unspecified interview would have repaired it silently. Repaired before release, and the released text
was run once to make the run bytes the shipped bytes — the thing `0.9.0` failed to do.

**The component interview is untouched and it is the half that happens more often.** A project has
one scope and as many components as it has folders. `new-component.md` still builds its interview
from topics. The asymmetry is deliberate: every one of the eleven runs is on the scope interview, the
component interview has never been measured once, and specifying it now would be writing text from an
argument rather than from evidence.

## [0.10.2] - 2026-08-29

**The razor governs what the blueprint offers, not what an owner writes.** One sentence the framework
had never said.

### Added

- The project blueprint's README states it where a reader meets the culled default: `0008` is a rule
  about what ships into every adopted project, and an owner may put anything he likes in his own
  `Principles` section, including all eight candidates or none. Without this a cull reads as a
  prohibition, and it is not one — the section is his.

### On the evidence

None, and the occasion for it is worth recording. The owner intends to write all eight principles
into ArtGlina's `PROJECT.md`, overruling `0012`'s cull for his own project. That is permitted and
nothing said so. The gap surfaced because somebody exercised a freedom the framework had never
granted in writing.

The ArtGlina pre-registration is amended before the run to match, and the amended arm is stronger
than the one it replaces: instead of asking whether an owner keeps two sentences he was offered, it
runs the six cut principles in a live project. **The failure predicted is not that they are ignored
but that they are obeyed**, with two quotable pairs to watch — "identify the affected scope" against
this framework's own word for a scope, in the document carrying the registry, and "preserve backward
compatibility where practical" against the `Assets` posture's "work here as the task requires".

The second is a rule returning through a different door. `0006` cut four preserve rules from that
posture because an assets folder is live and a rule ordinary work breaks teaches that the document
can be ignored. A project principle puts it back at a level that outranks the posture, and **nothing
in the framework notices a principle colliding with a posture**: the registry states one, the project
document states the other, and no check compares them.

## [0.10.1] - 2026-08-29

**Cold-start question 4 gains a scoring rule, because half of it could not fail.**

### Changed

- The reading notes now score the question's two halves separately, and say that only the first is
  mechanical. The first quotes the coverage line and names its file; there is a right answer in the
  document. The second names something outside, and the document need not contain any near miss, so
  it is scored against the coverage sentence the reader just quoted rather than against the document.
  A passing answer is not in the covered set and is something a person could plausibly ask the
  project for.
- **Three failures are named, two of them mechanical.** *"Not stated here"* is the failure this half
  exists to catch: under a closed inclusion the closure sentence licenses the derivation, so a reader
  who refuses because no exclusion is written has not understood that the boundary is closed, which
  is the habit the old form taught. *Something in the covered set* is checkable against the quote
  given one line earlier. *Something unrelated*, "cooking" for a pottery business, is the judgement
  call and is marked the weakest, to be failed only where the answer needed no reading at all.

### On the evidence

None. `0.10.0` and this repair are both unrun and the backlog says provisional in those words. The
only instrument that exercises them is an adoption, and it comes next.

**Why the half was kept rather than cut.** The two halves test different things. The first asks
whether the boundary was read; the second asks whether it was understood as closed. Under the old
exclusions wording the second job did not exist, because there was nothing to derive.

## [0.10.0] - 2026-08-29

**The boundary becomes a closed inclusion, and the blueprint offers two principles of eight.** Two
decisions, both from the ArtGlina interview, both changing what an adopted project writes. See
[0011](.docs/decisions/0011-the-boundary-is-a-closed-inclusion.md) and
[0012](.docs/decisions/0012-two-default-principles-of-eight.md).

### Changed

- **The boundary is written as what the project covers, closed.** `This project currently covers X.
  Anything else is outside it.` The complaint came from the person answering it: the complement of a
  project is endless and he can get lost in it, while what it covers took one sentence. The closure
  sentence is the boundary — without it the reader has an inventory and no rule. Naming a near miss
  stays available and stops being required.
- **The cold start check inverts with it, and not only in wording.** It asked the reader to name
  something the project does not cover, and its worth was that the answer could only come from
  reading a specific line. Under a closed inclusion "cooking" answers that for almost any project
  with no reading at all, so the question now asks what the project covers and where that is written,
  and then for something adjacent outside it. A boundary easier to write is worth little if the check
  that made it load-bearing can no longer tell whether it was read.
- **`Principles` gains a default of two, offered rather than pre-filled.** They are named in the
  blueprint's README, offered aloud in the interview, shown in the summary table as proposed, and
  written only if kept. Saying nothing leaves the section empty.
- `procedure.md` Step 4's "ask for it empty" gains its one exception, principles, with the reason:
  they are not a fact about the world that a wrong guess corrupts, and an owner with none settled is
  better served by two to reject than by a blank page.

### Removed

- **Six of the eight candidate principles**, each cut against `0008` rather than as a group.
  *Understand the current architecture* and *Prefer improving existing patterns over introducing new
  ones* were cut by `0003` already, by name, as behaviour any competent assistant has. *Read relevant
  documentation* is compelled by the stubs before any task. *Identify the affected scope* collides
  with this framework's own word for a project scope, in the document that carries the registry.
  *Keep the framework simple and internally consistent* restates another principle on one half and is
  enforced by `structure-check` on the other. *Preserve backward compatibility where practical* is
  empty in a folder of photographs.
- The exclusions form of the boundary, for new adoptions. **A project already adopted under it stays
  valid and is not rewritten.** Both forms answer the same question, and a migration would cost every
  adopted project a rewrite to gain nothing an assistant can act on.

### On the evidence

Neither change has been run. The two surviving principles rest on this framework's own use and have
never been offered to an owner; the boundary rests on one complaint and an argument about failure
direction. ArtGlina is adopted next, blind, with both changes live, and the pre-registration says in
advance what each outcome would mean.

**The argument that decided the boundary, kept because it is the one that transfers.** The two forms
fail in opposite directions. An exclusions list that misses something leaves it in scope, so an
assistant does the work and nobody finds out. A closed inclusion that misses something leaves it
outside, so an assistant asks. Failing towards asking is the direction the framework already chose,
in the stub's "if you cannot reach it, say so and stop".

## [0.9.4] - 2026-08-29

**`structure-check` row 4 names the comparison it makes.** The first of its rows repaired and run in
both directions.

### Changed

- **Row 4 states its procedure and requires the tool to say it performed it.** It used to ask for
  "the same text, apart from their first heading, apart from any line beginning with the at sign, and
  ignoring blank lines", leaving the tool to decide what sameness means. It now says: remove each
  file's first heading line, every line whose first non-blank character is an at sign, and every
  blank line; compare the remainder in order, character for character; report the line counts and
  what was removed; on a failure quote the first differing pair with a line number from each file.

### On the evidence

Row 4 ranked first of fourteen in the audit, over both axes: a wrong answer is a silent pass on two
stubs that differ, and nothing else covers it beyond the naming line. Run twice on correct stubs, it
passed and stated the procedure unprompted each time, down to naming the blank lines by number. Run
once against one word changed in one file, it failed and quoted the pair.

Row 7 passed in that arm, so row 4 fired alone, which is what the arm was built to isolate. Row 9
passed while quoting both variants side by side, showing it reads the claim rather than matching
fixed wording — registered in advance as its falsifier.

### Also in this release, from `.docs/` and causing no version of their own

An ownership map for `structure-check`: one line per defect, the row that owns it, and any row that
also fires. It exists because the overlap between rows 10 and 13 was found by accident, and it
records three defects no row owns at all. The audit's ranking is re-derived over two axes rather than
one, after a run showed a row can be wrong and harmless.

## [0.9.3] - 2026-08-29

**Two instruments repaired: the release step, and the row that never asked one question.**

### Changed

- **The release verification step moves between the commit and the tag.** It was placed before the
  commit and its commands are written for after it, so on its first real use it passed only because
  the operator supplied what it left out: `$PREV..HEAD` could not see uncommitted work, so a
  `--cached` command the procedure does not contain was invented on the spot, and `git status`
  printed ten modified files against a criterion saying it must print none. A step a tool has to
  repair in order to pass is a step that was not asking what it meant. Between the commit and the
  tag, `HEAD` is the tree the tag will name and a clean `git status` means something; after the tag,
  which is the only other place those commands work, a defect found is already permanent. The step
  now says that reaching for a command it does not contain is itself the finding.
- **`registry-check` check 4 names which line it compares against.** The row asked for "the address
  `PROJECT.md` gives for itself", and the document offers two lines answering to that description: a
  synced-store address and a local path. Across five logs, one unchanged component's row 4 cited
  three different comparands while passing every time. The two readings are two different checks, so
  the row now asks them separately. A relative address resolves and is compared against the folder
  the check runs in, against no line of text and explicitly not against the local path line, which is
  a hint. Any other address is compared as text against the `Address:` line, named as that line.

### On the evidence

Check 4's rewrite was run twice, with no plant, on a scope that discriminates as it stands because
one component carries `../` and the other the synced-store address verbatim. Both runs cited exactly
what was pre-registered: the relative component citing its stub lines and the resolved path and
neither line 39 nor line 45, the other citing line 39 and not 45. `Failed rows: 0` both times.

Worth stating precisely, because it is not the usual result: the verdicts were never wrong. Row 4
passed in all five earlier logs while doing a different thing each time. What was broken was the
question, and what the runs show is one question being answered twice.

This release was the first cut through the corrected procedure, verification run between the commit
and the tag, with no command invented.

## [0.9.2] - 2026-08-29

**The second razor, measured on a check for the first time.** A removal and the run that tested it.

### Removed

- The sentence in `registry-check` row 1 restating the three cases the condition above it already
  covers. `0.9.1` stated the cascade as one condition and then enumerated the cases again, so three
  lines became five and that release's claim of a removal was not visible in its own tree.

### On the evidence

`0008` says a rule earns its place only if an assistant would do otherwise without it. Every
application of it so far had been settled by reading, including the reading that cut this clause.
This one was measured, because the arm already existed: two logs, agreeing on every row, produced by
a prompt differing from the cut one by exactly this clause.

Run twice against the cut text, on the same plant. Every verdict identical to both baselines,
`Failed rows: 0`. The prediction was registered as the claim being tested, with the falsifier named
as the same verdicts reached by visibly different reasoning, since `0008` cuts on behaviour and not
on outcomes.

Two differences in the evidence columns were examined and neither survived. The wording of the
silence reason varies more between the two baselines than between either baseline and the cut arm. A
phrase missing from the first cut run reappeared in the second, and its source is a part of row 1 the
cut never touched.

**The reading and the running agreed, and that is a smaller result than it looks.** One clause, one
check, one tool, four runs. It says the razor's reading was right here. It does not say reading is
generally a safe substitute for running, and the backlog item about re-measuring the razor when the
model or the tool changes stands with one more measurement under it.

## [0.9.1] - 2026-08-29

**The n/a rule reaches the branch it was missing.** A fix and its run, no new capability.

### Changed

- `registry-check` row 1 states its cascade as one condition instead of enumerating cases. **Unless
  row 1 confirmed the folder exists, rows 2 to 6 are n/a and name it.** The `0.9.0` wording fired on
  one of row 1's three outcomes, leaving the other two, a component not yet attached and a component
  addressed off this machine, with no folder to read and no rule telling them to stay silent. That is
  the pathology the cascade exists for, one branch over in the same row, and a project with a GitHub
  URL in its registry meets it on a first run.
- `What this check cannot see` now says that a green table can mean nothing was audited. A project
  whose components all sit off this machine produces `n/a` on every row and `Failed rows: 0`, which
  looks like a pass. Read the table, not the count: if no row says pass, nothing was checked. This
  was registered in advance as the risk of the fix and confirmed as its honest behaviour.

### Removed

- The three cases in row 1's cascade, replaced by the condition they had in common: one rule instead
  of an enumeration, covering the two branches the enumeration had missed.

  **As tagged, this release did not show that removal.** The sentence stating the condition was
  followed by another restating all three cases, so `v0.9.1` points at a tree where three lines had
  become five. Fewer rules, more words. The restatement was cut afterwards, judged by `0008`: it
  prescribed nothing the condition above it did not already say, and a clause that changes no
  behaviour does not earn a document.

### On the evidence

Run twice against a scope whose component was given a repository address and no local path. Check 1
returned n/a on that branch with the reason, rows 2 to 6 returned n/a naming row 1, the other
component was untouched, check 7 invented no folder, `Failed rows: 0` both times. Pre-registered in
`.docs/predictions/registry-check-unreachable-component.md`, with three falsifying outcomes named
before the run and none of them observed.

### Correction to the 0.9.0 entry

Its evidence section claimed `structure-check` had "passed twice" a stale registry path. It had not:
those passes were on 2026-08-25, when the path was still correct. The claim was never established at
any point, and it reached three documents before being caught by reading them back. `git log -S`
places its first appearance in `381b200`, the commit that created `registry-check.md`.

## [0.9.0] - 2026-08-29

**A third check, and a measured limit on what a check is worth.** See
[decision 0009](.docs/decisions/0009-a-check-declares-its-read-set-in-advance.md).

### Added

- `blueprints/checks/registry-check.md`. It walks the registry from `PROJECT.md`, opens each declared
  component's stubs, and reports where the two disagree. It is the only check that reads more than
  one folder, and the first to carry a precondition: it runs from the scope, on the side of any
  filesystem boundary that reaches every component.
- **A rule governing every check written from now on.** A check declares its read set in advance, and
  that set must be computable from documents before any file is opened. The one-folder constraint on
  `structure-check` turns out to be a special case of it. Recorded as a second bounded scope rather
  than an exception, because an exception invites the next one and gives no way to judge it.
- A `Blueprint Version` for `blueprints/checks/`, which had never had one, so no release could record
  that it moved. It starts at `0.9.0`, the release that gave it a counter, rather than pretending to
  a history it cannot evidence.
- `.docs/runs/`, holding the raw output of every check run, verbatim and unedited, with an index
  naming the prompt version, the arm, the scope state and the date. A finding was disputed this week
  against a summary of a table that had dropped the row carrying it, and settled by opening the log.
  A paraphrase of a run is not the run.
- `.docs/predictions/`, holding a pre-registration per run. Four so far, each written and committed
  before the run it describes, and one of them scored a prediction of mine as wrong.

### Changed

- `blueprints/checks/README.md` states what a mechanical check is worth. It claimed a result that
  does not depend on the tool's judgment; that holds only as far as each row is fully specified.
  Where a row leaves something unsaid the tool supplies the missing rule itself, differently on
  different runs, and returns an equally confident table either way. Measured, not supposed: the same
  prompt on the same scope produced two different verdicts on one row and two different readings of
  the line that counts failures.

### On the evidence

`registry-check` was run seven times, three of them pre-registered: as written, repaired, as a
control against its own unrepaired self, twice against a scope with one line deliberately broken,
and twice more against the text that actually shipped.

Those last two matter, and they are the reason this section was rewritten after release. The `n/a`
rule below was written into the release commit itself, so for a few hours `0.9.0` shipped a prompt no
run had ever used, which is the state principle 6 exists to prevent. The backlog said provisional in
those words until the shipped text had been run. It has: one failure for the planted defect, five
`n/a` rows naming it, nothing correct touched, `Failed rows: 1`, twice.

The planted defect was the `WordPress 7 Engine`'s registry block naming a path the folder had moved
away from. No check caught that when it happened and none could have: `structure-check` had passed
that block twice, but on 2026-08-25 when the path was still correct, and it may not read outside the
folder it audits.

Two things it still cannot do. Check 4 has never failed on a real defect, only on a false one now
repaired, so the moved-parent case is untested. Check 7 cannot be tested by any honest run: a tool
that stays inside its read set passes it whether the row is well specified or not.

### Removed

- **Five verdicts per absent component.** When `registry-check` cannot find a component's folder, the
  five rows downstream of that no longer return a result. They are `n/a`, naming the row that
  stopped them. The check now declines to answer questions it used to answer, and that is the
  exchange principle 7 asks a release to name: what it buys is that the verdicts it does give are
  load-bearing. The rows it stopped producing were not merely redundant, they were unstable and
  sometimes wrong, one of them passing a component whose folder does not exist on the grounds that a
  missing folder contains no `PROJECT.md`.
- **The full-folder listing in check 6.** The row asks for one probe of one path now. The listing was
  where its instability came from, and it was the least stable row in the check.

### Known defect in this release's tag

`v0.9.0` points at `7a30e13`, whose tree contains `.docs/runs/README.md` and none of the logs it
indexes, because a global `*.log` ignore excluded them silently. The logs landed in `b699d47`
immediately after, with the checksums the index already claimed. The tag was left where it is: moving
it would rewrite published history to tidy away the one place this class of defect is visible in the
record itself.

## [0.8.0] - 2026-08-29

**A rule earns a document only if it changes behaviour.** The second razor, measured rather than
argued. See
[decision 0008](.docs/decisions/0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md).

### Added

- The razor itself. `0004` cuts facts, this cuts rules, and between them nothing enters a document
  because it is true, sensible or good practice. A rule earns its place only if an assistant would
  do otherwise without it.
- The Repository Blueprint states that test where it used to offer a fragment, and names the case
  worth catching: ordinary good practice for the platform reads as diligence and changes nothing.
- A criterion for `1.0` in the `README`, because "the contract is not stable" said nothing about
  what would make it stable. Two things, both checkable, neither yet true: the shape survives a
  project somebody other than its author adopted and then worked in, and a check catches a defect
  nobody planted.

### Removed

- `blueprints/repository/platforms/` and the WordPress fragment inside it, along with the four
  places that pointed at them. A platform rule is a rule about how one works with a widely used
  platform, which is exactly what a competent assistant already does; the property that makes it a
  platform rule is the property that makes it decoration.
- The nine bullets in the `WordPress 7 Engine`'s `REPOSITORY.md`, and so that file, and so the two
  stub sentences naming it and the `@REPOSITORY.md` import. Removed as one operation: the half-done
  state, a file with no pointers or pointers with no file, is what ruined the first attempt at the
  control arm.

### Changed

- The Repository Blueprint moves to `0.7.0`. Project, component and assets are untouched and stay
  where they were, all four carrying `Framework Version: 0.8.0`.
- `Local rules` goes back to being empty by default, which is what the blueprints always said it
  usually is. The blueprint had begun pre-filling the one section an owner was meant to write.

### Not changed, deliberately

- The rule that travels with the word `Repository`, that platform or framework core changes only
  through its own update mechanism. It sits in the registry, both arms of the experiment carried it,
  and both arms cited it. It was therefore not tested, and untested rules are not cut. `0.6.0` cut
  four rules for never having been run; this release cuts nine for having been run and made no
  difference. The same principle in opposite directions, and neither settled by argument.

### On the evidence

One task, one tool, one run per arm, in a domain the model knows well, which is the most favourable
ground for concluding that a WordPress rule is redundant and the least favourable for the opposite.
What remains untested is the category the first razor exists to protect: a rule about something an
assistant could not otherwise know, such as a generated directory or a vendored dependency. The
razor is adopted on evidence from one side of its own boundary, and the backlog carries the
re-measurement that follows from that.

## [0.7.0] - 2026-08-25

**A component with no address says so.** See
[decision 0007](.docs/decisions/0007-a-component-with-no-address-says-so.md).

### Added

- A fourth address form: none, said plainly, with the reason.
  `Address: none. No copy of this folder exists off this machine.` The criterion is a copy that
  exists off the machine, not version control: `git init` changes nothing here, and only a remote,
  a synced store or a containing folder that travels makes an address possible.
- `structure-check` 11 now knows what an address is and requires one of the four forms. It used to
  ask for one without saying what made one valid, which let a machine-local path into the slot and
  certified it as a pass.
- A table in the `README`, under **Filesystem boundaries**, answering "does any of this apply to me"
  in one glance. Three rows, and the first is "everything in one filesystem, nothing to do". The
  reasoning stays in `.docs/architecture.md`, which now points at the table rather than repeating it.

### Changed

- The session note is a precondition rather than a preference, and names the side from which every
  local path in the document is read. When a project spans a boundary one side usually reaches both
  and the other does not; read from the wrong side the paths are false rather than awkward.
- `.docs/architecture.md` says out loud that everything it knows about filesystem boundaries comes
  from one project, one machine and one person. A macOS setup with a network volume is expected to
  behave the same way and has not been tried.
- Blueprint versions now move only when that blueprint moves. `0.7.0` changed the project blueprint
  alone; component, repository and assets stay at `0.6.0` and carry `Framework Version: 0.7.0`.

### Rejected

- Naming the machine in the address, as `Machine-local. WSL on some-laptop`. It reads as an address,
  invites being followed, and becomes false the day the machine is replaced.
- Refusing to register such a folder at all. Under that rule `~/wordpress-7` would carry no stubs and
  no pointer to `PROJECT.md`, and the run where an assistant refused to set up a staging deployment
  and routed the decision back could not have happened.
- Reaching the WSL filesystem from Windows through `\\wsl.localhost\...` and calling that an address.
  It resolves, which is the problem: the name is a local alias, so on another machine it returns a
  different folder rather than an error.

**The accepted cost, stated plainly.** A reader on another machine gets a component's name, its
posture and a dead end. No wording produces a copy of a folder that exists in one place, and a
document implying otherwise is worse than one that says so. The gap runs one way only: the
component's own stubs still point upward with an address that resolves from anywhere, which is the
direction the framework exists for.

## [0.6.0] - 2026-08-24

A cut at what the postures carry. **Both inherit the project's principles. `Assets` adds nothing.
`Repository` adds one rule.** See
[decision 0006](.docs/decisions/0006-the-postures-carry-one-rule-between-them.md).

### Added

- One rule travelling with the word `Repository`: platform or framework core changes only through
  its own update mechanism, never by hand. The axis is ownership rather than immutability, so an
  upgrade that replaces core wholesale is the owner doing its job and a hand edit in the same files
  is not.
- `structure-check` 11 now fails a `Repository` block written without that rule, since the rule is
  the entire difference between the two words.
- A sixth thing to establish at Step 2 of the setup procedure: whether the folder holds code a
  platform or framework updates. It is the only reason to look at the contents, and it is what
  settles the posture.

### Changed

- The postures stop being opposites. `0.5.0` described them as two directions, change against
  preserve. They are a floor and one layer now, and one of them is empty.
- An `Assets` registry block reads `Assets. Live material. Work here as the task requires.`
- The component interview drops to two questions, the name and whether the folder has a rule of its
  own. The posture is proposed from what was seen and shown in the summary table as settled, where
  it can be overturned in a sentence.
- Cold start question 3 changes axis. It asked whether things get changed here or found and left
  alone. It now asks what limits what may be changed here and where that is written, which both
  postures answer only by reaching the parent.
- Cold start question 4 asks for the project boundary instead of any rule governing the folder.
  Under `0.6.0` the old question had the same answer as question 3 for an assets component, and the
  boundary is the one rule in the framework with a measured before and after.
- The assets override changes purpose. It is now where something in a live folder gets held still.
- `structure-check` 10 says what it means: an override may point at where the posture is stated and
  may not state it. The blueprint headers were rewritten so a literal reading cannot fail a correct
  file.

### Removed

- The four preserve rules: do not reorganize, do not rename, do not move, preserve the existing
  organization. An assets folder is live, and a rule that ordinary work breaks every day teaches an
  assistant that the document can be ignored.
- The posture question from the component interview. Whether platform code sits in the folder is
  visible, and `0004` forbids asking about what can be read.
- The rule about `blueprints/` from this repository's own adapters. Every blueprint file carries a
  visible notice at the top, so the rule described something already on screen, and
  `blueprints/project/README.md` forbids adapters from carrying rules at all.

**The accepted cost, stated plainly.** Nothing now stops an assistant rearranging a folder of
material on its own initiative. The rules that would have stopped it were never run: the assets
posture has not been used end to end on `0.5.0`. A folder that genuinely needs its arrangement held
is what `ASSETS.md` is for, and that is now the first real case the assets override has had.

**Closed.** Whether the two postures should collapse into one flag, and whether the pair should be
renamed. Both stay. `Repository` carries a layer that is expected to grow, and a layer that grows
needs somewhere to grow into.

### Documentation

- The project scope is described by the three states a project passes through: no documents, this
  scope alone with an empty registry, this scope with components. A single folder that has grown
  rules takes the scope on its own, and that is a finished setup rather than half of one. The old
  rule sent such a project to the component blueprint, which sends it straight back.
- `.docs/architecture.md` names the scope's second job: since `0.5.0` a component holds no document
  of its own, so a one-folder project still comes here for anything it wants to record.
- Both checks stop describing "a component that appears in no registry" as an uncovered gap. Under
  `0.5.0` such a folder is not a component at all. What is uncovered is a component whose stubs and
  registry block have drifted apart, and that needs a prompt reading both scopes at once.
- `register` becomes `registry` in `README.md` and `.docs/architecture.md`, matching every blueprint.
- The root of a project scope holds no second AI entry point, which is what the rule always meant.
  It says nothing about a `README.md` or a `LICENSE`.
- Step 2 of the setup procedure said four things and listed five.
- The `Status` section records the metric behind its numbers: non-blank lines, summed across the
  files of a scope.

## [0.5.0] - 2026-08-23

A third cut, at the number of documents rather than their contents. **The registry carries the
component; the component carries two stubs.** See
[decision 0005](.docs/decisions/0005-the-registry-carries-the-component.md).

### Added

- `blueprints/component/`, the normal way a folder is attached to a project. Two stubs, `AGENTS.md`
  and `CLAUDE.md`, identical apart from the heading. They name which component the folder is, carry
  the parent's address, and stop.
- A posture line in every registry block: `Repository` where things get changed, `Assets` where they
  are kept, and for `Assets` the four preserve rules travel with the word. This is the only thing a
  component is ever told about itself.
- An instruction in the stubs to fail loudly. An assistant that cannot reach `PROJECT.md` says so and
  stops, rather than working on whatever it can see.
- One rule that ends a whole class of setup question: a folder that has not been declared a
  component is not one. It is files, belonging to whichever component contains it and taking that
  component's posture. Being a component is a decision written into the registry, not a property of
  what sits on disk, so no tree gets surveyed for candidates.
- `blueprints/setup/new-component.md`, one prompt for any component. Three questions: what it is
  called, whether things get changed here or kept, and whether it has a rule of its own yet.
- A rule for local paths at setup: resolve the path in the exact form you mean to write, and when it
  holds only because of a symlink or mount, name that arrangement and the command that creates it. A
  `~/` path under a synced store read from another filesystem is true on the machine it was written
  on and false everywhere else, and nothing in any file records why. Observed twice: one setup run
  volunteered the symlink line, the next did not, from the same blueprint.
- Two checks. `structure-check` now verifies that the two stubs carry the same text, and that every
  registry block names a posture.

### Changed

- `REPOSITORY.md` and `ASSETS.md` are demoted from the normal way to attach a component to the
  override, for a folder that has rules of its own. Both keep `Local rules` and `Hazards` and nothing
  else.
- A registry address says where the component is, read from `PROJECT.md`. A component's stubs say
  where the parent is, read from the component. The two point opposite ways and carry different
  values, which the old component entry point hid by holding only one of them.
- The registry is authoritative. Where an override and the registry disagree about a component, the
  registry is right and the override is a bug.
- The `@` import in `CLAUDE.md` is restricted to a file in the same folder. Across a mount boundary it
  would state the parent's location a second time in a second format, and its failure mode is silent:
  a declined approval disables it permanently without saying so again.
- The cold start check for a component asks a different question. It now tests one chain end to end,
  stub to parent to the registry block, by asking whether things are changed or kept in this folder
  and what said so.

### Removed

- The component entry point as the normal case. A component holds no document of its own unless it
  has something to say that is true of it alone.
- The escalation boundary, `<PROJECT_WIDE_CONCERNS>`. It existed so a component would not walk up to
  a long parent without cause, and the parent is 33 lines. Reading it every time costs nothing.
- `Parent checked`, with the file that held it. A component holds no copy of anything in the parent
  except the address, so nothing it holds can fall out of date on its own.
- The parent address and the posture from `REPOSITORY.md` and `ASSETS.md`. Both are in the parent.
- The four preserve rules from `ASSETS.md`. They follow from the word `Assets` rather than from any
  particular folder, so they are written once in the registry.
- `blueprints/setup/new-repository.md` and `blueprints/setup/new-assets.md`, replaced by the single
  component prompt.

A component falls from three files to two and from 32 shipped lines to 22. The larger change is that
none of the 22 is a decision: two lines are the parent address and the rest are fixed text. Adding,
renaming or moving a component becomes one edit in one file.

**The accepted cost, stated plainly.** A component that cannot reach its parent now knows nothing at
all. Copying the posture down into the stub was rejected because it puts one rule in two places. The
stub fails loudly instead.

### Fixed after the validation run

The whole of `0.6.0` was validated by resetting a real project to bare folders and re-adopting it:
three scopes, three structure checks at 14/14, three cold starts at 5/5, plus two behavioural tests.
These are what the run turned up.

- `<SESSION_NOTE>` is split in two. `<PATH_NOTE>` says what makes the local path true and has nothing
  to do with components; `<SESSION_NOTE>` says where to start a session and depends entirely on them.
  A scope with no components needed the first and not the second, and one placeholder could not carry
  that. Three separate agents split them by hand during the run.
- Attaching a component now revisits the parent's session note. A scope adopted with no components
  correctly has none, and attaching one across a mount boundary makes it necessary; step 7 of the
  procedure covered only the stubs and the registry block, so nothing brought it back.
- `structure-check` 11 answers the empty registry. Two tools ran the same prompt on the same folder
  and disagreed, `n/a` against `pass`, because 11 is a presence check and the prompt tells a presence
  check with nothing to quote to fail. No blocks now passes when the document says so in visible text.
- `structure-check` 14 is no longer gated on the session note, so it can finally run. The first scope
  to carry a symlink line had no components, no boundary and no note, which left the one line holding
  its path up verified by nothing.
- `<SCOPE_EXCLUDES>` carries the undecided case. The fixed sentence had no empty form, so an agent
  improvised a replacement paragraph containing an instruction it invented. Measured on the way:
  with the boundary written as "not decided yet", two tools independently answered the boundary
  question by quoting a sentence about a component not being *attached*. An absent boundary is a
  decoy rather than a hole.
- The project-scope cold start catches up. Its question 3 still asked "changed there or kept", the
  axis this release removed, and it assumed at least one component existed.
- The three states make room for a project that has recorded nothing yet and knows a second place is
  coming. The text this release replaced carried "and no second one planned".
- "Knows nothing at all" is corrected. With its parent folder moved away, a component reported the
  failure before answering anything, found the folder at its new path, refused to open it because
  following it would be the guess the stub forbids, and named what it could not know. It is cut off
  from the posture and the principles; it is not left knowing nothing.
- The project blueprint says component state belongs to the registry alone. A sentence in "What this
  project is" saying the installation was not attached had to be repaired by hand the moment it was.
- `platforms/wordpress.md` is rewritten for `0.6.0`. It had told its reader to fill a
  `Platform Principles` section and a `<PLATFORM_PRINCIPLES>` placeholder, neither of which had
  existed since `0.5.0`, and it instructed dropping WooCommerce lines it did not contain. Used
  anyway, it produced no error: the agent mapped the old names onto the new ones silently. It now
  carries the blueprint version it was written against, and the rule about core is gone from it,
  because the registry carries that since `0.6.0`.

### Documentation

The framework's own documents were rebuilt to the shape they describe, having drifted three versions
behind it.

- `PROJECT.md` falls from 302 lines to 78 and follows the Project Blueprint. Gone with it: the
  `Project Version` counter, `Scope Ownership`, `Scope Entry Points`, `Framework Structure`,
  `Sources of Truth`, `Blueprint Lifecycle`, `Success Criteria` and `Long-Term Vision`, all of which
  described machinery that no longer exists or restated what the README already said.
- `README.md` falls from 238 lines to 130 and stops repeating `PROJECT.md`. It answers what the
  framework is for and how to adopt one; `PROJECT.md` is the entry point for working on it.
- `.docs/architecture.md` is rewritten for the current shape: why the registry cannot live anywhere
  else, what a component is told, the two address directions, and what a path spanning a mount
  boundary needs.
- The purpose is stated once, at the top of both: one roof over a project that lives in more than one
  place, one entry point holding the register, project-wide truth written once and each part
  answerable only for itself.
- Decision `0002` is marked superseded, and `0003`'s four jobs are marked as superseded by the single
  test in `0004`. Neither file is deleted; the record of why something existed outlives it.

---

## [0.4.0] - 2026-08-23

A second cut, deeper than `0.3.0` and made against a single rule instead of a list of jobs:
**a document carries what cannot be seen, and nothing that can.** See
[decision 0004](.docs/decisions/0004-documents-carry-what-cannot-be-seen.md).

### Changed

- The framework's purpose is stated as navigation. Working in one folder, an assistant reads the
  registry and reaches another that may sit on a different disk or in a different filesystem. The
  registry and the shared rules at the root are the feature; the rest supports them.
- A registry entry carries what a move needs and nothing else: name, one line, address, local path,
  entry point. Platform and production are gone from it.
- A component's own rules become one free `Local rules` section that may be left empty. The
  Repository Blueprint no longer prescribes what goes in it beyond the platform fragments.
- `Hazards` narrows again: only what an assistant cannot find by looking. Whether a `.git` exists is
  visible, so it no longer qualifies. Most components will delete the section.
- Folder naming is documented in the root `README.md`, where somebody creating a project will read
  it, rather than inside a blueprint comment. Hyphens or underscores; a space costs a pair of quotes
  in every shell command forever.

### Added

- `<SESSION_NOTE>` in the project blueprint: where to start a session so every component in the
  registry resolves, for projects whose components sit on different sides of a mount boundary. Not
  visible in any file and not inferable from one.

### Removed

- Every description of contents, from all three blueprints. An assistant can look.
- `Development Environment` and the platform, environment and URL fields with it.
- `Scope Ownership`, `Workstreams`, and the separate `Project Overview` and `Project Scope` sections,
  which merge into one short statement of what the project is and does not cover.
- The `.docs/` inventory from the component blueprints.

The text that ships into an adopted project falls from 166 lines to 88: a project scope of 33 lines,
a repository component of 25, an asset component of 30. The setup procedure falls from 320 lines to
145, because an interview cannot be longer than the fields it fills.

---

## [0.3.0] - 2026-08-22

Version `0.3.0` removes more than it adds. The framework had grown for a week until its own author
was reluctant to change it, and the cut brings it back to the four jobs it exists for. See
[decision 0003](.docs/decisions/0003-cut-the-framework-to-four-jobs.md).

### Added

- `blueprints/setup/`: prompts that adopt a blueprint by interview instead of by hand. A shared
  `procedure.md` and three thin entries, one per scope, each carrying the address of the framework
  and of every folder involved. The same file attaches a component on day one and two years later.
- `Environment hazards` in the Assets Blueprint, and a `Handling Rules` section that admits an
  exception for a subfolder holding worked code.
- A third state for the `Production` line: a component whose output somebody else deploys elsewhere.
  It writes `none` and names the handoff without naming the destination, because an address in a
  field called Production reads as a target however the prose around it is worded.
- A rule against spaces in the folder names that make up a project's path, and a note that the
  project's name and its folder need not match.
- A project scope prompt in the cold start check. The component prompt asks about a parent, a
  boundary and an unreachable parent, none of which exist at a project scope, so running it there
  returned three non-answers and measured nothing.

### Changed

- The two component kinds are told apart by what an assistant will mostly do in the folder, change
  things or find them and leave them as they are. The old rule sorted by content, "anything that is
  not a codebase", and broke on the first folder of source kept without version control.
- `<PROJECT_WIDE_CONCERNS>` now always opens with whether the request falls inside the project at
  all. No component can answer that, and without it a request the project excludes arrives looking
  like ordinary technical work. This is the one change in the release with a measured before and
  after: the same task, refused after the edit and started before it.
- Platform fragments are trimmed on adoption rather than copied in full. A rule survives if it can
  fire on work done from this folder.
- A component nested inside its project scope writes `../` and no local path at all.
- The structure check no longer fails a check that asks whether something is absent. Its evidence is
  the search that returned nothing.

### Removed

- All version counters. `Project Version`, `Repository Version`, `Component Version` and
  `Parent Project Version` are gone, along with the obligatory sweep of every component whenever the
  project document changed. A component now records `Parent checked`, the date it was last read
  against the parent, and compares it with the parent's `Last Updated`.
- `Sources of Truth` from both component blueprints, and most of `Project-Wide AI Principles` from
  the project blueprint. Both restated behaviour a competent assistant already has.
- Half of `Change Principles` and most of `Verification`. What survives is the part that is not a
  default: change only what the task needs, remove only your own dead code, reproduce a bug before
  fixing it.
- `Environment access` from the Repository Blueprint. Two paragraphs that never changed an outcome.
- `Development Environment` from the Repository Blueprint. Platform, environment and local URL are
  read off the files, and the parent registry already records the platform and the deployed location
  of every component. `Environment hazards` becomes `Hazards` and narrows to what no file shows and
  no tool catches, which for most repositories is nothing at all.
- `Change Principles` from the Repository Blueprint. The six lines that survived the first cut moved
  up to `Decision Rules` in the project blueprint, under a subsection for components holding code, so
  a new code component inherits them instead of carrying its own copy.

The text that ships into an adopted project falls from 272 lines to 166, and a component entry
point from 100 lines to 45.

---

## [0.2.0] - 2026-08-09

### Added

- Project Scope Blueprint `0.1.0`, derived from one working implementation. Covers the scope that
  holds project-wide context, the registry of the components below it, and the address those
  components point at. It is the only scope that publishes an address rather than consuming one, and
  the only one with no parent, which changes how both checks read against it.
- Decision `0001`: a project scope need not be a repository. Recorded in `.docs/decisions/` with the
  reasoning and the five places that still assumed the old form.
- Two further address forms in `Cross-Scope References`: an account-relative location in a synced
  store, and a relative path when the referenced scope contains the referring one. A repository URL
  remains the first of three rather than the only one.
- `Where the component sits` in the Assets Blueprint: the case of a component nested inside its
  parent's folder, which addresses the parent as `../` and carries no local path at all.
- `Paths across a mount boundary` in both blueprints. A `~/` hint can be true in one environment and
  false in another when the same folder is reached through a mount, and a symlink at the written
  location makes one written form true everywhere.
- A stated escalation boundary in the Assets Blueprint, with a `<PROJECT_WIDE_CONCERNS>` placeholder.
  The blueprint previously said when project context was required and never when it was not, so it
  failed the structure check's own question 9.
- Adapter purity in both adoption guides. Adapters redirect and stop, and anything added to one
  restates what the entry point or the framework already says.
- `Which one you need` in `README.md`: what separates the three blueprints in plain terms, the root
  against the codebase against everything else.
- Rule that an entry point is named for the kind of scope it opens and not for its subject, which
  fixes the set of names at three. A folder organized by workstream is an asset component and
  carries `ASSETS.md`; there is no `MARKETING.md`. Without this, the name slot collects topics and
  the set grows with every new area of work.
- `On a project scope` in the structure check: questions 7, 9 and 10 do not apply where there is no
  parent, and question 11 matters most.
- `A second tool` in the cold start check. The adapters exist because tools look for different
  filenames, so a run in one tool proves only the file that tool opened.

### Changed

- `<CANONICAL_PROJECT_REPOSITORY_URL>` renamed to `<CANONICAL_PROJECT_SCOPE_ADDRESS>` in both
  blueprints, and `<RECOMMENDED_LOCAL_CHECKOUT_PATH>` to `<PARENT_PROJECT_LOCAL_PATH>`. The old names
  named a git artefact and prescribed the answer.
- Structure check question 7 now asks for an address that resolves from outside the machine rather
  than for a repository URL. In its previous form it failed a correct adoption.
- `canonical project repository` replaced with `project scope` throughout both blueprints, including
  the `Documentation` and `Decisions` sections and the design notes.
- Both blueprints raised to `0.2.0`, and the WordPress fragment now names that version.

### Notes

- Every change here comes from one live adoption. A project scope that held one document while all
  its real material sat elsewhere was collapsed into the folder that held the material, and the
  framework had no room for the result.
- The Project Scope Blueprint was released against the owner's judgement rather than the usual
  caution. Its implementation is one day old and has not been lived with, so it is the least settled
  of the three and its README says so. If the arrangement does not hold, this is the blueprint that
  will move first.

## [0.1.0] - 2026-08-09

### Added

- `Scope Entry Points` section: the adapter rule, now stated for every scope rather than for the
  repository root only, and the separation between framework entry point names and the filenames
  external tools discover.
- Rule that a document name belongs to exactly one type of scope, which rules out placing a pointer
  named after another scope's entry point inside a smaller scope.
- `Cross-Scope References` section: a reference to another scope carries a resolvable address, which
  constrains where a referenced scope is allowed to live.
- Rule that a scope states when parent context is actually required.
- Three matching entries in `Design Philosophy`.

- Repository Component Blueprint `0.1.0`, derived from one working implementation. Covers a
  repository that is one component of a larger project.
- Platform fragment library inside the Repository Blueprint, starting with WordPress. Platform rules
  live in one replaceable section, so the blueprint itself stays technology-agnostic.
- `Blueprint Comments` convention: an HTML comment marks an unresolved decision, addresses the
  person adopting the blueprint, and is removed once worked through. Uncommented text is ready to
  use as it stands.
- `Comments` section and a final comment-removal step in both blueprint adoption guides.
- `Example` column in both placeholder tables, and a `Paths` section explaining the home-relative
  form. Every placeholder now has a concrete example.
- Rule at project scope that a local path accompanying an address is written relative to the home
  folder and never with a username: `~` already stands for the folder that contains it.
- An example in every replace-type blueprint comment, including a filled-in header block and the
  address pair that makes the upward reference work.
- `blueprints/checks/`: two prompts for verifying an adoption, shared by every blueprint. The
  structural audit returns a table where every row carries a file and line quote and an unevidenced
  check counts as failed. The cold start check tests whether an assistant opening the folder for the
  first time follows the chain, and states the conditions that make the run valid.
- `Adoption Checks` section in `PROJECT.md` recording why both checks return evidence rather than a
  verdict.
- `.gitattributes` normalizing line endings to LF.

### Changed

- Assets Blueprint raised to `0.1.1`: comment handling, placeholder examples, and address and path
  guidance in `ASSETS.md`.

### Notes

- These rules come from applying the framework to a live project, where an unaddressed reference to
  a parent scope turned out to be unusable in practice.
- The Assets Blueprint already satisfied the new rules and did not change.
- A standalone repository with no parent project is outside the Repository Blueprint's scope for
  now.

## [0.0.1] - 2026-08-08

### Added

- Core framework documentation and the canonical `PROJECT.md` entry point.
- Root `AGENTS.md` and `CLAUDE.md` adapters for AI tools.
- Assets Component Blueprint `0.1.0`, derived from one working implementation.
- Blueprint versioning and parent-project drift-check procedure.
- MIT license.

### Notes

- The framework is in early development; its contract is not yet stable.
- Repository and Project blueprints, reference examples, and documentation guides are planned.
