# The Interview

**Blueprint Version:** 0.11.0  
**Framework Version:** 0.11.0

The questions a person is asked when a project scope is set up. `procedure.md` Step 4 sends you here.

They are here as text rather than as topics because a topic list is a prediction about whoever
renders it. The same five topics, under one harness four days apart, produced an interview an owner
accepted and one he refused. `../checks/` ships prompts for the same reason.

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
   path is already settled and I will show it in the summary table.

6. **Components.** Which folders do you declare as components? A component is a folder belonging to
   this project, code or material; this folder is not one, it is the project scope. Name each one. A
   folder you do not name is files inside whichever component contains it. None is a complete answer.

---
