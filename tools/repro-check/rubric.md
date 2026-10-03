# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | The repro report's environment record, read against the issue's stated environment and the repo-facts block's bug-template asks | The report names the version of the software under test and the OS, plus every other setting the issue or template says changes the behavior (e.g. build profile, driver, shell, install method). A stranger can tell exactly where the attempt ran. Fails if no environment is recorded, or if a setting the issue says matters is missing. | required |
| target-version | The tested version in the environment record, read against the issue's reported version and the repo-facts block's latest release | The tested version is the issue's version, the current release, or main. A different version is called out in the report with the delta stated. Fails if an older version than the issue's is tested and the report doesn't say so. | required |
| steps-followable | The repro report's commands, inputs, and config, from starting state to trigger | A stranger could re-run every step from what the report shows: inputs and config are inline, public, or described precisely enough to recreate (the triggering element named, e.g. "an env.yml with a `category:` section"), and every command or UI action that reaches the trigger is named. Fails if the steps depend on private code, unshared config, or an unstated setup step the issue says is required. | required |
| behavior-matches | The report's artifacts (output excerpts, logs, exit codes, screenshots), read against the failure the issue describes | The artifact shows the same failure the issue describes: same kind of error (panic vs graceful error, crash vs garbled output), same message or symptom, reached through the issue's input, not a modified one. An honest cannot-reproduce passes when the report states it didn't reproduce, shows output from a real attempt at the issue's steps, and names what differed from the reporter's setup or what a triggering setup likely needs. It doesn't need to have hit the trigger: failing to reach it, said plainly, is the honest result. Fails if the artifact shows an adjacent failure, a different error from changed input, or only that the program runs. | required |
| claims-backed | Every assertion in the claim comment and repro report ("reproduced", "deterministic", "root cause is", "affects all versions"), read against what the artifacts show | Every claim matches an artifact in the package. A cannot-reproduce names what differed from the issue's setup; describing extra attempts in prose is fine when at least one attempt's output is shown and nothing claims the bug is absent or fixed. Fails if the package claims a reproduction, cause, frequency, or scope its artifacts don't show, or says the artifact confirms the issue when it doesn't. | required |
| claim-specific | The claim comment, read against the issue | The claim names this issue's specific behavior and states a concrete next step the author can actually deliver. Fails on interchangeable boilerplate ("assign me", "+1", "claiming this"), guaranteed fix timelines, or no stated intent. | required |
| policy-respected | The repo-facts block's contribution policy (including any AI-use policy), read against both comments | Two separate rules. (1) Disclosure: if the policy requires disclosing AI use, the comments disclose AI assistance; course packages count as AI-assisted work for this rule only. (2) Voice: if the policy requires human-written or human-reviewed comments, the comments pass when they read as the author's own words: specific to this issue, first-person, with no boilerplate or pasted model output. Being AI-assisted doesn't by itself fail the voice rule. Passes when the repo states neither requirement. Fails only if a stated requirement is unmet. | required |
| thread-aware | The thread highlights, read against the claim comment | If the thread shows another claim, a linked fix, or the reporter offering a fix, the claim acknowledges it and positions itself accordingly. Passes if the thread has none. | preferred |
| template-coverage | The repo-facts block's bug-template asks, read against the repro report | The report supplies every field the template asks for (version, OS, expected vs actual, etc.). | preferred |

## Verdict rule

Accept if every `required` check passes. Reject if any `required` check
is `fail` or `unclear`: proof that can't be verified isn't ready to
post. `preferred` checks never change the verdict; report them so the
author can tighten the comment. Exception for live claim-only drafts:
checks marked `unclear` with evidence `not yet applicable: claim-only
draft` are left out of the verdict, as SKILL.md directs.
