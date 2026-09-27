# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60

**Verdict output**

Live-mode run over three candidates (#60, #68, #64), pasted verbatim. The skill
accepted one and rejected two; #60 is the accepted issue carried forward.

## Summary

Graded all three candidates from `codepath/pathreview-ai301-fa26-s3` (repo-level facts — archived: no, latest release: none published, last push 2026-09-16, last 5 commits all human/COLLABORATOR-authored within 11 days, no AI-use ban found in `docs/CONTRIBUTING.md` or PR templates — apply to all three).

**Accepted (1), ranked by fit:**
1. **#60 — Faithfulness checker crashes on `text: None`** — clean bug report with a reproducible `TypeError` and a named failing test in `rag/`, no open PR against it (only a student claim comment, exempted by the Path Review house rule). Top fit: Python, a real crash with a stack trace, no competing PR — exactly the "reproduce a failure, land a small fix" practice you're after.

**Rejected (2):**
- **#68 — Keyword search `ZeroDivisionError`** — sunk by `unclaimed`: PR #74 ("Fixes #68") is open and actively implementing the fix.
- **#64 — Relevance scorer fixture bug** — sunk by `unclaimed`: PR #75 ("Closes #64") is open and actively implementing the fix.

Note: the classroom house rule exempts *claim comments* from blocking an issue, but not open PRs — an open PR is still the strongest claim there is, and both #68 and #64 have one.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 (11 days before today's 2026-09-27), authored by Aburke225 (COLLABORATOR)"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: no; no release published; last push 2026-09-16 (11 days ago), within 180 days"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Bug report with exact repro (`FaithfulnessChecker().check(...)` -> TypeError) and named failing test `test_none_context_chunk_text`; no disqualifier present"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignee; timeline shows only a dangling/deleted commit reference (not a PR) and one student claim comment ('I'll take this — working on the fix now.'), exempted by the Path Review house rule"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md sets workflow terms (CI green, xfail-marker removal) but states no ban on AI-written code; silence passes"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled 8 recently-updated issues (#62,#53,#72,#56,#69,#73,#54 plus #60 itself); zero comments from an OWNER/MEMBER/COLLABORATOR"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "Labeled `good first issue`, `bug`; body names the exact file/test to start from"},
      {"name": "recent-activity", "grade": "pass", "evidence": "Last comment 2026-09-21, 6 days before capture"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Same repo facts: newest commit 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: no; no release; last push 2026-09-16"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Bounded bug fix naming exact files (`rag/retriever/keyword_search.py`, its test) and the xfail marker to remove; no disqualifier present"},
      {"name": "unclaimed", "grade": "fail", "evidence": "PR #74 'fix: handle empty keyword search indexes' is open (not draft), body reads 'Fixes #68'"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "Same repo-level finding: no ban on AI-written contributions"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Same repo facts: newest commit 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: no; no release; last push 2026-09-16"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Bug fix to a test fixture with exact repro command (`pytest tests/unit/test_relevance_scorer.py -q`); no disqualifier present"},
      {"name": "unclaimed", "grade": "fail", "evidence": "PR #75 'test: make partial relevance fixture truly partial' is open (not draft), body reads 'Closes #64'"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "Same repo-level finding: no ban on AI-written contributions"}
    ],
    "verdict": "reject"
  }
]
```

---

## Eval iterations

**Run history**

Four runs, in order:

1. `--limit 3` smoke run — **3/3**. Confirmed the harness, the skill and my rubric
   were wired together before spending a full run.
2. Full run — **17/20**, below the 18/20 bar. Three false rejects: `issue-01`,
   `issue-04` and `issue-19`, all failing the same check, `scope-fits-newcomer`.
3. `--only issue-01,issue-04,issue-19,issue-05,issue-10,issue-15,issue-20` after
   rewording that check — **7/7**. The three misses flipped to accept and the four
   scope-category rejects held.
4. Full confirming run with `--save-run eval-run.txt` — **20/20**, category floor
   met in all five categories (claimed 4/4, clear-accept 8/8, dead-repo 3/3,
   policy 1/1, scope 4/4).

The last score matches the agreement line in the committed `eval-run.txt`:
`agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Issue analysis**

