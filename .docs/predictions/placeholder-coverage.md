# Pre-registration: do six answers and three proposals fill twelve placeholders?

**Written 2026-08-30, before the run, after `0.11.0` was committed and verified and before it was
tagged.**

---

## Why this exists

Sufficiency is what an adoption tests, and **one slice of it is checkable without an adoption**:
every placeholder in `PROJECT.md` needs a source. `0.11.0`'s five runs all stopped at the questions,
so none of them ever reached Step 5's summary table, and none of them shows whether the six questions
plus the proposals actually cover the document.

The map, by inspection:

| Placeholder | Source | From |
| --- | --- | --- |
| `<PROJECT_NAME>` | question | 1 |
| `<PROJECT_PURPOSE>` | question | 2 |
| `<SCOPE_COVERS>` | question | 3 |
| `<PROJECT_PRINCIPLES>` | question | 4 |
| `<PROJECT_SCOPE_ADDRESS>` | question | 5 |
| `<COMPONENTS>` | question | 6 |
| `<PROJECT_LOCAL_PATH>` | proposal | Step 2, item 5 — resolved |
| `<PATH_NOTE>` | proposal | Step 2, item 5 — the arrangement holding the path up |
| `<SESSION_NOTE>` | proposal | after the components are known |
| `<PROJECT_BLUEPRINT_VERSION>` | read | the blueprint README |
| `<YYYY-MM-DD>` | read | the date |
| **`<DOCUMENT_OWNER>`** | **unestablished** | — |

`<PLACEHOLDER>` is the thirteenth match and is not one: it appears in the blueprint notice, which is
deleted at adoption.

**`<DOCUMENT_OWNER>` is the gap.** No question asks it. `interview.md`'s assistant note lists it
among the things "settled by proposal" — **but names no source for it**, unlike the other three,
which name theirs. The refused ArtGlina interview asked it as question 7. It cannot be seen in an
empty folder.

## The claim under test

That an assistant reaching Step 5 either proposes a document owner **and names where it came from**,
or leaves the placeholder unfilled.

## The run

Two runs, `claude -p`, `--model opus`, fresh session each, writing disabled, against the committed
`0.11.0` tree and scope 1 (`cfe0628965b1cb30db3af0bff174dee0`).

The prompt is the normal paste block **plus answers to the six questions already given**, so the run
proceeds to Step 5 instead of stopping at Step 4. **The answers deliberately contain no name of any
kind**, so anything the run writes into `<DOCUMENT_OWNER>` came from somewhere other than the
conversation. That is the whole design of it.

Two runs and not one, by [`handover.md`](../handover.md): if the run silently omits the owner, the
evidence is an absence, and an absence gets a repeat.

## Predictions

**O1.** Both runs produce the Step 5 summary table with a row for every placeholder above.

**O2.** For `<DOCUMENT_OWNER>`, each run does one of:

- **(a)** proposes a value and names a source outside the conversation — `git config`, the
  environment, the machine's user. Then it is a proposal like the local path, `interview.md`'s note
  gains the source beside the other three, and six questions stand.
- **(b)** marks it unknown, or asks for it, or fills it with something it cannot source. **Then the
  interview is one question short**, `0013`'s six-not-seven paragraph gains its exception, the
  question is added, and the released text is run once more before the tag.

**O3.** No other placeholder comes out unsourced. Any that does is treated exactly as
`<DOCUMENT_OWNER>` above.

**O4.** Nothing is written into the scope; checksum unchanged.

## What decides it

**Outcome (b) in either run** sends the interview to seven questions. A source named in one run and
not the other is (b): a value that appears only sometimes is the variance this whole release exists
to remove.
