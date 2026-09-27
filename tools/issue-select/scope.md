# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s3`

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

<!-- YOU write this part: a few sentences about you. What languages and
tools you have actually used, what you want to get better at, anything
you want to avoid. The skill uses this only to RANK the issues your
rubric accepts, never to change a verdict: fit cannot rescue an issue
your rubric rejects, and cannot sink one it accepts. -->

I work mainly in **Python** and **Java**, and I use AI coding tools as
part of my normal workflow. What I want out of this contribution is
practice at **bug fixing**: reading an unfamiliar codebase, reproducing a
reported failure, and landing a small correct fix with a test behind it.

Rank accordingly. A bug report with a stated wrong behavior — a crash, a
wrong return value, a broken test fixture — ranks above a docs task or a
feature request. Python ranks above Java, and Java above anything else.

I do not want to work on security issues: authentication, password
handling, access control, ownership or permission checks, or anything
filed as a vulnerability. Fit never overrides a verdict, so an accepted
security issue stays accepted — but rank it last, below every
non-security candidate, and say so in the read-out.
