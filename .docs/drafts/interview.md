# Draft: the project scope interview, shipped as text

**Draft, 2026-08-30. Not in `blueprints/`. Nothing is released on the strength of this file.**

It exists to be the subject of
[`../predictions/does-a-shipped-script-stay-shipped.md`](../predictions/does-a-shipped-script-stay-shipped.md).
If the runs show a tool decorates it the way it decorated five topics, the proposal fails and this
file is deleted rather than repaired.

---

## For the assistant. Not shown to the person.

Ask the six questions below **verbatim and in order, in one message.** Do not introduce them, gloss
them, add clarifications, or add questions of your own. If something is missing from them, that is a
defect in this file and it is reported afterwards, not patched in the message.

Everything else is settled by proposal and shown in the summary table, where one sentence overturns
it: the local path in the form you resolved, the path note and the command that recreates it, each
component's posture, whether an override already exists, the document owner, and the session note
once the components are known.

---

## The questions

1. **Name.** What is this project called? It keeps its spaces, and the folder need not match.

2. **What it is.** A few sentences. Say whether the project is only software, or whether software is
   one part of something larger.

3. **Boundary.** Finish this sentence: *"This project currently covers ______. Anything else is
   outside it."* If something adjacent is commonly assumed to be inside and is not, name it. That
   part is optional.

4. **Principles.** The rules that hold across the whole project. Two are offered:

   - Validate ideas through practical use whenever possible.
   - Avoid speculative additions.

   Keep both, keep one, replace them with your own, or say none.

5. **Address.** Where does this project live, written so that it resolves from another machine? A
   repository URL, or a location in a synced store such as `OneDrive, Projects/northwind`. Your local
   path is already settled and is in the table below.

6. **Components.** Which folders do you declare as components? A component is a folder belonging to
   this project, code or material; this folder is not one, it is the project scope. Name each one. A
   folder you do not name is files inside whichever component contains it. None is a complete answer.

---

## Why six and not seven, since seven is what the runs produced

Seven questions appeared in all four runs of
[`interview-length-0.7-against-head.md`](../predictions/interview-length-0.7-against-head.md) and in
the refused ArtGlina interview. Fighting that number needs a reason, and the logs give one.

Six of the seven are stable across every run: name, what it is, boundary, principles, address,
components. **The seventh is different every time, and three of the four were things the framework
says not to ask.**

- `a1` asked whether `.docs/` exists, while stating in the same sentence that it does not. Step 4:
  *"A question about something you can read. Read it."*
- `a2` asked for the local path, having just resolved and proposed it.
- `b2` asked for each component's posture. Step 4: *"The posture is not one of them."*
- `b1` asked whether a component already has a rule of its own. Legitimate, and it belongs to
  `new-component.md`: an override is written when a component is attached, not while the scope is
  being set up.

So the seventh slot is not a seventh topic. **It is the slot an unspecified interview fills with
whatever it invented that run**, and in three runs of four it filled it with a question the framework
had already forbidden. Six is the number of questions the five topics actually contain; seven is the
number an unspecified interview produces.

## Where the wording had to earn itself

The two largest questions in every run were components and where-it-lives, so those are the two this
draft cuts hardest and the two most likely to be found insufficient.

**Address, question 5.** Arm B spent 124 words on it because it asked for the address *and* the local
path, then explained the difference. The local path is visible — the procedure resolves it in Step 2 —
so only the address is a question. That is the first razor applied to a question rather than to a
document, and it removes about eighty words.

**Components, question 6.** Cut to three sentences, and one of them is kept against the pressure to
cut it. *"This folder is not one, it is the project scope"* is in `new-project.md` as a measured
finding: without it the person counts the project folder as component one and corrects themselves
mid-block. It survives because a run showed it changes what the person does, which is `0008`'s test
applied to a sentence addressed to a person.

**What is deliberately absent.** No reason is given for any question. Not why the boundary is written
as an inclusion, not what "currently" records, not that the complement of a project is endless. All of
that is true, all of it is in `PROJECT.md`'s comments where the assistant reads it, and none of it
changes the answer a person gives. That is the whole proposal in one line: **the blueprint explains
to the assistant, and the assistant asks the person short questions.**
