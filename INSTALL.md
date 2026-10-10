# 📦 Installation Guide

This gallery supports multiple AI agent environments. Follow the guide below for your platform.

---

## 1. 🦙 Hermes Agent

Hermes automatically scans `~/.hermes/skills/` recursively for any `SKILL.md` file.

### Option A: Install All Skills
```bash
git clone https://github.com/grupoplustech/skills.git ~/.hermes/skills/grupoplustech
```

### Option B: Install a Specific Category or Skill
```bash
# Example: Ham Radio skills only
mkdir -p ~/.hermes/skills/ham-radio
cp -r skills/ham-radio/* ~/.hermes/skills/ham-radio/
```

Verify in your Hermes session:
```text
/skills
```

---

## 2. 🤖 Claude / Claude Code / Projects

### For Claude Code (CLI)
Copy the `CLAUDE.md` file from any skill into your target project repository root:
```bash
cp skills/agent-ops/agent-state-backup/CLAUDE.md /path/to/my-project/CLAUDE.md
```

### For Claude Projects (Web)
1. Open your Project in [Claude.ai](https://claude.ai).
2. Go to **Set custom instructions**.
3. Paste the contents of `CLAUDE.md`.

---

## 3. ⚡ Cursor IDE

Cursor uses `.cursor/rules/` for contextual rule files (`.mdc`).

1. In your project workspace, create the rules directory:
   ```bash
   mkdir -p .cursor/rules
   ```
2. Copy the desired `CURSOR.mdc` file:
   ```bash
   cp skills/integrations/composio-sdk-quirks/CURSOR.mdc .cursor/rules/composio-quirks.mdc
   ```

---

## 4. 💎 Google Gemini AI Studio

1. Navigate to [Google AI Studio](https://aistudio.google.com/).
2. Start a new Chat or Structured Prompt.
3. In the **System Instructions** box, paste the contents of `GEMINI.md`.

---

## 5. 💬 OpenAI / ChatGPT Custom GPTs

1. Go to [ChatGPT](https://chatgpt.com) -> **Explore GPTs** -> **Create a GPT**.
2. Go to the **Configure** tab.
3. Paste the contents of `GPT.md` into the **Instructions** section.
