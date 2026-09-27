# Rubric: is this a good first issue?

Five required checks, one per way a first contribution dies: nobody is
home, nobody uses the software, the work has no edges, somebody else is
already doing it, or the project will not take work made the way I make
it. Three preferred checks rank the issues that survive.

All "within N days" thresholds are measured against the capture date in
the bundle header (eval mode) or today (live mode).

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `maintainer-alive` | The "last 5 default-branch commits" list under Repo facts (live: the commit history linked from the repo front page) | The newest of those commits is dated within 180 days. A bot-authored commit counts only when it merges a human's pull request | required |
| `repo-in-use` | The "archived:" flag, "latest release", and "last push to any branch" lines under Repo facts | `archived: no`, AND the latest release is within 365 days; if no release is published, the last push to any branch is within 180 days instead | required |
| `scope-fits-newcomer` | The issue title and body, the comment thread, and the "linked PRs:" states under Repo facts | Default to pass. Fail only on one of four disqualifiers, and only when you can quote the text that matches: (a) a container issue; (b) an undecided end state on a *new feature*; (c) two or more closed-unmerged linked PRs; (d) a support question. Each is defined below; nothing outside that list fails this check | required |
| `unclaimed` | The "assignees:" and "linked PRs:" lines under Repo facts, plus every claim in the comment thread | All three of: no assignee; no linked or thread-mentioned PR in state open; no unreleased claim comment dated within 180 days | required |
| `ai-policy-allows` | The "contribution policy" line under Repo facts (live: `CONTRIBUTING.md`, `AI_POLICY.md`, contributor docs, PR templates) | The policy is silent, absent, or sets conditions on AI use. Fail only on an outright refusal of AI-written code or docs with no permitted assisted path | required |
| `maintainer-responsive` | The "maintainer first-response sample" under Repo facts | At least one sampled issue got an owner/member/collaborator reply within 30 days | preferred |
| `newcomer-signposted` | The issue's labels and body | It carries a `good first issue` or `help wanted` label, or the body names the files, paths, or acceptance criteria to start from | preferred |
| `recent-activity` | The issue's open date and the dates on its comments | The issue was opened or last commented on within 180 days | preferred |

## How to apply the checks

**`maintainer-alive` vs `repo-in-use`.** They fail for different reasons
and both matter: a repo can ship releases from a frozen fork, and a repo
can have daily commits on software nobody installs. Grade them
separately off the lines named above. Do not fold response latency into
either one; a busy project with a long triage queue is alive, and
`maintainer-responsive` already carries that signal at preferred weight.

**`scope-fits-newcomer`** fails on exactly these four things:

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
- *(b) The end state is not decided.* Ask this of new features and
  product decisions only. A bug report, a docs change, or a fix to
  behavior the issue states is wrong passes (b) automatically, whoever
  filed it — do not go looking for endorsement on those. For a feature:
  fail when no maintainer (OWNER, MEMBER, or COLLABORATOR) filed it,
  labeled it, or endorsed it in the thread; or the thread shows a design
  question still being argued with no maintainer ruling; or something
  the change cannot be built without is still marked TBD.
- *(c) Two or more closed-unmerged linked PRs.* Repeated abandoned
  attempts mean the work is harder than the write-up admits. One closed
  attempt is not enough to fail: people drift away for reasons that have
  nothing to do with the issue.
- *(d) It is a support request.* "How do I get this to work?" is a
  question for the maintainer, not a contribution.

None of these fail it: a long body, a terse body, several files or
several sub-tasks inside one coherent change, a missing reproduction,
real technical difficulty, a hard performance fix, or an issue that has
been open for years. Grade the size and definiteness of the work being
asked for, never the polish of the writing or the age of the thread. If
no quotable disqualifier is present, this check passes.

**`unclaimed`.** An open PR is the strongest claim there is, whether the
sidebar links it or a commenter merely mentions it; when sidebar and
thread disagree, believe the thread. A closed-unmerged PR is an
abandoned attempt, not a claim (it feeds (c) above instead). A claim
comment goes stale after 180 days; treat it as released sooner only if
the claimer stepped back or a maintainer reopened it to others. A bot
asking "are you still working on this?" does not release a claim, and
a `good first issue` label is a statement that the issue is friendly,
never that it is free.

**`ai-policy-allows`.** Conditions are not bans. Disclosure, human
review, personal understanding, testing, and "no fully AI-generated
pull requests" are terms to work under, and they pass. Fail only when
the project states it does not accept AI-written code or documentation
at all, so there is no version of my workflow it would take. Silence
passes: most repos say nothing, and nothing is not a restriction.

## Verdict rule

Accept only if every `required` check grades `pass`. Any required check
graded `fail` or `unclear` makes the verdict `reject`: an issue whose
evidence I cannot find is an issue I cannot vouch for, and `unclear` is
a fail wherever this rubric does not say otherwise.

`preferred` checks never change a verdict. They rank the accepted
issues: among issues this rubric accepts, prefer the one with more
preferred checks passing, and say which ones in the summary.
