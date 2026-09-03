# Draft: the interview after the owner answered it

> **SUPERSEDED IN PART, 2026-09-03.** The third sub-bullet under "The address" instructs `0007`'s
> fourth form for a project scope. That is wrong and `0.18.0` removed it: a project scope's address is
> required, the fourth form is for component blocks only, and where neither derivation rule fires the
> interview asks. See [`../decisions/0023-a-project-scope-address-is-required.md`](../decisions/0023-a-project-scope-address-is-required.md).
> **Do not take wording for the address rules from this file.** It is kept as the record of what was
> drafted on its date, not as a source.

**Draft, 2026-08-30. Not in `blueprints/`. Nothing ships before he reads it.**
Subject of [`../predictions/interview-v3.md`](../predictions/interview-v3.md).

Four questions still. Three of them change, and two of the changes come from watching where his
answers landed rather than from what he said about them.

---

## For the assistant. Not shown to the person.

Ask the four questions below **verbatim and in order, in one message.** Do not introduce them, gloss
them, add clarifications, or add questions of your own. If something is missing from them, that is a
defect in this file and it is reported afterwards, not patched in the message.

**Everything else is settled by proposal and shown in the summary table, where one sentence overturns
it. Each proposal names where it comes from, and a proposal with no named source is not one:**

- **The project's name** — from the folder name, offered as a draft. The name keeps its spaces and
  the folder need not match, so this is a value to be corrected rather than settled.
- **The address** — derived, and only by the two rules below. If neither yields a value, ask for it.
  - If the local path resolves inside a synced store, the address is the store's name and the path
    within it: `OneDrive, Projects/northwind`.
  - If the scope is a git working copy with a remote, the address is that remote **normalised to a
    URL with its scheme**. If it cannot be normalised to one of the four forms in `0007`, do not
    write it — ask.
  - If there is no copy of this folder anywhere off this machine, the address is `0007`'s fourth
    form: `none`, with the reason. Never a blank, and never a local path in the address slot.
- **The local path**, in the form you resolved in Step 2.
- **The path note**, naming the arrangement that makes that path true and the command that recreates
  it.
- **Each component's posture**, from whether the folder holds code a platform updates wholesale.
- **Whether an override already exists**, from the folder.
- **The session note**, once the components are known.

**Answer 1 has to tell you whether software is all of this project or one part of it.** The question
no longer asks that outright, because a person describing his business answers it without being asked
and asking made him enumerate. Derive it and write it into `<PROJECT_PURPOSE>`. If a business
description genuinely leaves it open, that is the one thing worth a follow-up.

---

## The questions

1. **What it is.** What is this project about? What business does it represent, or what business
   tasks does it solve?

2. **Boundary.** Finish this sentence: *"This project currently covers ______. Anything else is
   outside it."* **This is the sentence an assistant quotes when it declines work that is not part of
   this project.** Name **kinds of work** — `restoration and photography`, `hosting and deployment`,
   `content writing` — not folders or repositories, which question 4 asks for. **If you have not
   decided this yet, say so and say what would settle it; that is a complete answer.** If something
   adjacent is commonly assumed to be inside and is not, name it. That part is optional.

3. **Principles.** The rules that hold across the whole project. Two are offered:

   - Validate ideas through practical use whenever possible.
   - Avoid speculative additions.

   Keep both, keep one, replace them with your own, or say none.

4. **Components.** Which folders and repositories belong to this project? Name them; this folder is
   not one, it is the project scope. **Naming one now does not set it up now** — it goes in the
   registry as belonging to the project and not yet attached, which is a normal entry, and each one
   is attached later with its own prompt when you are ready. A folder you do not name is files inside
   whichever component contains it. None is a complete answer.

---

## What changed, and why each change

**Question 1 is his wording, not mine.** *"What is this project about? What business does it
represent, or what business tasks does it solve?"* The clause asking whether the project is only
software is gone. **It was an instruction to enumerate, and he enumerated.** The fact it was fishing
for is still needed — the cold start check asks whether the document answers it, and `0004` lists it
among the things a document carries — but it is **derivable from a description of a business**, which
makes it a proposal rather than a question by this framework's own razor. Moved to the assistant
note.

**Question 4 says that naming is not attaching, and this is the substantive fix.** His answers to
questions 2 and 4 were swapped: he gave the folder list at question 2, and at question 4 he wrote
*"I have a few but I will connect them later, not ready now."*

**The cause is one word.** *"Which folders do you declare as components"* reads as a commitment to
wire them now — stubs written, blocks added, work done today. He was not ready for that, so he
skipped it, and the list came out at the previous question instead.

**The registry does not work that way.** A component sits in it unattached quite normally;
`new-project.md` already requires the setup to end by listing exactly those and naming
`new-component.md` as the next step. **The question never said so**, so a person reading it had no
way to know that naming a folder costs nothing today. Now it says so. "Declare" is gone with it, and
"repositories" is added because that is the word he used for two of the three things he named.

**Question 2 says what the line is for, and that is the substantive change here.** It said how to
write the line, what shape it takes, that folders belong to question 4, and that undecided is allowed
— **and nothing about why a person is being asked.** A reframe was tried in conversation and rejected
by the answer it produced: asked *"what kinds of work should an assistant not start without asking
you?"* the owner answered *"do not touch core files in the platform repository"*, which is the
`Repository` posture's travelling rule and already lives in the registry block. **The reframe pulled a
component-level rule up into the project-level boundary**, the folder-list collision one layer over.

Told instead that the line is what an assistant quotes when it declines work, he produced a complete
boundary in a breath. **He was not missing an answer; he was missing what the line is for.** By `0004`
a purpose is exactly what no amount of looking at the folder reveals.

**It was not paid for, and I claimed it was.** Two clauses were trimmed to make room, which is why the
purpose clause cost six words rather than twenty. But the claim that the question is no longer than
the version he read is **false**, and measurement caught it:

| | v0.12.0, the version he read | v3 now |
| --- | --- | --- |
| Q1 what it is | 23 | 21 |
| **Q2 boundary** | **63** | **94** |
| Q3 principles | 37 | 37 |
| **Q4 components** | **52** | **83** |
| **whole block** | **175** | **235** |

**Q2 is up 49% and the block is up 34%**, in the one thing this sequence has spent three days
cutting. Q4's growth is the naming-is-not-attaching sentence and Q2's is the undecided clause, the
kinds-of-work sharpening and now the purpose clause.

Every one of those additions has a reason and two of them came from watching him fail to answer. That
is exactly the shape the backlog's closing finding describes: **every repair correct, and the sum
larger than the thing anybody agreed to.** Stated here rather than discovered later, and it is a
question for the owner rather than something to fix by trimming again.

The evidence for the purpose clause is one person on one occasion and the only measure is his
acceptance test.

**Question 2 surfaces the undecided option.** The blueprint has always allowed *not decided yet*, and
asks for what would settle it and what to do meanwhile — **but that lives in a comment the assistant
reads, not in the sentence the person answers.** A person who has settled his places and not his work
boundary was left reaching for the nearest thing that looked like an answer, which is exactly what
happened.

**The boundary stays about kinds of work**, and the reason is the only measured result on this line:
an assistant refused to build a staging deployment because the document said the project does not
cover hosting and deployment. **Hosting is not a folder.** A boundary made of places could not have
produced that refusal, and it is the single most evidenced behaviour in this repository. His own
first answer named marketing and SEO, which are not folders and are his project — so the project has
non-folder work; he simply does not think of it under the word *scope*.

**The examples are shortened and un-paired.** Three short ones rather than two full sentences joined
by *or*, because the pair was being copied whole. See the finding in the backlog.
