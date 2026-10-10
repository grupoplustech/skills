# Contributing to Grupo Plus Tech Skills Gallery

Thank you for your interest in improving and growing this open-source agent skills gallery!

## 🎯 Our Goal
We curate skills that:
1. **Solve real, complex engineering problems** (not generic prompts like "write an email").
2. **Offer technical depth** (edge cases, pitfalls, concrete commands, scripts, and error diagnostics).
3. **Support multiple AI agent runtimes** (Hermes, Claude, Cursor, Gemini, GPT).

---

## 📁 Skill Structure Requirements

Every skill must live in a subdirectory under its relevant category (e.g. `skills/agent-ops/<skill-name>/`) and contain:

1. `README.md`: Human-readable guide explaining the problem, prerequisites, architecture, and examples.
2. `SKILL.md`: Hermes Agent specification with YAML frontmatter (`name`, `description`, `version`, `tags`).
3. `CLAUDE.md`: Claude Code / Anthropic Projects prompt.
4. `CURSOR.mdc`: Cursor Rules format (`description`, `globs`, guidelines).
5. `GEMINI.md`: Google Gemini system instruction format.
6. `GPT.md`: OpenAI Custom GPT instruction format.

---

## 🛡️ Security & Privacy Checklist (Mandatory)

Before opening a Pull Request, ensure:
* [ ] **ZERO Credentials:** No real API keys, bearer tokens, passwords, or hashes.
* [ ] **Sanitized Variables:** Use clear placeholders (e.g., `YOUR_TELEGRAM_BOT_TOKEN`, `YOUR_RADIO_ID`, `example.com`).
* [ ] **No Private Domain Names / IPs:** Use generic domains or private RFC1918 ranges (`192.168.1.x`, `10.0.0.x`).
* [ ] **Empirical Verification:** Commands and scripts must have been tested in a real terminal environment.

---

## 🚀 How to Submit

1. **Fork** the repository.
2. **Create a feature branch**:
   ```bash
   git checkout -b feat/new-skill-lora-tuning
   ```
3. **Add your files** following the template structure.
4. **Commit and Push**:
   ```bash
   git commit -m "feat(skills): add LoRA tuning automation skill"
   git push origin feat/new-skill-lora-tuning
   ```
5. **Open a Pull Request** describing the motivation, tested environments, and use cases.
