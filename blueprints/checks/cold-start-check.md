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

**The tool you actually use.** Different tools discover different files. A result from one says
little about another, so test the one your work happens in.

**Sources named.** Every answer has to say which file it came from. An answer with no source is a
guess, however plausible it reads.

---

## Prompt

```text
Answer the questions below about the folder you have open.

Use only what you find in the files. For each answer, name the file it came from and quote the
line. If the files do not tell you, answer "not stated here" instead of guessing or answering from
general knowledge.

1. Which project is this folder part of?
2. Where is that project's canonical project-wide documentation? Give the address exactly as
   written.
3. Name one task you would carry out here without consulting that documentation, and one you would
   not start without it.
4. Suppose that documentation is unreachable. What do you do?
5. Which single file here is the one to read first, and what made you pick it?

Answer the five questions and stop. No summary.
```

---

## Reading the answers

| Question | What a working chain looks like | What a break looks like |
| --- | --- | --- |
| 1 | Names the project, cites the entry point. | "Not stated here", or a name inferred from the folder name. |
| 2 | Repeats the URL exactly. | Knows a parent exists, cannot say where. This is the failure the address rule exists to prevent. |
| 3 | Two concrete tasks that match the boundary in the document. | Vague answers, or claims project context is needed for everything. |
| 4 | Asks for access or for the missing context. | Offers to proceed on reasonable assumptions. |
| 5 | Names the canonical entry point and explains it arrived there through `AGENTS.md` or `CLAUDE.md`. | Names `README.md`, or lists everything it read without a first step. |

Question 4 is the one that fails most often, and the failure is easy to miss because the answer
sounds cooperative. An assistant that offers to fill the gaps itself will do exactly that, quietly,
on a real task.

---

## A second tool

The conditions call for the tool you actually work in. Running the same prompt in a tool from a
different vendor is a separate check, and a stronger one, at the cost of a single session.

The adapters exist because different tools look for different filenames. One reads `CLAUDE.md`,
another reads `AGENTS.md`, and a run in one tool only proves the file that tool happened to open. A
second tool that lands on the other adapter and still arrives at the entry point is evidence the
pair works, rather than the assumption that it does.

Question 5 is where this shows. If both runs cite the same adapter, the other one is still untested.

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
