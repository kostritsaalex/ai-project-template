# Setup Procedure

The shared procedure behind both setup prompts. Addressed to the assistant, not to the person
running it.

You arrive here from `new-project.md` or `new-component.md`. That file says what is being set up and
carries what is specific to it.

---

## The rule the whole setup follows

**A document carries what cannot be seen, and nothing that can.**

You can open the folder and look. The platform, the local URL, the file layout, whether a `.git`
exists, what the folder holds: all visible, none of it goes in a document and none of it is worth a
question.

What the documents carry is what no amount of looking reveals. Where the parent is. What the project
covers, and that anything else is outside it. The owner's principles. The registry of components that
do not know about each other, and the one word in each block that says how that folder is to be
treated.

So the interview is short by construction. If you find yourself asking about something you could have
read, stop and read it.

---

## Step 1. Access

The prompt that sent you here carries an address for the framework and for each folder involved.
Confirm you can reach all of them and name whichever you cannot.

If the framework is unreachable, stop and ask for a location you can read. Never reconstruct a
blueprint from memory. A component scope needs its project scope to exist already, because it copies
an address from it; if it does not, say which prompt to run first.

---

## Step 2. Look

Before asking anything, establish six things and report them in one short list.

1. Whether `PROJECT.md` is already here. A folder holding one is a project scope, not a component.
2. If it is here and you were sent to attach a component, stop. A folder root holds one entry point;
   two make the stubs ambiguous. Present the choice and let the person settle it: either the contents
   move into a subfolder and the root stays the project scope, or the component is created elsewhere.
3. Whether other AI instruction files are present, of this framework or another. Show them before
   overwriting anything.
4. Whether the folder already claims a parent, and whether that claim matches the one you were given.
5. Whether the local path you intend to write actually resolves, **in the exact form you intend to
   write it**. `~/OneDrive/Projects/x` and `/mnt/c/Users/name/OneDrive/Projects/x` may be the same
   folder or may not, and only one of them goes in the document. Resolve the one that does. If it
   resolves only because of a symlink or a mount, name that arrangement and the command that creates
   it: it is invisible on a machine that lacks it, and without it the path in the document is simply
   false there. If it does not resolve at all, say so and do not write it.
6. For a component only: whether the folder holds code belonging to a platform or framework, the
   kind an updater replaces wholesale. One line, yes or no. It is the only thing you need in order
   to propose the posture, and it is the only reason to look at the contents at all.

That is all. Do not survey the contents to describe them; nothing in these documents describes
contents. Do not survey them for components either. A folder is a component because somebody says so,
never because you noticed it, and a list of candidates you assembled from the tree turns into
questions the person has no reason to answer.

---

## Step 3. Read the blueprint

Read `blueprints/<scope>/README.md` and the blueprint file itself, comments included. Build your
questions from what you read there, not from a list you remember. Say in one line which file and
which version you read.

---

## Step 4. Ask

Ask the seven questions in [`interview.md`](interview.md) **verbatim and in order, in one message.**
Do not introduce them, gloss them, add clarifications, or add questions of your own. If something is
missing from them, that is a defect in that file and it is reported after the interview rather than
patched into the message.

The posture is not a question. Whether platform or framework code sits in the folder is visible, so
propose the posture from what you saw, put it in the summary table as settled, and let it be
overturned there.

Take the answer to question 6 as complete. A folder the person did not name is files inside whichever
component contains it, and it takes that component's posture. Do not offer a subfolder you noticed as
a candidate, and do not ask whether a component should be split into smaller ones.

`Local rules` and `Hazards` are allowed to come out empty. Empty is the usual answer, and the
sections are deleted when they do. Do not fish for content to put in them.

**This holds for a project scope. `new-component.md` still runs an interview of its own, from topics
rather than from text, and it is unspecified in exactly the way Step 4 used to be.** That asymmetry
is deliberate and is recorded in
[decision 0013](../../.docs/decisions/0013-the-interview-ships-as-text.md).

---

## Step 5. Summary

One table before writing anything: placeholder, the value you will write, and where it came from,
which is the person's answer, your proposal accepted, settled from a source you name, or unknown.

Name the source on every settled row so any of them can be overturned in a sentence. Wait for
confirmation.

---

## Step 6. Write

Follow the adoption steps in the blueprint's README. These hold for every scope:

- If a file you are about to write exists, show what is there and ask before overwriting.
- Delete the blueprint notice and every HTML comment, whether it asked for a replacement or said to
  keep something.
- Delete sections the answers emptied.
- State absence in visible text. A comment vanishes from the rendered document and reads as an
  unfinished task to the next assistant.
- Do not write a path you have not resolved, and do not silently substitute a different form of it
  for the one you resolved.
- Do not copy the blueprint's `README.md` or this file into the target.
- A component's two stubs say who the folder is and where the parent is, and stop. A rule written
  into one of them is a rule in a second place, and the parent registry is the first.
- Change nothing outside the folders named in the prompt, apart from the registry entry below.

---

## Step 7. Wire the component

Skip this for a project scope, which has no parent.

A component is attached when both halves are written, and writing one without the other is worse
than writing neither.

**Downward,** into the component: the two stubs. They name the component and carry the parent's
address, copied from the parent's own text rather than retyped.

**Upward,** into the parent registry: one block. The heading is the component's name and has to match
the stubs exactly, because that match is how an assistant standing in the folder finds the block
that describes it. Then the posture, then the address, then the local path.

    ## Northwind Brand Assets

    Assets. Live material. Work here as the task requires.
    Address: assets/brand

The two addresses point opposite ways and are different values. The registry says where the
component is, read from the parent. The stubs say where the parent is, read from the component. For a
component nested inside the project folder that is `wp-themes/` in the registry and `../` in the
stubs. Writing `../` in the registry sends a reader out of the project.

Check whether a block for this component already exists before adding a second one.

**Then check the parent's session note, because attaching may have invalidated it.** That note says
where to start a session so every component resolves, and it was written against the components that
existed at the time. A scope set up with none has no note at all, correctly. Attaching one that sits
on the far side of a mount boundary from the parent makes the note necessary where it was not before.
Add it, or say why it is still unnecessary. Nothing else in the parent changes when a component is
attached, which is why this is easy to miss.

The path note beside it is a different line and does not depend on the components. Leave it alone.

There are no version counters, no `Parent checked`, and no sweep. A component holds no copy of
anything in the parent except the address, so nothing it holds can fall out of date on its own.

The address is the exception, and it is the one edit that reaches every component. When it changes,
walk the registry and rewrite that line in each set of stubs. A stale address passes both checks in
`../checks/` and fails only when somebody follows it.

---

## Step 8. Hand back

Search every file you wrote for `<!--` and for `<` followed by a capital letter. Report both results
even when empty.

Then say which files you wrote or changed, which answers stayed unknown, that the structure check in
`../checks/structure-check.md` should run now, and that the cold start check needs a new session,
because you performed the adoption and your answers would come from this conversation.

Do not run the cold start check yourself.
