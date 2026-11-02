---
name: lesson-to-skill
description: Use after a confirmed mistake — user correction, the same blocker twice, a failed run with a known root cause, or an authoring defect — so that mistake is not repeated. Land the lesson in the owning existing skill, or create a new skill if none owns it. Skip when the owner already states the lesson.
---

# Lesson to Skill

A confirmed mistake is a **lesson**. Land it in one owning skill so the next run hits the rule before it repeats the error. This skill is standing approval to land that lesson — do not wait for a second "please update the skill".

Run this **after** [cite-or-stop](../cite-or-stop/SKILL.md) has stopped retries (or after the user names the mistake). Do not keep implementing while landing.

Before any create or edit, load [writing-for-agents](../writing-for-agents/SKILL.md).

## 1. Name the lesson

One sentence: what went wrong, what the next run must do instead. Attach citations (`[code]`, `[runtime]`, `[ticket]`, `[user]`, `[skill]` per cite-or-stop). If the only explanation is unsourced, prefix `Invented (not approved):` and **do not land it** until the user accepts that thought as the lesson.

Done when: the lesson is one cited sentence, or you have stopped because it is still invented.

## 2. Find the owner

Search `.agents/skills/*/SKILL.md` descriptions first, then bodies, for the domain of the lesson (automation, import Excel, FPS, citations, dual-framework, …). Pick **one** owner:

| Owner | Land in |
|---|---|
| Exact existing skill | that `SKILL.md` |
| Partial match | that skill, smallest edit |
| Lesson is a code/review convention | [update-knowledge](../update-knowledge/SKILL.md), not a new skill |
| Owner is listed in `.agents/vendored-skills.json` | a Brain-owned skill (create one if needed). Leave the vendored file untouched |
| No owner | §4 create |

If the owner already states the lesson, **take no action** — the miss was invocation. Optionally sharpen that skill's `description` trigger so the next run loads it. Do not paste a restatement into the body.

Done when: you have one owner path, or a documented "already stated / description sharpened" outcome.

## 3. Patch the owner

Smallest change that would have prevented **this** run:

- Durable rule next to the existing heading it belongs with (co-location).
- If the agent never loaded the skill, sharpen the `description` branch that should have fired.
- One meaning, one place. Delete any sentence that only retells this incident.

Write only under `.agents/skills/` (or knowledge via update-knowledge). Do not edit `.cursor/skills` or `.claude/skills` — those are symlinks.

Done when: a later agent that loads the owner would take the corrected action without reading this chat.

## 4. Create only when none owns it

New skill at `.agents/skills/<name>/SKILL.md` only — no nested `SKILL.md`. Model-invoked `description` with one trigger per branch. Follow writing-for-agents and SKILL-MECHANICS. Keep it a reusable pattern, not this ticket's diary.

Done when: the new file exists at that path, or you did not create because an owner was found.

## 5. Report

Tell the user: owner path, created vs patched vs skipped (already stated), and the one-sentence lesson that landed.

Done when: that report is in the reply.
