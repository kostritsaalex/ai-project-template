# 0013. The interview ships as text

**Date:** 2026-08-30  
**Status:** accepted

---

## Context

The framework was refused twice by the only person who can run an adoption. The second refusal was
about the interview, and about its length rather than its questions: *initialization has degraded;
consistency may have improved and the interview got much worse.*

The obvious repair was to cut words from the setup path. **Measurement stopped it.**

**The framework shipped no interview.** Zero question marks in `blueprints/setup/*.md`, zero in
`PROJECT.md`'s comments, not one sentence anywhere addressed to the person being interviewed.
`procedure.md` Step 4 named five topics in a sentence and constrained style in a paragraph. Every
word of every interview was composed fresh by whichever tool held the blueprint.

**And the setup path had barely moved.** Across `v0.7.0..HEAD`: `procedure.md` +4 non-blank lines,
`new-project.md` and `setup/README.md` unchanged, 441 to 468 lines total for everything an assistant
reads. The interview the owner refused was produced by a file four lines longer than the file that
produced the interview he accepted. **A razor aimed at words addressed to a person would have cut
nothing, and building one was the next thing planned.**

**The harness was constant.** Claude Code rendered both. So the variable is the model under it, and
that reframes the problem: `procedure.md` Step 4 is the same kind of claim as
[`0008`](0008-a-rule-earns-a-document-only-if-it-changes-behaviour.md) — a prediction about a reader
rather than a property of a document — and nobody had ever labelled it one. Five topics work exactly
as well as whoever renders them.

`blueprints/checks/` ships literal prompts and is the only part of this framework whose behaviour is
reproducible enough that people argue about specific rows. `setup/` shipped topics. Same job, two
treatments, one folder apart, and the asymmetry had no recorded reason.

## Decision

**The framework ships the wording of the project scope interview as text, the way `checks/` ships
prompts. The tool composes everything the look produces.**

`blueprints/setup/interview.md` holds six questions and 203 words. `procedure.md` Step 4 points at
it and requires it verbatim.

**The line between shipped and generated is not a new one.** It is
[`0004`](0004-documents-carry-what-cannot-be-seen.md) applied to a question instead of to a document:
propose what can be seen, ask only what cannot. A question is folder-independent by construction —
that is what made it a question rather than a proposal — so the shipped half is exactly the half with
no variables in it. The ship/generate split and the propose/ask split are the same split.

Generated, and never in the file: the Step 2 look report; the resolved local path and its form; the
path note and the command that recreates it; each component's posture; whether an override exists;
the document owner; the session note; the summary table; every exception branch in Steps 1 and 2.

**Six questions and not seven, and the reason is in the logs rather than in taste.** Seven appeared
in all four runs of the length experiment and in the refused interview. Six of the seven are stable
across every run — name, what it is, boundary, principles, address, components. **The seventh differs
every time, and three of four were questions the framework had already forbidden**: whether `.docs/`
exists, asked while stating that it does not; the local path, asked after being resolved; the
posture, which Step 4 says in as many words is not a question. The fourth belongs to
`new-component.md`. The seventh slot is not a topic. It is where an unspecified interview puts
whatever it invented that run.

## What the evidence is, and what it is not

**Ten runs, all logged in [`../runs/`](../runs/), two pre-registrations scored.**

**What carried this.** Added prose measured at **zero words in four runs of the script across two
different scopes**, `difflib` similarity 1.000 each time — nothing introduced, glossed, or appended.
That was the one result that could have refuted the proposal, and it was registered in advance with
deletion of the draft as the pre-committed response to failure. Alongside it, a **question block of
203 words against 503** for the unspecified interview, spread 1.2% across two scopes and 0 to 5 words
within an arm.

**What did not carry it, stated because it was argued and then measured.** The claim that the
question block varies with the folder, which was offered as the strongest argument after the length
experiment came out indeterminate. A control arm on a deliberately different scope moved it by
**−3.5%**, inside the band pre-registered as weakening it. **That finding is marked down and does not
support this decision.** ArtGlina's longer interview is better explained by two confounds already
recorded: a one-off instruction to that session to report traces without using them, and a real
project having more to say than a scratch tree.

