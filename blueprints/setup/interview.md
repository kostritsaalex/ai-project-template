# The Interview

**Blueprint Version:** 0.13.0  
**Framework Version:** 0.13.0

The questions a person is asked when a project scope is set up. `procedure.md` Step 4 sends you
here.

They are text rather than topics because a topic list is a prediction about whoever renders it.
What is not here is anything an assistant standing in the folder could propose: each of those is
listed below with the source it comes from, and a proposal with no named source is not one.

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
  - If neither rule fires, there is no copy of this folder off this machine and nothing to derive.
    **`0007`'s fourth form is not available here.** It belongs to a component block in a registry,
    and a project scope is what every component's stubs point at, so its address is the one that has
    to resolve. Never a blank either, and never a local path in the address slot. Ask instead, in
    these words or in words that keep every part of them:

    > This folder has no address yet, and a project needs one before I can set it up. Every folder
    > you later add to this project keeps its own copy of this address, and that copy is how anyone
    > working in one of those folders finds their way back here. So it has to be something that
    > works from a different machine, rather than a path on this one.
    >
    > Two things count. A git remote you have pushed to, which gives an address like
    > `https://github.com/you/northwind`. Or a folder inside a synced store — OneDrive, Google
    > Drive, Dropbox — which gives one like `OneDrive, Projects/northwind`.
    >
    > `git init` on its own does not count. It gives this folder a history and leaves it in exactly
    > one place, and what is being asked for is a second place.
    >
    > Set one of those up, or move the folder into one, and tell me when it is done. I will read the
    > address from the folder rather than from your description. Until then there is nothing I can
    > write, so setup stops here.

    Then stop, and write nothing. This is the one value that ends the setup rather than reaching the
    summary table as unknown.
- **The local path**, in the form you resolved in Step 2.
- **The path note**, naming the arrangement that makes that path true and the command that recreates
  it.
- **Each component's posture**, from whether the folder holds code a platform updates wholesale.
- **Whether an override already exists**, from the folder.
- **The session note**, once the components are known.

**Answer 1 has to tell you whether software is all of this project or one part of it.** Question 1 no
longer asks that outright: a person describing his business answers it without being asked, and asking
made one owner enumerate instead. Derive it and write it into `<PROJECT_PURPOSE>`. If a business
description genuinely leaves it open, that is the one thing worth a follow-up.

**Answer 2 may be "nothing", and that is a complete answer.** Write it as visible text — that no work
is currently forbidden, and that an assistant meeting something which looks outside the project asks
before starting it. **Never delete the section**, which reads as correct to every check.

---

## The questions

1. **What it is.** What is this project about? What business does it represent, or what business
   tasks does it solve?

2. **Agent boundaries.** Is there anything an agent should never do in this project? For example:
   never set up deployment, never spend money on my behalf, never publish anything publicly. **If
   there is nothing, say so** — that is a complete answer and I will write it down as such.

3. **Principles.** The rules that hold across the whole project. Two are offered:

   - Validate ideas through practical use whenever possible.
   - Avoid speculative additions.

   Keep both, keep one, replace them with your own, or say none.

4. **Components.** Which additional folders and repositories belong to this project? Main project
   directory doesn't count. Naming one now does not set it up now — each is attached later with its
   own prompt, when you are ready.

---
