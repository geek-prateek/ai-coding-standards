---
name: cite-or-stop
description: Use when a task is blocked, a retry failed, debugging behavior or test failures, or making factual claims about codebase/runtime state. Cite factual claims; after the same blocker twice, stop looping and hand off one next approach. Label unsourced ideas Invented (not approved). Casual and conceptual Q&A are exempt from inline tagging.
---

# Cite or Stop

Two jobs: **cite** what you know, and **stop** when the agent cannot finish it. A third retry of the same strategy is the failure mode this skill exists to cut.

## 1. Ground claims with citations

Citations prove that assertions are backed by real evidence rather than assumptions.

### Scope: When to Cite vs Conversational Mode
- **Strict Citation Mode (Mandatory)**: Apply tags when diagnosing bugs, reporting test failures, analyzing blockers, verifying ticket requirements, or explaining why repository code works or fails.
- **Conversational Mode (Exempt)**: Casual Q&A, conceptual programming explanations, high-level overviews, and conversational transitions do not require inline tags. Keep explanations natural, readable, and uncluttered.

### Source Tags

| Tag | Use when |
|---|---|
| `[code] path:lines` | Repo file you read this turn |
| `[runtime]` | Screenshot, quoted UI text, or a command you ran |
| `[ticket] KEY` | Jira/AC/comment or issue tracker item retrieved |
| `[user]` | Instruction or preference in this chat |
| `[skill] name` | Another skill required the step |

Done when: codebase-specific and diagnostic claims are clearly backed by tags, while casual conversation remains natural and readable.

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
- **Where it can be resolved** — a real owner and place: human with UAT/DB, product/QA, unread engine/DLL, Jira gap, or human decision workflow when clarification is required
- **What to take there** — the cited facts, not a new untested UI script

Done when: the user has one owner, one place, and the evidence pack for that place.

Then load [lesson-to-skill](../lesson-to-skill/SKILL.md) (or repo equivalent) so the blocker is landed in an owning skill/rule and is not retried next run.

## 4. Label invented

Any diagnostic step, repo journey, or codebase assumption that does not rest on a §1 tag is **invented**. Prefix it:

`Invented (not approved):` + the thought that produced it.

*Note: This applies to unverified assertions about the specific codebase or requirements, not standard programming concepts.* If the only remaining approach is invented, say so in the handoff and stop; do not run it unless the user explicitly chooses it.

Done when: every unsourced codebase idea in the reply carries that prefix, and none is implied to be approved.
