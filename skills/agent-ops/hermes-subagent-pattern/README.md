# 👥 Hermes Subagent Isolation & Orchestration Pattern

Architectural blueprint for designing and orchestrating autonomous subagents with isolated context windows, specialized system prompts, private memory stores, and clean supervisor delegation loops.

## 🎯 Use Cases
* Isolating heavy tasks (web scraping, codebase audits, report generation) to prevent polluting the primary assistant's context.
* Creating domain-specific subagents (e.g., DevOps specialist, QA engineer, Helpdesk bot) under dedicated profiles.
* Managing safe parent-child execution boundaries without infinite recursion.

## 🛠️ Multi-Runtime Support
* Hermes Agent: `SKILL.md`
* Claude Code / Projects: `CLAUDE.md`
* Cursor: `CURSOR.mdc`
* Gemini AI Studio: `GEMINI.md`
* OpenAI GPTs: `GPT.md`