`issue-19` (zxcalc/zxlive#517, "Selecting large subgraphs in proof mode freezes the
UI"). My rubric's final decision: **accept**. Gold label: **accept**.

My rubric reaches accept because every required check passes on the bundle's own
facts: the newest default-branch commit is dated 2026-08-04, one day before the
capture date, so `maintainer-alive` passes; the repo is unarchived with a release
on 2026-04-29, so `repo-in-use` passes; there are no assignees and no linked PRs
at all, so `unclaimed` passes; and the contribution policy line says nothing about
AI, which `ai-policy-allows` treats as silence, which passes.

`scope-fits-newcomer` is the interesting one, because on my first full run it
failed here and produced a false reject. The issue body lists "two potential
causes which should be fixed" and then three "Additional suggestions", and my
original wording let the grader read that list as a menu of separate changes —
its recorded evidence was "a menu of sub-items, not one bounded change with a
decided end state". That reading is wrong for this issue: all of it is one
performance fix that one pull request would carry, filed by RazinShaikh, a
COLLABORATOR, who had already diagnosed the causes. The issue is hard, but hard
is not unbounded, and my rubric is supposed to grade the definiteness of the work
rather than its difficulty. I rewrote the check so a container issue means only an
umbrella, tracking, meta, epic or megaissue, a body that lists other issue
numbers, or an open-ended invitation to keep contributing — and so that optional
extras an issue itself marks "additional suggestions" do not unbound it. On the
re-run and on the confirming full run, `issue-19` passed and the verdict matched
gold.

**Check rationale**

From the `rubric.md` uploaded to `tools/issue-select/`, the `scope-fits-newcomer`
row as it is currently written:

```
| `scope-fits-newcomer` | The issue title and body, the comment thread, and the "linked PRs:" states under Repo facts | Default to pass. Fail only on one of four disqualifiers, and only when you can quote the text that matches: (a) a container issue; (b) an undecided end state on a *new feature*; (c) two or more closed-unmerged linked PRs; (d) a support question. Each is defined below; nothing outside that list fails this check | required |
```

and the first of its four disqualifiers, defined below that table:

```
- *(a) Not one bounded change.* Fail only when the issue calls itself
  an umbrella, tracking, meta, epic, or megaissue; or its body is a list
  of other issue numbers, or of sub-items it says should be split into
  separate issues or PRs; or it invites repeated incremental
  contributions with no defined finish ("PRs welcome, big and small,
  adding more of X").
  One pull request is one bounded change however many pieces it has, so
  these all pass (a): a list of sub-items, files, causes, or acceptance
  criteria that a single PR would carry together; a short list closed
  with "etc." whose full set is discoverable in the code; and optional
  extras the issue itself marks "consider", "lower priority", or
  "additional suggestions", which a newcomer ships the core without.
```

Two things are deliberate here. First, the check **defaults to pass and requires a
quotable disqualifier** to fail. Scope is the only judgment call in my rubric that
cannot be read off a dated field in the repo-facts block, so it is the check most
likely to drift on re-runs; forcing it to name the text that sank an issue is what
makes it reproducible rather than a feeling about difficulty. Second, the
disqualifier list is **closed** — "nothing outside that list fails this check" —
because my first full run failed three accepted issues on reasoning that sounded
sensible and was nowhere in my rubric.

**Trade-offs**

What this wording gives up: an issue that is genuinely unbounded but never says so
will now pass. A body that reads like one clean task, filed by a maintainer, with
no umbrella language and no list of issue numbers, is accepted by my rubric even
if the work behind it is a month of refactoring. I traded recall on that case for
reproducibility, on the grounds that my false rejects were real and costing me
three points while that failure mode did not appear in the set.

It changed results. `issue-01`, `issue-04` and `issue-19` were all rejected before
the rewrite and accepted after, which is the whole 17/20 to 20/20 move. Because
loosening a check risks leaking into the issues it is supposed to catch, I ran the
four scope-category rejects — `issue-05`, `issue-10`, `issue-15`, `issue-20` — as
canaries in the same `--only` run, and all four stayed rejected: `issue-05` still
fails on "PRs are welcome both big and small", `issue-10` still calls itself a
megaissue, `issue-15` still has two closed-unmerged linked PRs behind years of
unsettled design debate, and `issue-20` still leaves its logo asset TBD with no
maintainer endorsement. The confirming full run reproduced all four.

---

## Selection rationale

**Selection rationale**

1. **Fit to my interests and the time available.** I work in Python and Java and I
   wanted practice at bug fixing specifically — reading an unfamiliar codebase,
   reproducing a reported failure, and landing a small correct fix — rather than
   docs or feature work. #60 is a Python crash in the RAG faithfulness checker
   with a stack trace and a named failing test, `test_none_context_chunk_text`, so
   the reproduction step is already written for me and the fix is one guard on a
   `None` chunk. I also asked the skill to rank security issues last, and it did:
   nothing security-related is in my accepted list.

2. **What the verdict identified correctly, and what I weighed that it could
   not.** The verdict was right about the thing I would have got wrong by hand: I
   picked #68 and #64 as candidates because they looked like clean tier-1 bugs,
   and the skill found open pull requests already fixing both (PR #74 "Fixes #68",
   PR #75 "Closes #64") — PR #75 was opened the same morning I ran this. It also
   correctly applied the Path Review house rule to #60, where a classmate had
   commented "I'll take this" six days earlier: a claim comment from a classmate
   does not block a classroom issue, but an open PR is still a claim. What I
   weighed that the rubric could not: my `maintainer-responsive` check fails for
   this whole repository, because no owner, member or collaborator has commented
   on any recently updated issue. On a real open-source repo I would treat that as
   a warning. Here it is an artifact of Path Review being a course sandbox, so I
   discounted it — and it is a preferred check, so it never touched the verdict.

3. **Anticipated difficulty in claiming it.** Low, but not zero. Course credit
   attaches to the pull request I open rather than to whether it merges, and the
   house rule says a shared issue costs nobody anything, so the existing claim
   comment does not stop me. The real risk is the one I just watched happen to
   #64: someone opens a PR against #60 before I do. I plan to claim it in Unit 2
   promptly and to check for an open PR against #60 again immediately before I
   start.
