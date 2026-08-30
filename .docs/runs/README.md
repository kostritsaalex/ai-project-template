# Run logs

Raw output of check runs, committed verbatim and never edited. Formatting, stray wording and all.

They are here because a conclusion that rests on an artefact needs the artefact to still exist. On
2026-08-29 a finding about `registry-check` was disputed against a two-row summary of a table that
actually had three rows, and the row carrying the finding was the one the summary had dropped. It was
settled by opening the raw log and by nothing else. That log was in `/tmp` at the time.

A paraphrase of a run is not the run. If a log and a summary disagree, the log is right.

---

| File | Prompt version | Arm | Scope state | Date |
| --- | --- | --- | --- | --- |
| `2026-08-29-registry-check-1-original.log` | `registry-check.md` as committed in `381b200`, before any repair | First run, as written | `WordPress 7`, believed correct: registry paths repaired earlier the same day, Engine override and its stub lines removed the same day | 2026-08-29 |
| `2026-08-29-registry-check-2-repaired.log` | `registry-check.md` as committed in `49b25dd`, after both repair passes | Second run, repaired prompt | Same scope, unchanged since the first run | 2026-08-29 |
| `2026-08-29-registry-check-2-control.log` | `registry-check.md` as committed in `381b200`, verified byte-identical to the first run's prompt | Second run, control: the original prompt again | Same scope, unchanged since the first run | 2026-08-29 |
| `2026-08-29-registry-check-3-negative.log` | `registry-check.md` as committed in `49b25dd` | Negative half, first run | Same scope with **one line deliberately broken**: the Engine's registry local path set back to `~/wordpress-7`, a folder that does not exist. Restored immediately after, verified byte-identical to the copy taken before planting | 2026-08-29 |
| `2026-08-29-registry-check-3-negative-repeat.log` | `registry-check.md` as committed in `49b25dd` | Negative half, repeat of the same arm | Same broken scope, unchanged between the two runs | 2026-08-29 |
| `2026-08-29-registry-check-4-shipped.log` | `registry-check.md` as shipped in `0.9.0` plus the check 6 rewrite, a text no earlier run had used | Negative half against the shipped text | Same planted defect, restored after | 2026-08-29 |
| `2026-08-29-registry-check-4-shipped-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |
| `2026-08-29-registry-check-5-unreachable.log` | `registry-check.md` at `0.9.1`, row 1's cascade collapsed from three cases to one condition | A component the registry never claimed is on this machine | Engine's address replaced by a repository URL and its local path line deleted; restored after | 2026-08-29 |
| `2026-08-29-registry-check-5-unreachable-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |
| `2026-08-29-registry-check-6-cut-clause.log` | `registry-check.md` at `0.9.2`, differing from the `0.9.1` prompt by exactly the cut restatement clause | The second razor measured on a check: does removing a clause that prescribes nothing change anything | Same plant as run 5, restored after | 2026-08-29 |
| `2026-08-29-registry-check-6-cut-clause-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |
| `2026-08-29-registry-check-7-row4-comparand.log` | `registry-check.md` at `0.9.3`, check 4 rewritten to name which line it compares against | Does the row ask one question | **No plant.** The scope discriminates as it stands: one component carries `../`, the other the synced-store address verbatim | 2026-08-29 |
| `2026-08-29-registry-check-7-row4-comparand-repeat.log` | Same | Repeat of the same arm | Same | 2026-08-29 |
| `2026-08-29-registry-check-8-row4-negative-relative.log` | `registry-check.md` at `0.9.3` | Check 4's negative half, relative branch | **Planted in a component's stubs, not in `PROJECT.md`.** `wp-themes/AGENTS.md` and `CLAUDE.md` line 11, `../` to `../../`, in the scope's own filesystem under OneDrive on the Windows side | 2026-08-29 |
| `2026-08-29-structure-check-1-deleted-override.log` | `structure-check.md` at `0.9.3`, component variant | **First `structure-check` log in this repository.** A deleted override: both `wp-themes` stubs name `REPOSITORY.md`, and no such file exists | Planted in the component's stubs; restored after | 2026-08-29 |
| `2026-08-29-structure-check-1-deleted-override-repeat.log` | Same | Repeat, because row 10's result is an absence | Same | 2026-08-29 |
| `2026-08-29-structure-check-2-row4-positive.log` | `structure-check.md` with row 4 rewritten to name its comparison | Row 4 positive, no plant | `wp-themes` correct | 2026-08-29 |
| `2026-08-29-structure-check-2-row4-positive-repeat.log` | Same | Repeat, a pass being evidence of an absence | Same | 2026-08-29 |
| `2026-08-29-structure-check-2-row4-negative.log` | Same | Row 4 negative | One word changed in `wp-themes/AGENTS.md` only, deliberately not the naming line; restored after | 2026-08-29 |
| `2026-08-29-registry-check-9-deleted-override.log` | `registry-check.md` at `0.9.3` | The same planted folder, seen from the scope | Same | 2026-08-29 |
| `2026-08-29-registry-check-8-row4-negative-string.log` | Same | Check 4's negative half, string branch | **Planted in a component's stubs, not in `PROJECT.md`.** The Engine's `AGENTS.md` and `CLAUDE.md` line 12, one path segment changed, in the WSL filesystem | 2026-08-29 |
| `2026-08-29-interview-length-a1.log` | Framework at `v0.7.0`, from a git worktree at that tag | Arm A, first run | **Not a check run and not a real project.** A scratch scope built for this experiment and deleted after: `storefront/` (astro `package.json`, `src/`, `public/`), `catalogue-photos/2026/` (three empty `.jpg`), `supplier-notes/` (two `.md`). Never written to; tree checksum `47809391e908d576d7fae6d9657e7e31` verified unchanged after all four runs | 2026-08-29 |
| `2026-08-29-interview-length-a2.log` | Same | Arm A, repeat | Same scope, unchanged | 2026-08-29 |
| `2026-08-29-interview-length-b1.log` | Framework at `HEAD` = `7e7f8df`, which is `0.10.2` plus the one-clause `procedure.md` repair `3363d09` | Arm B, first run | Same scope, unchanged | 2026-08-29 |
| `2026-08-29-interview-length-b2.log` | Same | Arm B, repeat | Same scope, unchanged | 2026-08-29 |
| `2026-08-29-shipped-script-bprime1.log` | `HEAD` unmodified | Arm B′, control, first run | **Scope 2**, a second scratch scope: five folders, all material, no code — `archive-2024/`, `archive-2025/`, `glaze-tests/`, `exhibition-prints/`, `client-briefs/`. Path-relative checksum `d24c2a045ebd3e87e47cb0b199472ded`, verified unchanged after all six runs | 2026-08-29 |
| `2026-08-29-shipped-script-bprime2.log` | Same | Arm B′, repeat | Same | 2026-08-29 |
| `2026-08-29-shipped-script-c1.log` | `HEAD` plus `blueprints/setup/interview.md` and Step 4 replaced by a pointer to it | Arm C, the script, first run | **Scope 1**, rebuilt identical to the previous experiment's; path-relative checksum `cfe0628965b1cb30db3af0bff174dee0` | 2026-08-29 |
| `2026-08-29-shipped-script-c2.log` | Same | Arm C, repeat | Same | 2026-08-29 |
| `2026-08-29-shipped-script-d1.log` | Same | Arm D, the script on the other scope, first run | Scope 2 | 2026-08-29 |
| `2026-08-29-shipped-script-d2.log` | Same | Arm D, repeat | Scope 2 | 2026-08-29 |
| `2026-08-29-released-interview-text.log` | **The text this release ships**, `blueprints/setup/interview.md` at `0.11.0`, run against the working tree the release commit contains | Release validation, one run | Scope 1, `cfe0628965b1cb30db3af0bff174dee0`, unchanged | 2026-08-29 |
| `2026-08-29-placeholder-coverage-1.log` | `0.11.0` as committed, six questions | Placeholder coverage, first run. **Answers supplied so the session reaches Step 5**, and deliberately containing no name of any kind | Scope 1, unchanged | 2026-08-29 |
| `2026-08-29-placeholder-coverage-2.log` | Same | Repeat, because a silent omission is an absence | Same | 2026-08-29 |
| `2026-08-29-released-interview-text-seven.log` | **The text this release ships**, `interview.md` at seven questions after the coverage check added one | Release validation, re-run after the interview changed | Same | 2026-08-29 |
| `2026-08-29-audit-e{A1,A2,C1,C2}.log` | `HEAD` at `0.11.0`, seven questions | Arm E, the before | **S-A** a scope inside a simulated synced store; **S-C** five folders of material, no git, no store | 2026-08-29 |
| `2026-08-29-audit-f{A1,A2,B1,B2,C1,C2}.log` | `HEAD` + `interview-v2.md`, four questions | Arm F, stopping at the questions | S-A, S-B a git working copy with an SSH remote only, S-C | 2026-08-29 |
| `2026-08-29-audit-g{A1,A2,B1,B2,C1,C2}.log` | Same | **Arm F with the four answers supplied**, so the session reaches the Step 5 summary table where the address and name are proposed. The first ten runs stopped at Step 4 and measured neither | Same three scopes, all unchanged | 2026-08-29 |
| `2026-08-29-posture-{h,j}{1,2,3}.log` | `HEAD` vs `HEAD` + a sharpened posture rule | Arms H and J | One scratch scope with three declared folders: own source in a git working copy, a WordPress install, and material | 2026-08-29 |
| `2026-08-30-core-rule-invalid-*.log` | Registry block with and without the core rule | **Invalid, kept as evidence.** The scratch `pluggable.php` omitted the `apply_filters` calls real WordPress has, so the filter route did not work and the one arm that edited core was the only one whose work functioned | A WordPress install declared as one component | 2026-08-30 |
| `2026-08-30-core-rule-{with,without}-{3,4}.log` | Same, rebuilt tree | **C2, and not used.** The rebuild made the correct route strictly easier than the core edit, so no arm had reason to touch core and C1 was unreachable | Same | 2026-08-30 |
| `2026-08-30-v12-placeholder-map-{1,2}.log` | `0.12.0` as committed, four questions | The placeholder map re-derived against the cut question set, answers supplied so both reach Step 5 | A three-folder scratch scope, unchanged | 2026-08-30 |
| `2026-08-30-v12-released-text.log` | Same | Fidelity of the released text before the tag | Same | 2026-08-30 |
| `2026-08-30-plugin-rule-{with,without}-{1,2}.log` | Registry block with and without the core rule, third attempt | **The subject moved off core to a third-party plugin**, after two attempts died on core: a hard-coded `m/d/Y` in a plugin exposing no hooks, with the fixture validated by execution before the arms | A WordPress install declared as one component; harness output checked per arm | 2026-08-30 |
| `2026-08-30-v3-{vM1,vT1}.log` | `0.12.0` as shipped | Arm V, the before | S-mixed in a simulated synced store; S-material, five folders, no code | 2026-08-30 |
| `2026-08-30-v3-w{M1,M2,T1,T2}.log` | `HEAD` + `interview-v3.md`, four questions reworded | Arm W, stopping at the questions | Both scopes, unchanged | 2026-08-30 |
| `2026-08-30-v3-a{M1,T1}.log` | Same | Arm W with answers supplied, reaching Step 5 — **the arm that tests whether the software fact survives Q1's cut** | Both scopes, unchanged | 2026-08-30 |
| `2026-08-30-boundaries-interview-x{1,2,3,4}.log` | The agent-boundaries interview, four questions, 146 words | Fidelity | The two scratch scopes | 2026-08-30 |
| `2026-08-30-boundaries-coldstart-populated-y{1,2}.log` | `cold-start-check.md` project prompt, rows repaired for the new form | **The first run of these rows against any document carrying it** | A hand-written scope with three prohibitions — not an adopted project, which is the declared limit | 2026-08-30 |
| `2026-08-30-boundaries-coldstart-empty-z{1,2}.log` | Same | **The empty case**, the branch `0010` warns about: a stated absence a reader can take as permission | A hand-written scope recording no prohibitions and the visible sentence saying so | 2026-08-30 |
| `2026-08-30-registry-check-10-artglina.log` | `registry-check.md` at `0.14.0`, row 2 carrying the declared-not-attached clause | **The change's own subject**: the scope that produced 7 failed rows on `0.13.0` | **`Artglina`, real and unmodified, read-only.** Two components declared, both folders present, neither carrying stubs. Three root files verified byte-identical before and after every run | 2026-08-30 |
| `2026-08-30-registry-check-10-artglina-sandboxed.log` | Same | The same arm, run first, kept because it is a different reading of row 2 | Same scope. The session sandbox refused `ls` outside its own directory, so row 2's evidence is a set of path probes rather than the listing the row asks for. The repeat above granted the two registry-named folders and got the listing | 2026-08-30 |
| `2026-08-30-registry-check-11-missing-folder.log` | Same | **Negative control 1**: a genuinely missing folder must still fail row 1 and cascade with row 1's reason, not the new one | A scratch scope, components as subfolders addressed relatively, `artglina-ua/` deleted. **The visible-text sentence saying neither component is wired was removed**, because it is row 1's own pre-existing exception and would have confounded the control | 2026-08-30 |
| `2026-08-30-registry-check-11-missing-folder-blocked.log` | Same | The same control, run first, kept because its row 1 failed for the wrong reason | The first scratch scope, components outside the session's directory. Row 1 failed on blocked access rather than an observed absence — the right verdict on weaker evidence, which is why the arm was rebuilt | 2026-08-30 |
| `2026-08-30-registry-check-12-stubs-present-defect.log` | Same | **Negative control 2**: the new outcome must not swallow a real defect | The same scratch scope, `artglina-ua/` restored with both stubs written, then the registry heading changed to `Artglina UA Site` so it disagrees with the naming line in those stubs. **One component attached and broken, one declared and not attached, in one table** | 2026-08-30 |
| `2026-08-30-registry-check-13-artglina-one-path.log` | `registry-check.md` at `0.15.0`, the rows that probe a path gaining one declared path, one command | Arm 1, the real scope again after row 7's first true positive | **ArtGlina, real and unmodified, read-only.** Three root files checksummed before and verified byte-identical after | 2026-08-30 |
| `2026-08-30-registry-check-14-plant-undeclared-listing.log` | Same | Negative control, **disclosed plant**: one deliberate extra listing of a folder no registry line names, appended to the pasted text | A scratch copy of the scope, its two component paths pointed at scratch folders, plus one folder the registry does not name. Deleted after | 2026-08-30 |
| `2026-08-30-registry-check-15-nested-declared-path.log` | Same | Negative control, a declared path two levels below an undeclared folder | A scratch copy of the scope, one component's local path pointing at `outer/inner/artglina-ua`. Deleted after | 2026-08-30 |

Fifteen of these ran against the `WordPress 7` scope at `OneDrive, Projects/Development/WordPress-7`, from
inside WSL, with the Engine's folder granted to the session because it sits outside the scope's
filesystem.

**Two of these logs were produced by planting in a component's stubs rather than in `PROJECT.md`.**
Every other plant edited the scope document; the row-4 negative arms edited the thing the registry is
checked against, which is the other side of the comparison. A reader comparing these logs to the
earlier ones would otherwise assume the scope document was the broken thing. The four stub files
across two filesystems were snapshotted with checksums before anything was planted, each arm's pair
restored from that snapshot rather than retyped, and all four verified byte-identical afterwards.

**These files need an override to be committed at all.** A global `*.log` ignore excluded all five
silently on the first attempt, and the commit went through carrying this index and none of the files
it describes. The repository's `.gitignore` now negates it. If a log added later does not appear in
`git status`, that is why, and `git check-ignore -v` on the file will name the rule.

Checksums at commit time, so a later edit is detectable:

```text
e2113e36892734d131400fd0b59da44a  2026-08-30-registry-check-10-artglina-sandboxed.log
bfa733ef63a17551197ddb55006bfe0a  2026-08-30-registry-check-10-artglina.log
ad2b122d36119ded2a04fcf13bf57249  2026-08-30-registry-check-11-missing-folder-blocked.log
5f74dcb4cd2c5ccf136ce608c47ea93f  2026-08-30-registry-check-11-missing-folder.log
bf2f0093f3174c308a64a56bd582f285  2026-08-30-registry-check-12-stubs-present-defect.log
0b7d6c26ddf37a8bcca563bbfbd001da  2026-08-30-registry-check-13-artglina-one-path.log
7528a5f2e0802ee8e752c60a8988cd0c  2026-08-30-registry-check-14-plant-undeclared-listing.log
6ee0d82daaed9c205980fc6c397e76ff  2026-08-30-registry-check-15-nested-declared-path.log
b67b4df0208b0a9461f18e77871858e7  2026-08-29-registry-check-1-original.log
cf722de35201272594e2f9b27cd9a778  2026-08-29-registry-check-2-repaired.log
6bdd042245658a913d25c0aadaf40d8c  2026-08-29-registry-check-2-control.log
f05464775dff20994c5dc5806fdb18f7  2026-08-29-registry-check-3-negative.log
38b7e3e0dfa615069558410b7b817e8d  2026-08-29-registry-check-3-negative-repeat.log
c060bcecf5e18b3ab770524b2bcdba06  2026-08-29-registry-check-4-shipped.log
c889c6f6960f8d82debaa20e393d709e  2026-08-29-registry-check-4-shipped-repeat.log
65b0ddf0ca1b124524710595d7f25b20  2026-08-29-registry-check-5-unreachable.log
605d88261b6ebfd8a79012ffb5f7dc9e  2026-08-29-registry-check-5-unreachable-repeat.log
515cf7ea5dd5a319e77992b38e977581  2026-08-29-registry-check-6-cut-clause.log
d8dd1ebd4b577c9fc1feb8e965684f8b  2026-08-29-registry-check-6-cut-clause-repeat.log
e1588659e9633cd23a01e751ed882ee0  2026-08-29-registry-check-7-row4-comparand.log
11d6e5eadeb66b33f9cfc0d4ab367c6e  2026-08-29-registry-check-7-row4-comparand-repeat.log
43d5cce31488a7574bf09b029e7b79cc  2026-08-29-registry-check-8-row4-negative-relative.log
4c13e40c9817e3ff4e7d20703e1c30c2  2026-08-29-registry-check-8-row4-negative-string.log
4d0eb949757a7e9165333018697010be  2026-08-29-registry-check-9-deleted-override.log
f3bc602e06e2650ab4a21cc7449a352a  2026-08-29-structure-check-1-deleted-override.log
10ee2c1eb867132b3635fda4efe6a974  2026-08-29-structure-check-1-deleted-override-repeat.log
45fa11257420e2f0726c2b12f7f4d7aa  2026-08-29-structure-check-2-row4-positive.log
6b121ec91c4b55d2bcc51b0d6586dfc0  2026-08-29-structure-check-2-row4-positive-repeat.log
c3b8f56af7b03aa64eb4291eecb45889  2026-08-29-structure-check-2-row4-negative.log
ecc4170878cb75d120a0fa9711f21ac6  2026-08-29-interview-length-a1.log
c411a8a2c6f93934360288239c487558  2026-08-29-interview-length-a2.log
80c4c47ded6f9ca5d0b46569bbba7d8b  2026-08-29-interview-length-b1.log
f65aca1671634a46eead89db142bb645  2026-08-29-interview-length-b2.log
cd260974c33fd14e95de3e6eeebe026a  2026-08-29-shipped-script-bprime1.log
1f2908fa4d435b616c0cfd85e17a4a27  2026-08-29-shipped-script-bprime2.log
b446c16cfdf8dc79695e7c6030650590  2026-08-29-shipped-script-c1.log
789986262a49905836d2d62e38d7ee7a  2026-08-29-shipped-script-c2.log
714335b9bf741c81bc97bcb27b09a79d  2026-08-29-shipped-script-d1.log
6e01c0dcb0fe153edd2dbf9b12c10a75  2026-08-29-shipped-script-d2.log
14da8e21cfa27b5284710e627b55685f  2026-08-29-released-interview-text.log
dba6ac2e180fd20ae46205a705618f54  2026-08-29-placeholder-coverage-1.log
ce2c047b684a1c7eca8d5dd55e307a7c  2026-08-29-placeholder-coverage-2.log
85b91316bd29a0427f3da013188300f0  2026-08-29-released-interview-text-seven.log
ce1c0e733179a377917005fcde81da42  2026-08-29-audit-eA1.log
88eb598a73393e1b428c0621cc791006  2026-08-29-audit-eA2.log
33648566b450d7604382c5d2a805c611  2026-08-29-audit-eC1.log
4a0b081b76c335164d18bed85dd10633  2026-08-29-audit-eC2.log
adda830e675cc39ca873e94a08341303  2026-08-29-audit-fA1.log
fd812b7ca9bc909208a343fc66f5e443  2026-08-29-audit-fA2.log
027e4c665110151c40af59752969898c  2026-08-29-audit-fB1.log
13be8ebdbc10045a1570647685fee58c  2026-08-29-audit-fB2.log
0e0896540291a895213e239facbc3ce3  2026-08-29-audit-fC1.log
ce43f280c64347ec52cf1e97eb579b1d  2026-08-29-audit-fC2.log
ece278eb72a0eb18a701aee7dfd60763  2026-08-29-audit-gA1.log
89ec1ccbc9768dfa1c7bbe30f1d611b0  2026-08-29-audit-gA2.log
9ba1bb5274bf68df9fdb89c41f563b34  2026-08-29-audit-gB1.log
f7f21f95191afce1a717676f92975c6c  2026-08-29-audit-gB2.log
6018952ef37b259697417e28a9223248  2026-08-29-audit-gC1.log
575c90b588988546fd68c9600efed285  2026-08-29-audit-gC2.log
84bba65ee2943998bbcc958e575b24c2  2026-08-29-posture-h1.log
971caf04855189ac2e3714c7e70150b7  2026-08-29-posture-h2.log
6d982976c24a6ad0fc49cb0b6d244c68  2026-08-29-posture-h3.log
f4685046f62dca45d85399434fd4e5fd  2026-08-29-posture-j1.log
81b07e11e06ae1b4faccb1d39d71a126  2026-08-29-posture-j2.log
b80119371295571c629f905dc2cf5829  2026-08-29-posture-j3.log
545563a86fe5d76947cafd2724ae7efa  2026-08-30-core-rule-invalid-with-1.log
9356bea6d8936b76b53ff1d58279ac40  2026-08-30-core-rule-invalid-with-2.log
a9f04364dc40026b7ea801066c7659e9  2026-08-30-core-rule-invalid-without-1.log
2dd8a1b9237acd0440087e62cc2c976b  2026-08-30-core-rule-invalid-without-2.log
c8beee442563ad7cd29d074c86c20dd6  2026-08-30-core-rule-with-3.log
584c4be5d240b466c6970150842f6c50  2026-08-30-core-rule-with-4.log
6f64906e19d718ef4120a9585f7b1975  2026-08-30-core-rule-without-3.log
b3fdc3804f9a5d619dc524fdd39bf80e  2026-08-30-core-rule-without-4.log
654b19b2632c46aeb72b7263cd0a7b95  2026-08-30-v12-placeholder-map-1.log
c47c7b7a609b6fba9497f485ae39b510  2026-08-30-v12-placeholder-map-2.log
1c9b82e34dd64ca8b630a98a4449a63a  2026-08-30-v12-released-text.log
934200f24d993a14e7da4f2201c42549  2026-08-30-plugin-rule-with-1.log
8b91c174104a50cffd9965b7f168460d  2026-08-30-plugin-rule-with-2.log
5bd9304237ff56fa92a736512a7c781a  2026-08-30-plugin-rule-without-1.log
bbdb540a1404428af8bffc585299797c  2026-08-30-plugin-rule-without-2.log
581c5cd05a5260c8ecec3e1fe4742013  2026-08-30-v3-aM1.log
987f8d6b8661be4096d4390dfaadcce6  2026-08-30-v3-aT1.log
1f56e5b83270fae961090d5ab45b8c72  2026-08-30-v3-vM1.log
57c058c55d3e193caf615d27c010dff9  2026-08-30-v3-vT1.log
d3c559668ceccde4d730b65347c02bfc  2026-08-30-v3-wM1.log
9f2b55340e115f9537d2fc8113c3ac26  2026-08-30-v3-wM2.log
2f7c8d50137719a22e7188a9db8edaff  2026-08-30-v3-wT1.log
dce9408a27781163921d5b56650ce5a2  2026-08-30-v3-wT2.log
615519e2c7f03649b76b7658ba6ef6ee  2026-08-30-boundaries-coldstart-empty-z1.log
9a31b2045357d4e467bc38d8b16ec38a  2026-08-30-boundaries-coldstart-empty-z2.log
498960335f9dfd5f5e4efd3c2d6212c5  2026-08-30-boundaries-coldstart-populated-y1.log
c7ab2bbb8a740c4cf1ebeef6929577e4  2026-08-30-boundaries-coldstart-populated-y2.log
be18cd947b8ce2fd23f7917156207220  2026-08-30-boundaries-interview-x1.log
7324890a9a64e96571ef3736397ea75c  2026-08-30-boundaries-interview-x2.log
0a3895d3c22a6861344cbd199c7f73ea  2026-08-30-boundaries-interview-x3.log
5d3badf6156ea0285a1051254da274f9  2026-08-30-boundaries-interview-x4.log
```

## What they are evidence for

The scoring of three pre-registrations,
[`registry-check-first-run.md`](../predictions/registry-check-first-run.md) and
[`registry-check-second-run.md`](../predictions/registry-check-second-run.md) and
[`registry-check-negative-run.md`](../predictions/registry-check-negative-run.md). Read those for
what was predicted; read these for what happened.

Two pairs carry most of the weight.

The control against the first log: check 6 passes in one and fails in the other, on a byte-identical
prompt against an unchanged scope. That pair is the whole evidence for the limit now stated in
[`blueprints/checks/README.md`](../../blueprints/checks/README.md), that an under-specified row
returns a confident table either way.

The two negative logs against each other: check 1 fails identically in both, which is the check doing
the job it exists for, while the rows downstream of it disagree between the runs. In the repeat,
check 6 **passes** for a component whose folder does not exist, on the reasoning that a missing
folder contains no `PROJECT.md`. That is true and worthless, and it is the clearest single artefact
of a row being forced into a verdict it has no basis for.

---

## The four interview logs are a different kind of run, and the index should say so

Every other log here is a **check** run against a real project scope. The four
`2026-08-29-interview-length-*` logs are **setup** runs against a scratch folder, and what they
record is a question block rather than a verdict table. They were produced by `claude -p`, one fresh
non-interactive session each, with `Write`, `Edit` and `NotebookEdit` disabled so no run could write
into the scope — a deviation from an ordinary adoption, identical across both arms, recorded in
[`../predictions/interview-length-0.7-against-head.md`](../predictions/interview-length-0.7-against-head.md).

The prompt was `blueprints/setup/new-project.md`'s own paste block with the two addresses filled in.
That file is **byte-identical between `v0.7.0` and `HEAD`**, so the two arms' prompts differ in
exactly one line, the framework path.

They are evidence for two things. The pre-registered one is length, and it came out indeterminate by
the thresholds set in advance. The one nobody registered is worth more: **arm A run 1 and arm B run 2
each asked a question the setup procedure explicitly forbids**, and they are different questions in
different versions. `a1` asks whether `.docs/` exists while stating in the same sentence that it does
not — a question about something it had already read. `b2` asks the person for each component's
posture, which Step 4 says in as many words is not a question and must be proposed. Two violations of
two named rules in four runs, on both sides of four releases.

**The six `shipped-script` logs are the subject changing, not the scope.** Arms C and D ran against a
framework that does not exist in any commit of `blueprints/`: `HEAD` with a drafted interview script
installed and `procedure.md` Step 4 replaced by a pointer to it. Both the installed file and the exact
Step 4 diff are committed beside the draft, as `.docs/drafts/interview-as-installed.md` and
`.docs/drafts/step-4-replacement.diff`, because a run against a tree nobody can reconstruct is not
evidence.

In all four script runs the question block is byte-identical to the script — `difflib` similarity
1.000, zero added words. The control arm B′ moved the question block by −3.5% against arm B on a
completely different scope, which **weakens** the folder-variance finding these logs were partly meant
to support. Both results are scored in
[`../predictions/does-a-shipped-script-stay-shipped.md`](../predictions/does-a-shipped-script-stay-shipped.md).

**The five `2026-08-30-registry-check-1{0,1,2}` logs are the `0.14.0` change.** They were produced by
`claude -p`, one fresh non-interactive session each, the prompt block pasted from
`registry-check.md`'s raw text rather than referenced by path — which is why row 7 passes in all
five, and why it failed on the ArtGlina run that prompted the change.

**The three `2026-08-30-registry-check-1{3,4,5}` logs are the `0.15.0` change**, and they exist
because row 7 caught its own runner. The operator's interactive run against ArtGlina failed row 7 on
`/home/kostritsaalex/Projects`, a folder no registry line names, read by one command that tested both
component paths at once. These three ran against the repaired text, one fresh `claude -p` session
each, **with the parent granted in every arm** so that the failing command remained available and the
prompt was the only thing preventing it. Arm 1 lists three folders and no fourth; the disclosed plant
still fails row 7 and names the folder; a component two levels below an undeclared folder is reached
by one command and its intermediates appear nowhere. Pre-registered before the edit existed, in
[`../predictions/registry-check-one-path-one-command.md`](../predictions/registry-check-one-path-one-command.md).

Predictions for all three arms were written before the edit existed, in
[`../predictions/registry-check-declared-not-attached.md`](../predictions/registry-check-declared-not-attached.md),
and every one held. Two arms were run twice for the reasons the index gives, and in both pairs the
verdicts agree; what differs is the quality of the evidence, not the result.
