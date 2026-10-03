# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

- Where it lives: eval, the repro report's environment line or section,
  read against the issue's own environment (often in the issue body)
  and the repo-facts block's "bug reports" template asks and "latest
  release" line. Live, the student's draft repro comment against the
  issue body and the repo's issue template
  (`.github/ISSUE_TEMPLATE/`).
- What good looks like: the software's version and the OS are named,
  plus any setting the issue or template ties to the behavior (build
  profile, driver, shell, install method). The tested version is the
  issue's, the latest release, or main. If it differs from the issue's,
  the report says so in a sentence. A report with no environment at
  all fails, however good its output looks.

## Steps

- Where it lives: eval, the commands, inputs, and config shown in the
  repro report (code blocks and the prose around them). Live, the same
  in the draft repro comment.
- What good looks like: starting from nothing but the stated
  environment, a stranger could run every step. Input files and config
  are shown inline, linked publicly, or described precisely enough to
  recreate (the triggering element named), every command or UI action is
  named, and any setup the issue says is needed appears. Terse is fine.
  Steps that run against a private repo, unshared config, or "my
  project" fail.

## Behavior shown

- Where it lives: eval, the artifacts in the repro report (pasted
  output, logs, exit codes, error messages, `git status`-style
  checks), read against the failure the issue body describes. Live,
  the same artifacts in the draft against the live issue body.
- What good looks like: put the artifact next to the issue's
  description and ask "is this the same failure?" It needs the same
  failure class (panic vs graceful error, crash vs garbled output,
  silent no-op vs error), the same message or symptom, and the
  issue's input. Check that the input matches the issue character for
  character: a changed operator, flag, or range syntax that produces a
  different error is a wrong target, not a reproduction. A control run
  (same steps, trigger removed, normal result) strengthens the proof.
  Artifacts that only show the program running, or a version banner,
  show nothing. An honest cannot-reproduce counts when it says plainly it didn't
  reproduce, shows output from a real attempt at the issue's steps, and
  names what differed or what a triggering setup likely needs. Not
  reaching the trigger is the honest result, not a failure.

## Honesty

- Where it lives: eval, every assertion in the claim comment and repro
  report ("reproduced", "confirmed", "deterministic", "root cause is",
  "affects every version", "I verified"), each paired with the
  artifact that's supposed to back it. Live, the same in both drafts.
- What good looks like: each assertion points at something shown.
  "Reproduced" means the behavior artifact matches the issue. A cause
  is stated as a hypothesis unless the package shows evidence for it.
  A cannot-reproduce says what was tried and what differed from the
  reporter's setup. Ordinary wording like "happens every run" next to
  a shown run is fine. Red flags: certainty language over an artifact
  that shows a different failure; frequency or scope claims ("on all
  my machines", "everyone has this") with nothing shown; the expected
  and actual lines contradicting the artifact.

## Comms

- Where it lives: eval, the claim comment read against the issue
  title and body; both comments read against the repo-facts block's
  "contribution policy" line (AI-use policy, disclosure requirements,
  rules about human-written comments) and the thread highlights
  (other claims, linked fixes, a reporter who has a fix ready). Live,
  the draft comments against the repo's CONTRIBUTING.md, any AI policy
  file, the issue thread, and `scope.md`'s house rules (a classmate's
  claim doesn't block you).
- What good looks like: the claim names this issue's specific behavior
  and a next step the author can deliver, with no guaranteed dates,
  no "assign me", no +1. If the policy requires AI disclosure, a
  sentence discloses it. If the policy requires human-written
  comments, the words read as the author's own, specific to this
  thread. Where the thread shows someone else working on a fix, the
  claim acknowledges it and offers something complementary
  (verification, testing) rather than racing it.
