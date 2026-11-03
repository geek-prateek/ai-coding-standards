
# 🧠 AI Coding Standards & Agent Skills

[![skills.sh](https://skills.sh/b/geek-prateek/ai-coding-standards)](https://skills.sh/geek-prateek/ai-coding-standards)

**Learn engineering principles. Apply them in context. Verify the outcome.**

A public collection of reusable, project-aware skills for AI coding agents and developers.

These skills help AI understand existing project conventions, make better engineering decisions, apply appropriate coding practices, and verify changes without introducing unnecessary complexity.

---

## 📑 Skills Catalog

### 🛡️ Governance & Discipline

| Skill | Description | Best For |
| :--- | :--- | :--- |
| **[`cite-or-stop`](./cite-or-stop/SKILL.md)** | Enforces evidence-backed claims, prevents repeated failed attempts, and provides structured handoffs when blocked. | Avoiding hallucinations, unsupported assumptions, and retry loops. |

### 🔄 Meta-Learning & Self-Healing

| Skill | Description | Best For |
| :--- | :--- | :--- |
| **[`lesson-to-skill`](./lesson-to-skill/SKILL.md)** | Converts confirmed errors, user corrections, and recurring problems into reusable instructions to help prevent the same mistakes in future tasks. | Continuous learning, error prevention, and improving AI agent behavior. |

### 🏗️ Coding Standards & Best Practices

| Skill | Description | Best For |
| :--- | :--- | :--- |
| **[`solid-principles`](./solid-principles/SKILL.md)** | Helps developers learn and apply SOLID principles. Analyzes existing code and suggests design improvements without introducing unnecessary abstractions. | Clean, maintainable, and extensible code. |
| **[`precision-and-rounding`](./precision-and-rounding/SKILL.md)** | Analyzes existing numeric types, rounding rules, calculations, and configurations before suggesting changes. Preserves established project behavior unless explicitly instructed otherwise. | Preventing precision loss, incorrect rounding, and calculation inconsistencies. |
| **[`database-query-patterns`](./database-query-patterns/SKILL.md)** | Analyzes database queries, ORM patterns, schemas, and indexes before recommending improvements. Helps identify inefficient queries while preserving existing data behavior. | Query optimization, database performance, and data correctness. |

> **Learn → Apply → Verify:** Understand the principle, apply it according to existing project conventions, and verify the outcome.

---

## 🚀 Quick Setup & Usage

### ⚡ Quick Install (Recommended)

Install AI coding skills directly from GitHub:

```bash
npx skills add geek-prateek/ai-coding-standards
```

Install a specific skill:

```bash
npx skills add geek-prateek/ai-coding-standards --skill precision-and-rounding
```

Install globally across projects:

```bash
npx skills add geek-prateek/ai-coding-standards -g
```

Browse available skills:

```bash
npx skills add geek-prateek/ai-coding-standards --list
```

Explore skills at [skills.sh](https://skills.sh).

### Option 1: Global Setup (Works Across All Projects)

Install once to make these skills available across projects.

#### Google Antigravity

```bash
# Windows (PowerShell)
cd $HOME\.gemini\config\skills
git clone https://github.com/geek-prateek/ai-coding-standards.git .
```

```bash
# macOS / Linux
cd ~/.gemini/config/skills
git clone https://github.com/geek-prateek/ai-coding-standards.git .
```

#### Claude Code

```bash
cd ~/.claude/skills
git clone https://github.com/geek-prateek/ai-coding-standards.git .
```

> **Note:** Skill discovery paths may vary by agent and version. The Skills CLI is the recommended installation method for supported agents.

---

### Option 2: Per-Project Setup

To use skills in a specific project, copy the required skill folders into your agent's supported skills directory.

Example:

```text
my-project/
├── .agents/
│   └── skills/
│       ├── cite-or-stop/
│       │   └── SKILL.md
│       ├── lesson-to-skill/
│       │   └── SKILL.md
│       ├── solid-principles/
│       │   └── SKILL.md
│       ├── precision-and-rounding/
│       │   └── SKILL.md
│       └── database-query-patterns/
│           └── SKILL.md
└── src/
```

#### Or via Git Submodule

```bash
git submodule add https://github.com/geek-prateek/ai-coding-standards.git .agents/skills/shared
```

Ensure your coding agent can discover the nested skill folders.

---

## 📂 Repository Layout

```text
ai-coding-standards/
├── README.md
├── cite-or-stop/
│   └── SKILL.md
├── lesson-to-skill/
│   └── SKILL.md
├── solid-principles/
│   └── SKILL.md
├── precision-and-rounding/
│   └── SKILL.md
└── database-query-patterns/
    └── SKILL.md
```

*Each skill may also contain supporting references, examples, and evaluation cases.*

---

## ➕ How to Add a New Skill

To keep the repository clean and scalable:

1. **Create a directory:** `<skill-name>/`
2. **Add `SKILL.md`:** Include valid YAML frontmatter.
3. **Define when to use it:** Describe the specific problem and activation criteria.
4. **Follow existing project conventions:** Avoid forcing patterns or changing established behavior without justification.
5. **Keep it generic:** Do not include proprietary code, credentials, internal URLs, or company-specific information.
6. **Add evaluations where useful:** Include practical scenarios to verify the skill's effectiveness.
7. **Update the catalog:** Add the new skill to the Skills Catalog.

Example `SKILL.md`:

```yaml
---
name: skill-name
description: >-
  Describe what the skill does and when to use it.
---

# Skill Title

## Learn
Explain the concept with practical examples.

## Apply
Analyze existing project conventions before suggesting changes.

## Verify
Validate correctness, compatibility, and edge cases.
```

> **Important:** Don't create a skill just because a programming concept exists. Create one when a recurring problem benefits from a specific, reusable workflow.

---

## 🤝 Contributing

Contributions, suggestions, and improvements are welcome!

Feel free to open an issue or submit a pull request to improve existing skills or propose new ones.

---

## 📄 License

See the repository's [LICENSE](LICENSE) file for licensing information.
