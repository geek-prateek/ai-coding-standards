---
name: cite-or-stop
description: Use when a task is blocked, the same retry failed, product or test behavior cannot be produced, or you are about to explain why something works or does not. Cite every claim; after the same blocker twice, stop looping and hand off one next approach. Label any unsourced idea Invented (not approved).
---

# Cite or Stop

Two jobs: **cite** what you know, and **stop** when Cursor cannot finish it. A third retry of the same strategy is the failure mode this skill exists to cut.

## 1. Cite every claim

Every sentence that states a fact carries a source on that sentence (or the one immediately after). Source tags:

| Tag | Use when |
|---|---|
| `[code] path:lines` | Repo file you read this turn |
| `[runtime]` | Screenshot, quoted UI text, or a command you ran |
| `[ticket] KEY` | Jira/AC/comment you retrieved |
| `[user]` | Instruction in this chat |
| `[skill] name` | Another skill required the step |

Done when: a reader can tell, for each factual sentence, which tag backs it.

## 2. Stop on the same blocker twice

A **blocker** is evidence that the current strategy cannot produce the requested outcome (same modal, same missing field, same catch-22 in code).

After the **second** evidence-backed hit of that blocker:

1. State the blocker with its citations.
2. Skip any further attempt of the same strategy (different amount, different click order, different wait — still the same strategy if the cited catch-22 is unchanged).
3. Go to **§3 One handoff**.

Done when: you have not started a third attempt of that strategy.

## 3. One handoff

Give **one** next approach. Not a menu of guesses. The handoff names:

- **Blocked outcome** — what the user asked for, in their words
- **Why this agent cannot finish it** — cited (code, runtime, missing source)
- **Where it can be resolved** — a real owner and place: human with UAT/DB, product/QA, unread engine/DLL, Jira gap, or [brain-wave](../brain-wave/SKILL.md) when a human decision is required
- **What to take there** — the cited facts, not a new untested UI script

Done when: the user has one owner, one place, and the evidence pack for that place.

Then load [lesson-to-skill](../lesson-to-skill/SKILL.md) so the blocker is landed in an owning skill and is not retried next run.

## 4. Label invented

Any step, journey, or explanation that does not rest on a §1 tag is **invented**. Prefix it:

`Invented (not approved):` + the thought that produced it.

Invented material is never presented as repo convention, ticket AC, or a proven user journey. If the only remaining approach is invented, say so in the handoff and stop; do not run it unless the user explicitly chooses it.

Done when: every unsourced idea in the reply carries that prefix, and none is implied to be approved.
