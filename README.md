# 🧠 AI Coding Standards & Agent Skills

[![skills.sh](https://skills.sh/b/geek-prateek/ai-coding-standards)](https://skills.sh/geek-prateek/ai-coding-standards)

**Understand. Learn. Apply. Verify. Improve.**

A collection of reusable, project-aware skills that help AI agents understand requirements, make better engineering decisions, reduce hallucinations, and deliver reliable results.

Project-independent, language-agnostic, composable, and token-conscious.

---

## 📑 Skills Catalog

| Skill | Purpose |
| :--- | :--- |
| **[`prompt-intelligence`](./prompt-intelligence/SKILL.md)** | Detect missing requirements, resolve ambiguity, discover scenarios, optimize prompts, and verify outcomes. |
| **[`cite-or-stop`](./cite-or-stop/SKILL.md)** | Enforce evidence-backed claims, reduce hallucinations, and prevent repeated failed attempts. |
| **[`lesson-to-skill`](./lesson-to-skill/SKILL.md)** | Convert confirmed mistakes and corrections into reusable preventive instructions. |
| **[`solid-principles`](./solid-principles/SKILL.md)** | Apply SOLID principles without unnecessary abstractions or overengineering. |
| **[`precision-and-rounding`](./precision-and-rounding/SKILL.md)** | Preserve numeric precision, rounding consistency, and existing calculation behavior. |
| **[`database-query-patterns`](./database-query-patterns/SKILL.md)** | Optimize database queries, ORM patterns, and performance while preserving data correctness. |

## 🚀 Installation

**Install all skills:**

```bash
npx skills add geek-prateek/ai-coding-standards
```

**Install a specific skill:**

```bash
npx skills add geek-prateek/ai-coding-standards --skill prompt-intelligence
```

**Install globally across projects:**

```bash
npx skills add geek-prateek/ai-coding-standards -g
```

**List available skills:**

```bash
npx skills add geek-prateek/ai-coding-standards --list
```

Alternatively, copy the required skill folders into your agent's supported skills directory or use a Git submodule:

```bash
git submodule add https://github.com/geek-prateek/ai-coding-standards.git .agents/skills/shared
```

Skill discovery paths vary by agent and version. Ensure your agent supports nested skill directories. The Skills CLI is recommended for supported agents.

## 🤖 Usage

Invoke a specific skill:

```text
Use prompt-intelligence to analyze this requirement
before implementation.
```

Or add the following to your global agent instructions:

```text
Automatically use relevant installed skills.
Inspect existing context before making changes.
Identify consequential gaps, risks, and edge cases.
Follow project conventions and preserve existing behavior.
Ground claims in evidence and verify outcomes.
Learn from confirmed mistakes.
Avoid unnecessary complexity and token consumption.
```

## 🔄 Skill Workflow

| Stage | Skill |
| :--- | :--- |
| Understand & Discover | `prompt-intelligence` |
| Apply & Implement | Relevant coding standards |
| Verify & Validate | `cite-or-stop` |
| Learn & Improve | `lesson-to-skill` |

Skills work independently or together. Apply only what the task requires.

## 📂 Repository Structure

```text
ai-coding-standards/
├── README.md
├── prompt-intelligence/
│   ├── SKILL.md
│   └── EVALUATIONS.md
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

## 🎯 Core Principles

- **Context First:** Understand existing behavior before making changes.
- **Evidence Over Assumptions:** Never fabricate facts, citations, or test results.
- **Scenario Coverage:** Consider relevant edge cases and regression risks.
- **Simplicity:** Avoid unnecessary changes, abstractions, and token usage.
- **Privacy:** Never publish proprietary code, credentials, private data, or internal references.
- **Continuous Improvement:** Learn from verified outcomes and confirmed mistakes.

## 🧪 Evaluation

Measure effectiveness through requirement coverage, factual accuracy, functional correctness, regression testing, token efficiency, and reduced rework.

See [Prompt Intelligence Evaluations](./prompt-intelligence/EVALUATIONS.md).

Skills improve AI reliability but do not guarantee hallucination-free or error-free results.

## 🤝 Contributing

New skills and improvements are welcome.

- Address a recurring, reusable problem.
- Include a `SKILL.md` with valid YAML frontmatter.
- Define activation criteria, instructions, and verification rules.
- Keep examples generic and privacy-safe.
- Add evaluations where useful and update the catalog.

Follow existing conventions and avoid duplicating skill responsibilities.

## 📄 License

See [LICENSE](LICENSE).

---

**Better prompts. Better decisions. Verified outcomes.**
