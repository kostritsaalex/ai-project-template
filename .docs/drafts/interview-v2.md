# Draft: the interview after the per-question razor audit

**Draft, 2026-08-29. Not in `blueprints/`, and `blueprints/` is held until the ArtGlina adoption has
finished.** Subject of
[`../predictions/interview-after-the-audit.md`](../predictions/interview-after-the-audit.md).

Four questions, down from seven. Questions 1 and 5 of `0.11.0` become proposals; question 7 goes with
[its razor case](../backlog.md).

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

---

## The questions

1. **What it is.** A few sentences. Say whether the project is only software, or whether software is
   one part of something larger.

2. **Boundary.** Finish this sentence: *"This project currently covers ______. Anything else is
   outside it."* Name **kinds of work** — for example `restoration, photography and selling online`,
   or `hosting and deployment, content writing, SEO`. Where the work happens is the registry's job,
   not this sentence's. If something adjacent is commonly assumed to be inside and is not, name it.
   That part is optional.

3. **Principles.** The rules that hold across the whole project. Two are offered:

   - Validate ideas through practical use whenever possible.
   - Avoid speculative additions.

   Keep both, keep one, replace them with your own, or say none.

4. **Components.** Which folders do you declare as components? A component is a folder belonging to
   this project, code or material; this folder is not one, it is the project scope. Name each one. A
   folder you do not name is files inside whichever component contains it. None is a complete answer.

---

## What changed and why, per question

**Question 1 of `0.11.0`, the name → a proposal.** The folder name is visible in Step 2, and the
blueprint already says the name keeps its spaces and the folder need not match, so it was never a
settled value. **This is the one change in the batch justified by the razor and not by a run**, and
it cannot be otherwise: nothing in a scratch scope can observe an owner correcting a proposed name.
Recorded as such in the backlog so the measured changes do not lend it their credibility.

**Question 5, the address → a proposal with a named fallback, and the branches are unequal.**
Measured against three real scopes: the synced-store rule reproduces WordPress 7's hand-written
`OneDrive, Projects/Development/WordPress-7` exactly, and computes ArtGlina's correctly. The
git-remote rule failed on form, once, on this repository — the remote is
`git@github.com:kostritsaalex/ai-project-template.git` and the document carries
`https://github.com/kostritsaalex/ai-project-template`. **An SSH remote satisfies none of `0007`'s
four forms**, so the rule requires normalisation and asks when normalisation fails, rather than
writing a form `structure-check` 11 would reject.

**Question 3, the boundary → an example of kinds of work.** It was eliciting folder lists and
colliding with the components question. The cause is in git: `0.10.0` changed the worked example from
`hosting and deployment, mobile applications, accounting` to `the main folder and the
northwind-storefront repository`, three kinds of work becoming two places, and every adoption since
followed the example rather than the rule. **The merge the owner asked about is deliberately not
made:** the registry lists places and the boundary names kinds of work, so merging would ratify the
collision rather than remove it. The merge stays available if duplication survives this reword.

**Question 7, the document owner → cut with its razor case**, which was already open.

**Questions 2, 4 and 6 of `0.11.0` are unchanged** and become 1, 3 and 4. They are in nobody's
folder. Components is protected by `0005`: being a component is a decision written into the registry,
never a property of what is on disk, so no survey can propose it.

## The floor

Four is a stated floor, not a coincidence. What remains is exactly what lives only in the owner's
head, which is what `0004` said a document carries. The claim and its falsifiers are in the backlog.
