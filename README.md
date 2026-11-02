# 🧠 Agent Skills Toolkit

A curated collection of modular, production-ready **Agent Skills** designed for modern AI coding assistants (Google Antigravity, Claude Code, Cursor, Windsurf, etc.).

These skills act as operational guardrails and behavioral protocols for AI agents—enforcing citation of evidence, cutting off hallucination and retry loops, and turning mistakes into permanent self-learning rules.

---

## 📑 Skills Catalog

### 🛡️ Governance & Discipline
| Skill / Command | Description | Best For |
| :--- | :--- | :--- |
| **[`cite-or-stop`](./skills/cite-or-stop/SKILL.md)** | Enforces verifiable source citations (`[code]`, `[runtime]`, etc.) for every factual claim. Automatically cuts off execution after 2 failed retries on the same blocker and provides a structured handoff. | Preventing retry loops, unverified assumptions, and hallucinations. |

### 🔄 Meta-Learning & Self-Healing
| Skill / Command | Description | Best For |
| :--- | :--- | :--- |
| **[`lesson-to-skill`](./skills/lesson-to-skill/SKILL.md)** | Turns confirmed errors, user corrections, and root-cause blockers into persistent agent skills or rules so the mistake is never repeated in future runs. | Continuous improvement, post-mortems, knowledge retention. |

*(As new skills are added, document them in this table)*

---

## 🚀 Quick Setup & Usage

### Option 1: Global Setup (Works Across All Projects)
Install once to make these skills available everywhere on your machine.

#### Google Antigravity
Clone or link into your global Antigravity config directory:
```bash
# Windows (PowerShell)
cd $HOME\.gemini\config\skills
git clone https://github.com/<YOUR_USERNAME>/<REPO_NAME>.git .

# macOS / Linux
cd ~/.gemini/config/skills
git clone https://github.com/<YOUR_USERNAME>/<REPO_NAME>.git .
```

#### Claude Code
```bash
cd ~/.claude/skills
git clone https://github.com/<YOUR_USERNAME>/<REPO_NAME>.git .
```

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
   │       └── lesson-to-skill/
   │           └── SKILL.md
   └── src/
   ```

#### Or via Git Submodule (Recommended for teams):
```bash
git submodule add https://github.com/<YOUR_USERNAME>/<REPO_NAME>.git .agents/skills/shared
```

---

## 📂 Repository Layout

```text
.
├── README.md
└── skills/
    ├── cite-or-stop/
    │   └── SKILL.md
    ├── lesson-to-skill/
    │   └── SKILL.md
    └── <new-skill-name>/
        └── SKILL.md
```

---

## ➕ How to Add a New Skill

To keep the repository clean and scalable:

1. **Create a Directory:** `skills/<skill-name>/`
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
