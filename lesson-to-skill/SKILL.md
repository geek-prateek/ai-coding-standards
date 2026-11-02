---
name: lesson-to-skill
description: Use after a confirmed mistake — user correction, the same blocker twice, a failed run with a known root cause, or an authoring defect — so that mistake is not repeated. Land the lesson in the owning existing skill, or create a new skill if none owns it. Skip when the owner already states the lesson.
---

# Lesson to Skill

A confirmed mistake is a **lesson**. Land it in one owning skill so the next run hits the rule before it repeats the error. This skill is standing approval to land that lesson — do not wait for a second "please update the skill".

Run this **after** [cite-or-stop](../cite-or-stop/SKILL.md) has stopped retries (or after the user points out a mistake). Do not keep implementing while landing.

## 1. Name the lesson

One sentence: what went wrong, what the next run must do instead. Attach citations (`[code]`, `[runtime]`, `[ticket]`, `[user]`, `[skill]` per cite-or-stop). If the only explanation is unsourced, prefix `Invented (not approved):` and **do not land it** until the user confirms that thought.

Done when: the lesson is one cited sentence, or you have stopped because it is still unverified.

## 2. Find the owner

Search your skills directory (`.agents/skills/*/SKILL.md` or equivalent) descriptions first, then bodies, for the domain of the lesson (e.g. testing, database, authentication, API integrations, build tools, ...). Pick **one** owner:

| Owner | Land in |
|---|---|
| Exact existing skill | that `SKILL.md` |
| Partial match | that skill, smallest edit |
| Lesson is a general coding/style rule | Global project rules (e.g. `AGENTS.md`), not a new skill |
| Owner is a third-party/vendored skill | A custom project skill. Leave third-party files untouched |
| No owner found | §4 Create |

If the owner already states the lesson, **take no action** — the failure was in skill activation. Sharpen that skill's `description` trigger so the next run loads it automatically. Do not paste duplicate text into the body.

Done when: you have one owner path, or a documented "already stated / description sharpened" outcome.

## 3. Patch the owner

Smallest change that would have prevented **this** run:

- **Co-location:** Place the durable rule directly under the existing heading it logically belongs with.
- **Trigger sharpening:** If the agent failed to load the skill, sharpen the `description` keyword triggers.
- **Prune incident details:** Keep only the universal, forward-looking rule. Delete any narrative that just retells this one incident.

Done when: a later agent session reading that skill would take the corrected action without needing this chat context.

## 4. Create only when none owns it

New skill at `.agents/skills/<name>/SKILL.md` (or your platform's skills directory).
- Model-invoked `description` with distinct, specific triggers.
- Concrete **Done when:** completion bounds on every step so the agent cannot exit prematurely.
- Keep it a reusable workflow pattern, not a diary of a specific bug.

Done when: the new file exists with valid frontmatter, or you skipped creation because an existing owner was patched.

## 5. Report

Tell the user: owner path, created vs patched vs skipped (already stated), and the one-sentence lesson that landed.

Done when: that summary is clearly stated in the response.
