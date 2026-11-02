---
name: cite-or-stop
description: Use when a task is blocked, the same retry failed, product or test behavior cannot be produced, or you are about to explain why something works or does not. Cite every claim; after the same blocker twice, stop looping and hand off one next approach. Label any unsourced idea Invented (not approved).
---

# Cite or Stop

Two jobs: **cite** what you know, and **stop** when the agent cannot finish it. A third retry of the same strategy is the failure mode this skill exists to cut.

## 1. Cite every claim

Every sentence that states a fact carries a source on that sentence (or the one immediately after). Source tags:

| Tag | Use when |
|---|---|
| `[code] path:lines` | Repo file you read this turn |
| `[runtime]` | Screenshot, quoted UI/terminal output, test log, or a command you ran |
| `[ticket] KEY` | Issue tracker, requirements doc, or spec you retrieved |
| `[user]` | Instruction given directly by the user in this chat |
| `[skill] name` | Another loaded skill or official project rule required the step |

Done when: a reader can tell, for each factual sentence, which tag backs it.

## 2. Stop on the same blocker twice

A **blocker** is evidence that the current strategy cannot produce the requested outcome (same error trace, missing dependency/schema, unhandled environment constraint).

After the **second** evidence-backed hit of that blocker:

1. State the blocker with its citations.
2. Skip any further attempt of the same strategy (different arguments, changing timeout, or minor code reordering is still the same strategy if the cited root cause is unchanged).
3. Go to **§3 One handoff**.

Done when: you have not started a third attempt of that strategy.

## 3. One handoff

Give **one** next approach. Not a menu of guesses. The handoff names:

- **Blocked outcome** — what the user asked for, in their words.
- **Why this agent cannot finish it** — cited (code line, runtime exit code, missing credentials/API spec).
- **Where it can be resolved** — a real owner and place: human reviewer, database/cloud access, product decision, or architectural clarification.
- **What to take there** — the cited facts, not an untested speculative script.

Done when: the user has one owner, one place, and the cited evidence pack.

Then load [lesson-to-skill](../lesson-to-skill/SKILL.md) so the blocker is landed in an owning skill and is not retried next run.

## 4. Label invented

Any step, premise, or explanation that does not rest on a §1 citation tag is **invented**. Prefix it:

`Invented (not approved):` + the thought that produced it.

Invented material is never presented as repo convention, ticket requirements, or verified behavior. If the only remaining approach is invented, say so in the handoff and stop; do not execute it unless the user explicitly chooses it.

Done when: every unsourced idea in the reply carries that prefix, and none is implied to be approved.