**The length experiment that preceded all this came out indeterminate** and is not evidence either
way. It is recorded at P3 in its own file.

**What survives of the variance argument is about behaviour, not length.** On one framework version,
one run guessed the owner's business from folder names and invited correction; another refused to
guess on the ground that a plausible guess reads as fact. Both are honest readings of
`procedure.md`'s *"show the draft and ask what is wrong with it."* That is what a fixed wording
settles.

## Consequences

**What this cuts, because principle 7 is not decoration.** Step 4's five-topic sentence, its "ask in
one block" instruction, and its four-things-to-avoid list with the principles exception — the whole
apparatus for drafting questions, which is dead once the questions are fixed. **Step 4 falls from 463
words to 227**, and `procedure.md` as a whole from 1806 to 1575.

`blueprints/setup/` grows from 3900 words to 4121, **+221**, the new file being 399 and the cuts 178.
That is the exchange principle 7 asks a release to name: the folder a person never reads grows by
221 words so that the message a person does read falls from roughly 503 to 203.

**Fidelity is not sufficiency, and this is the limit that matters.** Every run had writing disabled
and stopped at the questions. Nobody answered them and no `PROJECT.md` was produced. **The six
questions are proven to arrive verbatim. They are not proven to be enough to write a complete
document from.** The test for that is an adoption, it is scheduled, and it is the same instrument
that un-provisions `0.10.0` through `0.10.2`. Until it runs, this release is provisional in exactly
the way those three are.

**A shipped script ships its defects with perfect fidelity.** The draft's question 5 referred to a
summary table "below" that is not below — the table is Step 5, after the answers. Four runs
reproduced the false clause four times. An unspecified interview would have repaired it silently.
That is the accepted cost of specifying, stated plainly: the mechanism has no judgement, which is the
point of it and also its price. The clause is repaired in the released text and the released text is
run once before the tag.

**The component interview is untouched, and it is the half that happens more often.** A project has
one scope and as many components as it has folders. `new-component.md` still builds its interview
from topics and is unspecified in exactly the way Step 4 was.

**This asymmetry is deliberate.** The scope interview is where all ten runs are. The component
interview has never been measured — not once, in any experiment in this repository. Specifying it now
would be writing text from an argument rather than from evidence, which is the mistake this entire
sequence was built to avoid. It is named here so that the next session meets it as a known gap rather
than discovering it as a defect.

**`blueprints/setup/` gets a version counter**, starting at `0.11.0` rather than pretending to a
history it cannot evidence, the way `blueprints/checks/` started at `0.9.0`. The argument for leaving
that folder uncounted was that nobody adopts anything out of it. That stopped holding the moment it
began shipping text a person reads.

**The razor question is answered by not needing one.** A third razor was proposed, to cut sentences
addressed to a person. It was never a razor: `0004` cuts facts in documents and `0008` cuts rules in
documents, and both name a corpus, while this one named a category of sentence with no corpus to cut
it from — the framework contained none. **A razor needs a place.** Now that a corpus exists, `0008`
reaches it: an interview question is a rule addressed to whoever renders it, and the six here earn
their place because two renderings of the same five topics differed enough that one was refused.

## Origin

**Decided by the owner, 2026-08-30**, across a day that began with a measurement he required before
any repair and ended with him accepting a result whose strongest argument had been withdrawn by its
own control.

The framework is reviewed by a second assistant whose prompts reach a working session through him, so
a message here may be his words, the review's relayed, or both, and nothing inside the session
distinguishes them. What is certain is the decision, and three of its constraints are his in
substance: that the measurement come before any repair and never in the same pass; that the
indeterminate band be honoured when it was inconvenient; and that the released text be run once
before the tag rather than shipped on the strength of runs against a draft.

What arrived with the review and is recorded as arriving rather than as anyone's: that the third arm
be spent on the cure rather than on a fact whose two outcomes prescribed the same act; that the
result be reported as fidelity and not sufficiency; and that the component asymmetry be stated rather
than fixed.

The two things this session can vouch for are the measurements that changed the diagnosis — that the
framework shipped no interview text at all, and that its own control weakened its own best argument.
