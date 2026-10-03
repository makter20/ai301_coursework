# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

makter20

---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60#issuecomment-5967263551

Hi, I'd like to take this on as my first contribution.

Others have already confirmed the `TypeError` at `faithfulness_checker.py:38` when a chunk has `text: None`. Next, I'll reproduce it myself at current `main` with the issue's snippet and `test_none_context_chunk_text` (using `--runxfail`), compare it against a chunk with no `text` key, and post my environment and output here. I'm committing to the reproduction report, not a fix or a timeline.

Disclosure: I'm using Claude Code for this course work. I'll run every command myself and only paste real output.

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60#issuecomment-5967284474

Reproduced: same `TypeError` at `faithfulness_checker.py:38`.

**Environment**

- `main` at `2f4e82f52efbcfcc57d65b3fa5348672163ca088`, fresh clone
- macOS 14.5 (x86_64), Python 3.13.5
- Clean venv: `structlog` 26.1.0, `pytest` 9.1.1 (the module only imports `re` and `structlog`; no `make setup`/Docker)

**Steps**

```bash
git clone https://github.com/codepath/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
python3 -m venv .venv
.venv/bin/pip install "structlog>=24.1.0" "pytest>=7.4.0"
.venv/bin/python -c "
from rag.evaluator.faithfulness_checker import FaithfulnessChecker
FaithfulnessChecker().check('Knows Python.', [{'text': None}])
"
```

**Actual** (exit 1)

```text
  File ".../rag/evaluator/faithfulness_checker.py", line 38, in check
    context_text = " ".join([chunk.get("text", "") for chunk in context_chunks])
TypeError: sequence item 0: expected str instance, NoneType found
```

**Expected:** returns a float, per `test_none_context_chunk_text`.

**Control:** `[{'content': 'Python skills'}]` (no `text` key) → `score = 0.0`, no crash.

**Named test**

- `pytest tests/unit/test_faithfulness_checker.py -k test_none_context_chunk_text` → `1 xfailed`
- with `--runxfail` → `1 failed`, same `TypeError` at line 38

No code or markers changed. Tested on one machine and Python version only.

Disclosure: I'm using Claude Code for this course work.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

All four runs, in order:

1. Calibration check (`--only calib-01,calib-03,calib-04 --include-calibration`): 0/0 scored. Calibration packages are never scored, but all 3 matched their labels.
2. First full run: **17/20** (below the 18/20 bar). The misses were all false rejects of accept packages (clear-accept 5/8): pkg-05 (steps-followable, template-coverage), pkg-09 (behavior-matches), and pkg-10 (behavior-matches, claims-backed).
3. Canary re-run after revising the rubric (`--only pkg-05,pkg-09,pkg-10,pkg-18,pkg-14,pkg-02,pkg-20,calib-03 --include-calibration`): 7/7 scored. The three misses flipped to accept and the four reject canaries still held.
4. Final full run (`--save-run`): **20/20** (PASS). This matches the agreement line in the `eval-run.txt` I committed.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]
It covers pkg-09, an honest cannot-reproduce for fd's --exec-batch ordering issue:

- Verdicts: the gold label is accept. My rubric graded it reject on the first full run and accept on the final run.
- Why it was rejected: the old behavior-matches wording asked for "the issue's trigger run". The grader read that as "the trigger was reached", which an honest cannot-reproduce by definition hasn't done.
- Why it now passes: the revised condition asks for a plain statement that it didn't reproduce, output from a real attempt, and the differences named. pkg-09 shows all three, so the same evidence passes.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

The `behavior-matches` check, as it reads in `tools/repro-check/rubric.md` now:

> | behavior-matches | The report's artifacts (output excerpts, logs, exit codes, screenshots), read against the failure the issue describes | The artifact shows the same failure the issue describes: same kind of error (panic vs graceful error, crash vs garbled output), same message or symptom, reached through the issue's input, not a modified one. An honest cannot-reproduce passes when the report states it didn't reproduce, shows output from a real attempt at the issue's steps, and names what differed from the reporter's setup or what a triggering setup likely needs. It doesn't need to have hit the trigger: failing to reach it, said plainly, is the honest result. Fails if the artifact shows an adjacent failure, a different error from changed input, or only that the program runs. | required |

Why it reads that way:

- What I revised: the earlier pass condition asked for output from "the issue's trigger run". The grader read "trigger run" as "the trigger was reached", so honest packages failed this check on my first full run: pkg-09 (a cannot-reproduce) and pkg-10, both gold accept. A cannot-reproduce never reaches the trigger, so that wording made honesty impossible to pass.
- What replaced it: three things a grader can see in the artifacts: a plain statement that it didn't reproduce, output from a real attempt at the issue's own steps, and the differences from the reporter's setup named. I added "It doesn't need to have hit the trigger" so the old reading can't come back.
- What I kept strict: the first sentence still requires the same kind of error, the same symptom, and the issue's input, not a modified one. Loosening the cannot-reproduce path couldn't open a door for wrong-target packages. Showing an adjacent failure, a different error from changed input, or just that the program runs still fails.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This is the trade-off in loosening `behavior-matches` so an honest cannot-reproduce can pass:

- Package it changed: pkg-09 went from reject to accept, matching its gold label of accept.
- Why nothing else changed: the revision only added a cannot-reproduce path. The first sentence, which requires the same kind of error and the symptom reached through the issue's input, wasn't touched. In the final run every reject category still agrees: wrong-target 4/4, no-evidence 4/4, unfollowable-comms 3/3, disclosure 1/1. No package that should hold slipped through the new path.
- A case I accept it will miss: a lazy cannot-reproduce. It makes one shallow attempt, shows that output, says "didn't reproduce", and names a guessed difference (e.g. "maybe it's macOS-only"). That passes `behavior-matches`, because the check asks that a difference is named, not that it's plausible or was tested. `claims-backed` only catches it if the package goes further and says the bug is absent or fixed. I'm accepting that, because the alternative of making the grader judge whether a guess is good enough brings back the disagreement that failed pkg-09.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
