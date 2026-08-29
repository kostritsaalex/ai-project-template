# Prediction: the ArtGlina adoption, carrying two changes

**Written:** 2026-08-29, before the adoption session starts.  
**Subject:** the framework at `0.10.0`, adopted from scratch on a real project, blind.

## Two changes on one run, and why they do not confound each other

`0.10.0` changed the boundary question ([`0011`](../decisions/0011-the-boundary-is-a-closed-inclusion.md))
and added two default principles ([`0012`](../decisions/0012-two-default-principles-of-eight.md)).
Both land in this adoption. **This is not an isolated variable and is not claimed as one.**

They are separable because they produce different observables in different parts of the interview.
The boundary shows up as whether the owner answers without the complaint he made last time. The
principles show up as whether he accepts, edits or rejects two sentences he is offered. Neither
outcome can be produced by the other change. What a single run cannot do is tell whether a change
would have worked with the other absent, and nothing here will claim that.

## What is also being tested, without either change

The adoption path itself. `blueprints/project/PROJECT.md` last changed at `0.7.0` and
`setup/procedure.md` at `0.8.0`, while the only from-scratch scope adoption on record was on `0.6.0`.
Both the blueprint and the procedure have moved since the path was last exercised, and now they have
moved again.

## Predicted, boundary

**The owner answers the coverage question in one sentence and does not complain.** He already
supplied the answer unprompted when objecting to the old question — the main folder and two
repositories — so the content is not in doubt; what is being tested is whether the question is
answerable without the getting-lost he described.

*Falsified if* he asks what counts as covered, lists things and then removes them, or produces the
same open-ended difficulty in the new direction. Any of those means the closure did not bound the
question and only moved it.

**A near miss is named or is not, and either is a pass.** It is optional by decision. If he volunteers
one, that is evidence the optional half is worth keeping; if he does not and the boundary still reads
as a rule, that is evidence it is worth keeping optional.

## Predicted, principles

**He keeps both.** They are his own submissions, two of eight, so acceptance is the weak outcome and
proves least.

*The informative outcomes are the other two.* If he **edits** either, the wording shipped is wrong and
the edit says how. If he **rejects** one, a principle that survived the razor by reading fails on
first contact with the person it was written for, which would be the strongest single result available
here and would reopen `0012`.

**Watch for the failure `0012` predicted rather than the verdict.** A default invites acceptance
without thought, and acceptance is what is predicted. So the thing to record is not that he said yes
but **whether he engaged with them at all** — a yes that arrives with a reason, an objection or a
reworded line is engagement; a bare yes to both is the acceptance-without-thought the decision
identified and did not solve. That distinction is registered now because it will be tempting to score
a bare yes as a confirmation.

**Six were cut and he proposed eight.** If he asks for any of the six back, the reason he gives is
worth more than the principle: it is the first outside test of whether reading `0008` onto a rule
matches what its author meant by it.

## Predicted, the adoption itself

**The interview stays short and asks nothing answerable by looking.** `0004`'s razor governs the
procedure, so a question about what a folder contains, what platform anything runs on, or whether a
`.git` exists is a defect in the blueprint rather than a lapse by the session.

**Two questions arrive that the blueprint does not prompt**, and both are the framework's own
unfinished business rather than the interview's. Which working copy the registry's local path should
name, since two folders answer to one repository URL. And whether the `Unsorted` folder is declared a
component at all, which only the owner can settle.

**The session note is not asked in the first block.** It cannot be settled before the components are
named. If it is asked early, the procedure's ordering failed.

## What would make this run worthless rather than negative

**Any sign the session read the withheld record**, the old documents, or `artglina-ua`'s git history.
The blindness rests on an instruction and on a judgement log that sits in the framework repository the
session must open. If the finished documents contain something the interview did not supply, that is
the first thing to check and the run is void, not negative.

## Not scored here

The comparison against the withheld record. That happens with the owner afterwards, and a divergence
is not a mistake. Scoring it before the key is seen would turn it into one.

---

# Amendment, 2026-08-29, before the run

**The principles arm changed. The owner intends to write all eight into ArtGlina's `PROJECT.md`,
overruling the cull for his own project.** Everything above this line was written before the
amendment and is unedited; the prediction it made about the principles is superseded by what follows.

**This is not a breach, and the framework now says so.** `0008` governs what the blueprint *offers*
to every adopted project. It says nothing about what an owner writes in his own `Principles` section,
which is his. Nothing was stating that, and without it a cull reads as a prohibition — so the
blueprint's README now says it outright.

## Why this makes the arm stronger

The original arm asked whether he would keep two sentences he was offered, where acceptance was
predicted and proved least. This one runs the six cut principles in a live project and asks what they
do there. The cull was made by reading; this is the first thing resembling a measurement of it.

## Predicted, and this is the part that matters

**Six of the eight cannot be acted on in a project of photographs, invoices and two WordPress
checkouts. The failure worth watching is not that they are ignored — it is that they are obeyed.**

A principle nobody can act on is inert and costs a line. A principle acted on where it does not
belong changes work, and changes it wrongly.

**One complication, named now rather than after.** ArtGlina is mixed: material and code. Inside the
WordPress components, "understand the current architecture" and "preserve backward compatibility"
have real referents and may earn their place there. The prediction is about the material half and
about the project document that governs both. What makes ArtGlina the right subject is exactly that
it has both halves under one `PROJECT.md`.

## Two pairs to watch, both quotable

**"Identify the affected scope", against the framework's own word.** `scope` is this framework's term
for a project scope or a component, and the sentence sits in the document that carries the components
registry. An assistant reading it as "work out which registered scope this touches" has been sent to
the registry by a principle that meant "work out what you are changing".

**"Preserve backward compatibility where practical", against the `Assets` posture's "work here as the
task requires".** In a folder of material, backward compatibility means not renaming and not moving,
and renaming and reorganising is ordinary work there.

This second pair is sharper than it looks, because it is a rule returning through a different door.
`0006` removed four preserve rules from the `Assets` posture for precisely this reason: an assets
folder is live, a rule written for a museum is broken by ordinary work, and a rule that ordinary work
breaks teaches an assistant the document can be ignored. That was cut at the posture level. A project
principle saying "preserve backward compatibility" puts it back at the project level, where it
outranks the posture.

**What an observation looks like.** Hesitation about renaming a folder of photographs. An assistant
reading "scope" as a project scope. A refusal, or a request for confirmation, on work the posture
plainly permits. Any of those is a principle colliding with a posture, **and nothing in the framework
notices such a collision today** — the registry states the posture, the project document states the
principles, and no check compares them.

## What would falsify it

The six sit inert and change nothing. Then the cull was right about their emptiness and wrong about
the risk, and the entry should say so.

Or one of the six visibly improves work on the material half, which would mean the reading that cut
it was wrong and `0012` reopens.

## The 0008-shaped test, available whenever wanted

One task on ArtGlina with the eight, one with the two, judged by the work. The design is the one that
settled `0008` and it costs two runs. It is not part of this adoption and does not need to be.
