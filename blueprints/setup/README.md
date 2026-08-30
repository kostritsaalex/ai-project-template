# Setup Prompts

**Blueprint Version:** 0.12.0  
**Framework Version:** 0.12.0

Two prompts that adopt a blueprint by interview. Instead of opening each file and working through
its placeholders by hand, you paste one prompt, answer questions in blocks, and get filled files.

They apply to every blueprint, so they live here rather than being repeated in each one. The same
arrangement as [`../checks/`](../checks/), and the two sets are meant to be used together: setup
creates, checks verify.

| Prompt | Sets up | Depends on |
| --- | --- | --- |
| [new-project.md](new-project.md) | A project scope | Nothing |
| [new-component.md](new-component.md) | Any component, code or material | An existing project scope |

[`procedure.md`](procedure.md) holds the shared procedure. You never paste it; both prompts send the
assistant to read it.

[`interview.md`](interview.md) holds the four questions a project scope is asked, as text rather than
as topics, and `procedure.md` Step 4 sends the assistant there. **The component interview is still
built from topics**, which is a known asymmetry recorded in
[decision 0013](../../.docs/decisions/0013-the-interview-ships-as-text.md).

---

## Which one, and in what order

The project scope first, then one run of the component prompt per folder.

There is no separate prompt per kind of component. A repository attached on the first day and a
photography folder attached two years afterwards are the same operation: two stubs in the folder, one
block in the registry. The difference between them is one word in that block, and the assistant
proposes it from what it saw rather than asking.

There is also no separate prompt for adding a component later, and none for a folder that has years
of history behind it. The assistant looks before it asks.

---

## What they do not do

**They do not replace reading the blueprints.** They read them for you, which is not the same thing.
Every question comes from the placeholder table and the comments in the blueprint being adopted, read
at the moment the prompt runs. Nothing about the questions is stored here, so a change to a blueprint
reaches the interview without anyone editing these files.

**They do not know your project.** Every answer written into a file comes from you, and the interview
is short because the documents are: they carry what an assistant cannot see for itself, and nothing
it could find by opening the folder.

**They do not set up an override.** When a component turns out to need rules of its own, the
assistant is told to add `REPOSITORY.md` or `ASSETS.md` from the matching blueprint, but that is a
step inside the component run rather than a prompt of its own.

**They do not verify their own work** beyond a text search for leftover comments and placeholders.
The two prompts in [`../checks/`](../checks/) do that, and the cold start check has to run in a
session that did not perform the adoption.

---

## Before you run one

Each prompt carries addresses, and they are the part you fill in: where the framework is, where the
target folder is, and for a component, where its parent `PROJECT.md` lives. Nothing else in the
pasted text needs editing.

The framework's address takes one of two forms. A path to a local checkout is the reliable one. The
repository URL, `https://github.com/kostritsaalex/ai-project-template`, works only where the
assistant can fetch raw files, and not at all if the copy in use is private.

This is the framework's own rule applied to itself: a reference to another scope carries an address
that resolves from where the reference is read. A prompt naming the framework without saying where it
is asks the assistant to recognize it, and an assistant that has never seen it will invent something
that looks right.

---

## What is not here yet

A prompt for reconciling a project whose folders have been rearranged. It reads what is actually on
disk, compares it against what the documents claim, reports the differences and fixes them with
confirmation. It is a separate job from adoption and it does not regenerate anything: a `PROJECT.md`
holds priorities, boundaries and decisions that exist nowhere else, and rebuilding it from an
interview would keep only what its owner happened to remember that day.
