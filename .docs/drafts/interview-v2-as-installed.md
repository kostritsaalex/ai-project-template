# The Interview

> **SUPERSEDED IN PART, 2026-09-03.** The third sub-bullet under "The address" instructs `0007`'s
> fourth form for a project scope. That is wrong and `0.18.0` removed it: a project scope's address is
> required, the fourth form is for component blocks only, and where neither derivation rule fires the
> interview asks. See [`../decisions/0023-a-project-scope-address-is-required.md`](../decisions/0023-a-project-scope-address-is-required.md).
> **Do not take wording for the address rules from this file.** It is kept as the record of what was
> drafted on its date, not as a source.
>
> **This note is the only edit ever made to this file, and it is one this file's job argues against.**
> The file records the text *as installed* for a past experiment, so a reader reconstructing that run
> wants it byte-exact. The byte-exact text is every commit of it up to and including `v0.18.0`; the
> note is here because a defective address rule sitting unmarked in a folder a session may draw
> wording from was judged the larger risk.

**Blueprint Version:** 0.12.0  
**Framework Version:** 0.12.0

The questions a person is asked when a project scope is set up. `procedure.md` Step 4 sends you here.

They are here as text rather than as topics because a topic list is a prediction about whoever
renders it. What is not here is anything an assistant standing in the folder could propose.

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
