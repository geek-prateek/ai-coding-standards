---
name: lesson-to-skill
description: Use after a confirmed mistake — user correction, the same blocker twice, a failed run with a known root cause, or an authoring defect — so that mistake is not repeated. Land the lesson in the owning existing skill/rule, or create a new skill if none owns it. Requires verified evidence or explicit user approval before modifying any rule.
---

# Lesson to Skill

A confirmed mistake is a **lesson**. Land it in one owning skill or rule file so future runs avoid repeating the error.

> [!CAUTION]
> **Safety Principle**: Skills and rules are the agent's long-term memory. A wrong, hallucinated, or speculative rule poisons all future agent runs across the repository. Never land an unverified or speculative lesson directly into project rules.

Run this **after** [cite-or-stop](../cite-or-stop/SKILL.md) has stopped retries (or after the user names the mistake). Do not keep implementing code while landing a lesson.

Before any create or edit, follow project agent authoring guidelines (e.g. [writing-for-agents](../writing-for-agents/SKILL.md) if present).

---

## 0. Detect Repository Skills/Rules Location

Auto-detect the active agent configuration structure in the repository:
1. **Canonical skills directory**: Look for `.agents/skills/`, `.github/skills/`, `.claude/skills/`, or `.cursor/skills/`. If a directory is a symlink, target its canonical source.
2. **Rules directory**: Look for `.cursor/rules/`, `.windsurf/rules/`, `.gemini/rules/`, or `.cline/rules/`.
3. **Root instruction files**: If neither exists, locate project instruction files such as `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, or `.cursorrules`.

---

## 1. Formulate Lesson & Enforce Verification Gate

State the lesson in **one sentence**:
- What went wrong + What future runs must do instead.
- Attach specific citations (`[code]`, `[runtime]`, `[ticket]`, `[user]`, `[skill]` per `cite-or-stop`).

### Verification Gate (Hard Stop):
Before proceeding to edit or create any file, verify evidence:

| Evidence Status | Action |
|---|---|
| **Direct User Instruction (`[user]`)** | Approved to land. The user explicitly corrected or confirmed the rule. |
| **Reproducible Proof (`[code]` + `[runtime]`)** | Approved to land only if the cause is unambiguous and verifiable. |
| **Inferred / Speculative / Unsourced** | **HARD STOP.** Prefix `Invented (not approved):`. **DO NOT modify any file.** Present the lesson to the user and ask for confirmation first. |
| **User Disagrees or Rejects** | **ABORT.** Do not write to any skill or rule file. |

Done when: the lesson is one cited sentence backed by verified evidence OR the user has explicitly confirmed an invented lesson.

---

## 2. Find the Owner

Search existing skills or rules (descriptions first, then content) for the domain of the lesson. Pick **one** owner:

| Owner | Land in |
|---|---|
| Exact existing skill | That `SKILL.md` (or rule file) |
| Partial match | That skill/rule, smallest edit |
| Lesson is a general code/architecture convention | Project convention/knowledge file (e.g. [update-knowledge](../update-knowledge/SKILL.md) or `AGENTS.md` / `CLAUDE.md`) |
| Owner is vendored / third-party / read-only (e.g. in `.agents/vendored-skills.json` or external packages) | A project-owned skill/rule; leave upstream vendored files untouched |
| No owner | §4 create |

**Check for Duplicate or Stated Rules**:
If the owner already states the lesson, **take no action on file body** — the miss was invocation. Optionally sharpen that skill's `description` trigger so the next run loads it. Never paste duplicate restatements into the body.

Done when: you have one owner path, or a documented "already stated / description sharpened" outcome.

---

## 3. Patch the Owner (Safe & Minimal)

Apply the smallest change that would have prevented **this** failure:

- **Non-destructive**: Co-locate the durable rule under the existing relevant heading. Do not overwrite or delete unrelated instructions.
- **Trigger Sharpening**: If the agent never loaded the skill, sharpen the `description` frontmatter trigger that should have fired.
- **Universal, Not an Incident Log**: Keep it a timeless, reusable rule. Never copy-paste temporary session logs, ticket IDs, or one-off incident narratives into the rule body.
- **Canonical Only**: Write only to the canonical source file (do not write to symlinks).

Done when: a later agent loading the owner would follow the corrected rule without reading this chat.

---

## 4. Create Only When None Owns It

If no owner exists, create a new skill or rule in the detected configuration location:
- For skills: `<skills-dir>/<name>/SKILL.md` with standard frontmatter (`name`, `description`).
- Model-invoked `description` with clear triggers.
- Reusable pattern, not a one-off ticket diary.

Done when: the new file exists at that path, or you did not create because an existing owner was found.

---

## 5. Report to User

Always report clearly in your reply:
1. **Target File**: Exact file path patched or created.
2. **Action**: `Patched` | `Created` | `Skipped (already stated, sharpened description)`.
3. **The Landed Rule**: The exact one-sentence rule added.
4. **Citation Backing**: The source tag (`[user]`, `[runtime]`, etc.) that validated this change.

Done when: that report is presented in the final response.
