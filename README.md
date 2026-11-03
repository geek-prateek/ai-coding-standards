
# 🧠 Agent Skills Toolkit

A curated collection of modular, production-ready **Agent Skills** designed for modern AI coding assistants (Google Antigravity, Claude Code, Cursor, Windsurf, etc.).

These skills act as operational guardrails and behavioral protocols for AI agents—enforcing citation of evidence, cutting off hallucination and retry loops, turning mistakes into permanent self-learning rules, and helping AI follow existing project coding standards and patterns.

---

## 📑 Skills Catalog

### 🛡️ Governance & Discipline

| Skill / Command | Description | Best For |
| :--- | :--- | :--- |
| **[`cite-or-stop`](./cite-or-stop/SKILL.md)** | Enforces verifiable source citations (`[code]`, `[runtime]`, etc.) for every factual claim. Automatically cuts off execution after 2 failed retries on the same blocker and provides a structured handoff. | Preventing retry loops, unverified assumptions, and hallucinations. |

### 🔄 Meta-Learning & Self-Healing

| Skill / Command | Description | Best For |
| :--- | :--- | :--- |
| **[`lesson-to-skill`](./lesson-to-skill/SKILL.md)** | Turns confirmed errors, user corrections, and root-cause blockers into persistent agent skills or rules so the mistake is never repeated in future runs. | Continuous improvement, post-mortems, knowledge retention. |

### 🏗️ Coding Standards & Best Practices

| Skill / Command | Description | Best For |
| :--- | :--- | :--- |
| **[`solid-principles`](./solid-principles/SKILL.md)** | Helps developers learn and apply SOLID principles. Analyzes existing code, identifies design problems, and suggests improvements without introducing unnecessary abstractions. | Writing clean, maintainable, and extensible code while following existing project conventions. |
| **[`precision-and-rounding`](./precision-and-rounding/SKILL.md)** | Analyzes existing numeric types, calculation flows, rounding rules, and configurations before suggesting changes. Preserves the project's established rounding behavior unless a change is explicitly required. | Avoiding precision loss, incorrect rounding, and calculation inconsistencies across applications. |
| **[`database-query-patterns`](./database-query-patterns/SKILL.md)** | Analyzes existing database queries, ORM patterns, schema, and indexes before recommending improvements. Helps identify N+1 queries, inefficient data access, and performance issues without changing existing behavior. | Writing efficient database queries, improving performance, and maintaining data correctness. |

> **Learn → Apply → Verify:** Coding standards skills help developers understand concepts, apply them to existing projects, and verify changes while preserving established behavior.

*(As new skills are added, document them in these tables.)*

---

## 🚀 Quick Setup & Usage

### Option 1: Global Setup (Works Across All Projects)

Install once to make these skills available everywhere on your machine.

#### Google Antigravity

Clone or link into your global Antigravity config directory:

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

> Note: Agent skill discovery paths and installation methods may vary by tool. Ensure the individual skill folders are placed where your coding assistant discovers skills.

---

### Option 2: Per-Project Setup

If you want to use specific skills in a single codebase:

1. Create an `.agents/skills` folder at your project root.
2. Copy the desired skill folder(s) into it:

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

#### Or via Git Submodule (Recommended for teams):

```bash
git submodule add https://github.com/geek-prateek/ai-coding-standards.git .agents/skills/shared
```

---

## 📂 Repository Layout

```text
.
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

*Skills may also contain supporting references, examples, and evaluations.*

---

## ➕ How to Add a New Skill

To keep the repository clean and scalable:

1. **Create a Directory:** `<skill-name>/`
2. **Add `SKILL.md`:** Include valid YAML frontmatter at the top:

   ```yaml
   ---
   name: <skill-name>
   description: >-
     When to use this skill, what problems it solves, and specific trigger keywords.
   ---

   # Skill Title

   Detailed workflow, rules, and procedures...
   ```

3. **Keep it Generic:** Do not include project-specific credentials, private URLs, or company internal names.
4. **Update Catalog:** Add a new row to the [Skills Catalog](#-skills-catalog) table above.

---

## 📄 License

Distributed under the [MIT License](LICENSE).
