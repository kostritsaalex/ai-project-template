# Pre-registration: do six answers and three proposals fill twelve placeholders?

**Written 2026-08-29, before the run, after `0.11.0` was committed and verified and before it was
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

---

# Result, scored 2026-08-29, before the tag

Logs: `2026-08-29-placeholder-coverage-{1,2}.log`.

**O1 holds.** Both runs produced the Step 5 summary table with a row for every placeholder. Both also
added rows the map did not predict and which are correct: a visible line for components listed but
not attached, and one for `.docs/` not existing yet.

**O3 holds.** No placeholder other than `<DOCUMENT_OWNER>` came out unsourced. Run 1 marked
`<PROJECT_LOCAL_PATH>` **unknown** and said why — the OneDrive path in the answer does not exist and
the folder it was sent to is elsewhere — which is the procedure's Step 6 rule working, not a gap.

**O4 holds.** Scope checksum `cfe0628965b1cb30db3af0bff174dee0`, unchanged.

**O2 is (b), and the route matters more than the verdict.**

Both runs wrote `Alex`. **They sourced it differently:**

| run | value | source given |
| --- | --- | --- |
| 1 | Alex | "proposed from your account identity" |
| 2 | Alex | "my proposal, from the framework's own `PROJECT.md`" |

Run 2 read the **framework's own** `Document Owner` and copied it into a different project's
document. **That route writes `Alex` into the `PROJECT.md` of anybody who adopts this framework.** It
produced the right answer here only because the adopter and the framework's owner are the same
person — which is the condition the `1.0` criteria in the `README` already name as the thing that has
never been tested.

The pre-registration named a differing source as the deciding outcome before the runs, so this is
(b) by the rule written in advance and not by a reading chosen afterwards.

## What was done

`interview.md` gains **question 7: "Document owner. Whose name goes on the `Document Owner` line?"**
Seven questions, 217 words. The claim that the owner is settled by proposal is removed from the
assistant note, because it was never true.

`0013`'s six-not-seven paragraph gains the exception, with this run as its evidence.

**The released text was run again**, `2026-08-29-released-interview-text-seven.log`: **0 added words,
similarity 1.000, seven questions**, scope unchanged. That is six runs of the mechanism with zero
added prose, and it keeps the rule that the shipped bytes are run bytes.

## The general rule this leaves, and it is worth more than the question

**A proposal earns its place only if the assistant note names where it comes from.** The other three
proposals name their sources — the local path from Step 2's resolution, the path note from the
arrangement holding it up, the session note from the components. `<DOCUMENT_OWNER>` was listed among
them with no source named, and that unnamed source is exactly where the defect was.

This is the cheapest slice of the sufficiency test and the only part that needed no adoption. It
found a real defect in a released tree before it was tagged, for the price of two runs.

---

# Re-run against the four-question interview, pre-registered 2026-08-30 before the `0.12.0` tag

`0.12.0` cuts three questions and `<DOCUMENT_OWNER>` with them. **The map has to be re-derived, not
assumed**, because this check is what found the last gap and the question set has changed twice
since.

The map as it now stands, eleven placeholders:

| Source | Placeholders |
| --- | --- |
| **question** (4) | `<PROJECT_PURPOSE>` `<SCOPE_COVERS>` `<PROJECT_PRINCIPLES>` `<COMPONENTS>` |
| **proposal** (5) | `<PROJECT_NAME>` `<PROJECT_SCOPE_ADDRESS>` `<PROJECT_LOCAL_PATH>` `<PATH_NOTE>` `<SESSION_NOTE>` |
| **read** (2) | `<PROJECT_BLUEPRINT_VERSION>` `<YYYY-MM-DD>` |

**T1.** Two runs, answers supplied, reach Step 5 and fill every one of the eleven. **Any placeholder
without a source is the `<DOCUMENT_OWNER>` finding again**, and the response is the same: it becomes
a question or a proposal with a named source, and the release does not go out as drafted.

**T2.** No run asks for a document owner, or writes one into the header. The line is gone from the
blueprint; a run that reinstates it is a finding, not a courtesy.

**T3.** One further run of the released text with writing disabled: **0 added prose, four questions**,
keeping the rule that the shipped bytes are run bytes.

**T4.** Nothing written into the scope.

## Result of the `0.12.0` re-run, scored 2026-08-30

**T1 holds.** Both runs produced a Step 5 table covering **all eleven** placeholders, including
`<YYYY-MM-DD>` as `2026-08-30`, sourced "Today". No placeholder came out without a source, so the
`<DOCUMENT_OWNER>` shape did not recur under four questions.

**T2 holds.** Zero mentions of a document owner across all three runs. Neither run asked for one nor
reinstated the header line.

**T3 holds.** 0 added prose, similarity 1.000, four questions.

**T4 holds.** Scope checksum `0c00b4979692efee7e4015ef5f54227e` unchanged.

Eleven runs of the mechanism now carry zero added prose, across four subjects and five scopes.
