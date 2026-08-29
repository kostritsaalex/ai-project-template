# Prediction: check 4 names which line it compares against

**Written:** 2026-08-29, before the run.  
**Subject:** `registry-check.md` check 4, rewritten to settle which comparison it asks for.

## Why

Across five logs, row 4 for `WP Themes` — an unchanged component, a passing row every time — cited a
different comparand almost every run:

```text
run4-shipped             line 39 and line 45
run4-shipped-repeat      line 39 alone
run5-unreachable         line 45 alone
run5-unreachable-repeat  line 45 alone
run6-cut-clause          line 45 alone
```

This is not the wording variance found on rows 2 to 6, where one fact was stated in different words.
Here a different comparison is performed. Line 39 is the synced-store `Address:`; line 45 is a local
path. A resolved `../` is a filesystem path, so as a location it can only meet line 45; line 39 does
not resolve at all. The row said "the address `PROJECT.md` gives for itself under where the project
lives", which names both, and let the tool choose.

`run4-shipped-repeat` shows what choosing costs. Its evidence resolves `../` to this folder, "whose
own address is `PROJECT.md` line 39: OneDrive, Projects/Development/WordPress-7". That is not a
comparison. It asserts this folder is that address with nothing behind it, which is this check's own
"no evidence" case wearing a quote.

## The change: two questions, not two ways of asking one

- **A relative address** resolves from the component's folder and must land on the folder the check
  runs in. Compared against **that folder and no line of text.** The local path line is explicitly
  not the comparand: it is a hint, and a verdict resting on a hint is not evidence.
- **Any other address** is compared as text against the **`Address:` line**, character for character.
  Named as that line, not the local path beneath it.

## The run

Same scope, **no plant**: both components correct. The scope is discriminating as it stands, because
`WP Themes` carries `../` and the Engine carries the synced-store address verbatim, so one component
exercises each branch.

## Predicted

| Row | Component | Verdict | The evidence must cite |
| --- | --- | --- | --- |
| 4 | WP Themes | pass | Both stub lines 11, the path `../` resolved to, and that it is this folder. **Neither line 39 nor line 45.** |
| 4 | Engine | pass | Both stub lines 12, and `PROJECT.md` line 39, matched as text. **Not line 45.** |

Everything else as in a clean positive run: all other `WP Themes` rows pass or n/a, all Engine rows
pass, check 7 lists three folders, `Failed rows: 0`.

## What would falsify it

- **`WP Themes` row 4 citing line 45 or line 39.** The row now forbids both for a relative address.
  Either citation means the rewrite did not remove the choice.
- **The Engine's row 4 citing line 45.** Its address is a string comparison and the local path is not
  the comparand.
- **Either row failing.** Nothing about this scope changed; a failure would mean the rewrite made the
  row stricter than the documents it audits.

## Re-run rule

Any row disagreeing with this prediction gets the arm run again before anything is concluded. And
because the defect being fixed is *variance in the comparand*, a single agreeing run is weak evidence
by construction: this arm is run twice regardless of whether the first run agrees.

---

# Outcome

**Run:** 2026-08-29, twice, no plant. **Every prediction confirmed on both runs.**

`WP Themes` row 4 passed citing both stub lines 11, the path `../` resolved to, and that it is this
folder. **It cited neither line 39 nor line 45**, in either run. The Engine's row 4 passed citing both
stub lines 12 and `PROJECT.md` line 39, compared character for character, **and not line 45**, in
either run. `Failed rows: 0` both times.

Across the two runs, line 39 appears in row 4 exactly once each — the Engine's — and line 45 appears
in row 4 not at all. Under the old wording, five logs had produced three different comparands for one
unchanged component.

**None of the three falsifiers fired.** No relative-address row cited a line of text, no
string-comparison row reached for the local path, and neither row failed on a scope nothing had
changed.

This is a stronger result than a stable verdict: the verdicts were never the problem. Row 4 passed in
all five earlier logs too, while doing a different thing each time. What was fixed is the row asking
one question, and what the runs show is the same question being answered twice.
