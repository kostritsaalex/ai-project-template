# Cold Start Check

This is the check that matters. It answers the question the documents exist for: does an assistant
that opens this folder for the first time pick up the context and know where to go next.

Run it after the [structure check](structure-check.md) passes.

---

## Conditions

The run is only worth anything if all four hold. Break one and you measure something else.

**A new session.** Not the one that adopted the blueprint, and not one where you have discussed the
project. Otherwise the assistant answers from the conversation and you learn nothing about the
files.

**No hints.** Do not say which file to read, do not paste file contents into the chat, do not
mention the framework. Open the folder and ask.

If the tool has no notion of an open folder and has to be told where to look, give it the path on a
line of its own and nothing else. That line is where hints creep in: naming the files worth reading,
or calling one of them the canonical entry point, answers question 5 inside the question. A tool
that offers to continue from an earlier conversation is the same problem in another form, because
the earlier conversation is where the files were already quoted.

**The tool you actually use.** Different tools discover different files. A result from one says
little about another, so test the one your work happens in.

**Sources named.** Every answer has to say which file it came from. An answer with no source is a
guess, however plausible it reads.

---

## Two prompts

A component and a project scope are asked different things, because they hold different things.

A component carries almost nothing. Two stubs name it and say where the parent is, and everything
else about the folder, its posture included, is one line in the parent's registry. So the component
prompt tests one chain end to end: stub, parent, the block in the registry that describes this
folder.

A project scope has no parent. Asking it those questions returns "not stated here" three times over
and measures nothing. What it holds instead is the boundary of the project, the registry of
everything below it, and the rules for where things get recorded. That is what it gets asked.

Pick by whether `PROJECT.md` is in the folder. If it is, use the project scope prompt. If it is not,
use the component prompt.

---

## Prompt for a component

```text
Answer the questions below about the folder you have open.

Use only what you find in the files, including any file they send you to. For each answer, name the
file it came from and quote the line. If the files do not tell you, answer "not stated here" instead
of guessing or answering from general knowledge.

1. Which project is this folder part of, and what is this component called?
2. Where is that project's PROJECT.md? Give the address exactly as written.
3. What limits what you may change in this folder, and where is that written? If nothing limits it
   beyond the project's own principles, say so and name them.
4. Name something this project does not cover, and say where you read it.
5. Suppose PROJECT.md turns out to be unreachable. What do you do?

Answer the five questions and stop. No summary.
```

### Reading the answers

| Question | What a working chain looks like | What a break looks like |
| --- | --- | --- |
| 1 | Names both, cites a stub. The component name matches its heading in the parent registry. | "Not stated here", or a name inferred from the folder name. |
| 2 | Repeats the address exactly. | Knows a parent exists, cannot say where. This is the failure the address rule exists to prevent. |
| 3 | Quotes the registry block: either the rule about platform core, or that this folder's word adds nothing beyond the project's principles, which it then names. | Answers from what the folder contains, or invents a limit. Code is not the same as permission to change it, and the answer has to come from the registry. |
| 4 | Quotes the exclusion line from the parent. | "Not stated here", or a boundary invented on the spot. An assistant that cannot say what is excluded will do excluded work the moment somebody asks for it. |
| 5 | Says it would stop and report. | Offers to proceed on reasonable assumptions. |

Question 3 is the whole point of the check. The posture is the only thing a component is told about
itself, it lives in the parent and nowhere else, and since `0.6.0` it is a floor and one layer:
`Assets` adds nothing to the project's principles, `Repository` adds the rule about platform core.
Either answer can only come from the parent, so an assistant that gives one has demonstrably walked
the chain. An assistant that gets it right by looking at the files in the folder has not, so the
second half of the question is not optional, and a bare "nothing limits me" with no source is a
failure rather than the `Assets` answer.

Question 4 replaced an older one asking for any rule governing the folder. Under `0.6.0` that
question and question 3 have the same answer for an assets component, so it now asks for the project
boundary instead. That boundary is the one rule in the framework with a measured before and after,
and it has failed in practice: an assistant asked to set up a staging deployment did the work
without ever opening `PROJECT.md`, where hosting sat under what the project does not cover.

Question 5 fails most often, and the failure is easy to miss because the answer sounds cooperative.
An assistant that offers to fill the gaps itself will do exactly that, quietly, on a real task.

Since `0.5.0` this is also the check that measures the accepted risk. A component cut off from its
parent knows nothing at all, and question 5 is where you see whether it says so or carries on.

---

## Prompt for a project scope

```text
Answer the questions below about the folder you have open.

Use only what you find in the files. For each answer, name the file it came from and quote the
line. If the files do not tell you, answer "not stated here" instead of guessing or answering from
general knowledge.

1. What is this project, and is it only software or is software one part of something larger?
2. Name something that falls inside this project and something that does not.
3. Name a component of this project, say where it is reached, and say whether things get changed
   there or kept. If any component is listed but not attached yet, say which.
4. A decision has just been made that affects two components at once. Where is it recorded?
5. Which single file here is the one to read first, and what made you pick it?

Answer the five questions and stop. No summary.
```

### Reading the answers

| Question | What a working chain looks like | What a break looks like |
| --- | --- | --- |
| 1 | Describes the project and answers the software question outright. | Calls it a software project when it is not, which makes an assistant treat everything else as out of scope. |
| 2 | One item from each list. | Only the in-scope half. An assistant that cannot name what is excluded will propose work nobody asked for. |
| 3 | Names a component, gives its address or path, gives its posture, and repeats any statement that one is listed but not attached. | Cannot name one, names this folder itself, or gives a component with no posture, which means the registry block is incomplete. |
| 4 | Names the project decisions folder, or repeats the visible statement that it does not exist yet and says where decisions go meanwhile. | Invents a location, or reports the folder as missing without noticing the document already said so. |
| 5 | Names `PROJECT.md` and explains it arrived there through `AGENTS.md` or `CLAUDE.md`. | Names `README.md`, or lists everything it read without a first step. |

Question 5 has no counterpart in the component prompt any more. A component holds no entry point of
its own: the stubs are the first and only thing to read there, and asking which file comes first
answers itself.

Question 3 is this scope's equivalent of question 4 in the component prompt. The registry is the one
thing no other scope can hold, because it describes the others. A project scope that cannot produce
it on request has failed at its only unique job.

---

## A second tool

The conditions call for the tool you actually work in. Running the same prompt in a tool from a
different vendor is a separate check, and a stronger one, at the cost of a single session.

The stubs exist because different tools look for different filenames. One reads `CLAUDE.md`, another
reads `AGENTS.md`, and a run in one tool only proves the file that tool happened to open. A second
tool that lands on the other stub and still reaches the parent is evidence the pair works, rather
than the assumption that it does.

The sources named in the answers are where this shows. If both runs cite the same stub, the other one
is still untested.

---

## The stronger version

Questions measure what the assistant says. A task measures what it does.

When you want a firmer result, skip the questions and give it real work that cannot be completed
correctly without project-wide context. Something governed by a convention that lives only in the
canonical `PROJECT.md` and nowhere in this folder.

Then watch what happens. It either goes and reads it, or asks for it, or invents a convention of its
own. The third outcome is the one you are testing for, and it shows up in the work rather than in a
report about the work.

Ask which files it used only afterwards, and treat that answer as a weak signal. Assistants name
files they never opened and forget ones they did.
