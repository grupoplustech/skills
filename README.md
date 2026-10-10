# 🧠 Grupo Plus Tech · Community Agent Skills Gallery

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Hermes Agent](https://img.shields.io/badge/Hermes-Compatible-6366f1.svg)](https://hermes-agent.nousresearch.com/)
[![Claude Code](https://img.shields.io/badge/Claude-Code%20%2F%20Projects-d97706.svg)](https://claude.ai)
[![Cursor](https://img.shields.io/badge/Cursor-Rules%20MDC-000000.svg)](https://cursor.com)
[![Gemini](https://img.shields.io/badge/Google-Gemini%20Studio-4285f4.svg)](https://aistudio.google.com/)
[![ChatGPT](https://img.shields.io/badge/OpenAI-Custom%20GPTs-10a37f.svg)](https://chatgpt.com)

A curated, production-tested gallery of open-source agent skills, system protocols, and operational blueprints. Built by **[Grupo Plus Tech](https://grupoplustech.com)** for developers, sysadmins, and amateur radio operators who orchestrate AI agents across different execution environments.

Every skill in this repository is designed as **multi-runtime**, providing ready-to-use definitions for:
* 🦙 **Hermes Agent** (`SKILL.md`)
* 🤖 **Claude / Claude Code / Projects** (`CLAUDE.md`)
* ⚡ **Cursor IDE** (`CURSOR.mdc`)
* 💎 **Google Gemini AI Studio** (`GEMINI.md`)
* 💬 **ChatGPT / Custom GPTs** (`GPT.md`)

---

## 🧭 Repository Tree & Catalog

```text
skills/
├── 📻 ham-radio/
│   ├── dmr-linux-codeplug/           # Native Linux DMR programming (qdMR, QLog, Codeplug vs User DB)
│   ├── hf-digital-modes/             # HF Digital Modes (FT8, JS8Call, CAT Control CI-V / Rigctl)
│   └── space-weather-hf-propagation/ # Real-time NOAA solar metrics (SFI, Kp, flares) & HF band forecast
├── 🛠️ agent-ops/
│   ├── agent-state-backup/           # Safe Git versioning & DR snapshots for live AI agents without leaks
│   ├── hermes-subagent-pattern/      # Multi-agent orchestration pattern (profiles, delegation, lifecycle)
│   ├── stdio-mcp-server-builder/     # Zero-dependency stdio MCP server builder in Node.js & Python
│   └── vps-health-snapshot/          # Single-run server diagnostics (Docker, SSL, Ports, Cron, RAM)
├── 🌐 web/
│   ├── web-accessibility-audit/      # WCAG 2.2 AA accessibility auditor for Next.js/React & contrast math
│   └── nextjs-secure-actions/        # Security hardening for Next.js Server Actions (IDOR, Zod, auth)
└── 🔌 integrations/
    ├── telegram-supergroup-topics/   # Telegram Forum Topics auto-discovery and scheduled thread delivery
    ├── composio-sdk-quirks/          # Diagnostics for Composio SDK 1.0+ project mismatch & MCP routing
    └── nextjs-protected-screenshots/ # Headless session-injected Playwright audits for protected Next.js apps
```

---

## 📋 Skill Matrix & Capabilities

| Category | Skill | Functions / Capabilities | Runtime Compatibility |
| :--- | :--- | :--- | :--- |
| **Ham Radio** | [`dmr-linux-codeplug`](skills/ham-radio/dmr-linux-codeplug/) | Codeplug architecture, qdMR setup, OpenGD77/Baofeng/AnyTone quirks, QLog sync, udev rules | Hermes, Claude, Cursor, Gemini, GPT |
| **Ham Radio** | [`hf-digital-modes`](skills/ham-radio/hf-digital-modes/) | WSJT-X, JTDX, CI-V protocol debugging, ALSA audio loopbacks, ALC & PTT troubleshooting | Hermes, Claude, Cursor, Gemini, GPT |
| **Ham Radio** | [`space-weather-hf-propagation`](skills/ham-radio/space-weather-hf-propagation/) | NOAA SWPC live API ingestion, Planetary Kp, Solar Flux (SFI), ionospheric MUF band forecast | Hermes, Claude, Cursor, Gemini, GPT |
| **Agent Ops** | [`agent-state-backup`](skills/agent-ops/agent-state-backup/) | Safe `.gitignore` patterns, Git automated sync, zero secret leaks, SQLite WAL lock prevention | Hermes, Claude, Cursor, Gemini, GPT |
| **Agent Ops** | [`hermes-subagent-pattern`](skills/agent-ops/hermes-subagent-pattern/) | Isolated personas, state boundaries, delegation loops, background monitor patterns | Hermes, Claude, Cursor, Gemini, GPT |
| **Agent Ops** | [`stdio-mcp-server-builder`](skills/agent-ops/stdio-mcp-server-builder/) | JSON-RPC 2.0 framing, stdin/stdout buffering, stream isolation (logs to stderr), tool schemas | Hermes, Claude, Cursor, Gemini, GPT |
| **Agent Ops** | [`vps-health-snapshot`](skills/agent-ops/vps-health-snapshot/) | Unified terminal audit: Docker status, open listening ports, SSL cert expiry, cron jobs | Hermes, Claude, Cursor, Gemini, GPT |
| **Web Dev** | [`web-accessibility-audit`](skills/web/web-accessibility-audit/) | WCAG 2.2 AA contrast formulas, keyboard navigation, semantic landmarks, ARIA audit | Hermes, Claude, Cursor, Gemini, GPT |
| **Web Dev** | [`nextjs-secure-actions`](skills/web/nextjs-secure-actions/) | Audits `'use server'` actions against authorization bypass, IDOR vulnerabilities & Zod validation | Hermes, Claude, Cursor, Gemini, GPT |
| **Integrations** | [`telegram-supergroup-topics`](skills/integrations/telegram-supergroup-topics/) | Extract hidden Telegram `thread_id`, route scheduled messages and crons to specific topics | Hermes, Claude, Cursor, Gemini, GPT |
| **Integrations** | [`composio-sdk-quirks`](skills/integrations/composio-sdk-quirks/) | Fix zero-account listing bug, project mismatch, 401 vs 502 triage in Composio Tool Router | Hermes, Claude, Cursor, Gemini, GPT |
| **Integrations** | [`nextjs-protected-screenshots`](skills/integrations/nextjs-protected-screenshots/) | Automated visual QA with Playwright injecting auth cookies and bypass tokens in Next.js apps | Hermes, Claude, Cursor, Gemini, GPT |

---


---

## 🛡️ Filosofía de Diseño: Anti-Bloat y Carga Responsable
*(Inspirado en el análisis de Fazt Code y Dax de OpenCode sobre la saturación de contexto)*

Muchos repositorios populares de skills cometen el error de empujar **mega-packs de 50+ archivos Markdown**. Esto degrada el rendimiento de los modelos modernos por tres razones críticas:
1. **Contaminación de Contexto (Trigger Polución):** Cada skill registrado gasta tokens en el arranque solo con su descripción. Si la descripción es ambigua, el agente lo auto-invoca sin necesidad, llenando la ventana de contexto de texto estático.
2. **Restricciones que Limitan la Inteligencia del Modelo:** Forzar reglas rígidas pensadas para modelos antiguos ahoga la capacidad de modelos avanzados (Claude 3.7, Gemini 2.5, GPT-4.5) que ya resuelven el problema de forma nativa ("vainilla").
3. **Falsas Métricas de Estrellas:** Decenas de miles de estrellas en GitHub no garantizan utilidad en tu terminal diario.

### 🎯 Principios de este Repositorio:
* **Instalación Granular, No Bundles Ciegos:** Instala únicamente el skill que resuelve tu problema actual en tu proyecto.
* **Ingeniería y Protocolos, No Prose Prompting:** Nuestros skills no dicen *"sé un programador experto"*; entregan comandos reproducibles, endpoints de NOAA, fórmulas de WCAG, udev rules y protocolos de hardware.
* **Descripciones con Triggers Precisos:** Cada skill define exactamente cuándo activarse y cuándo mantenerse en reposo.

## 🚀 Quickstart & Installation

See [**INSTALL.md**](INSTALL.md) for full instructions tailored to each platform.

### For Hermes Agent
```bash
# Clone directly into your Hermes skills directory
cd ~/.hermes/skills
git clone https://github.com/grupoplustech/skills.git grupoplustech-skills
```
Hermes will automatically index every `SKILL.md` in the directory.

### For Claude Code
Symlink or copy the `CLAUDE.md` from the desired skill into your project root or `~/.claude/skills/`.

### For Cursor
Copy `CURSOR.mdc` into `.cursor/rules/<skill-name>.mdc` in your workspace.

### For Gemini AI Studio / OpenAI Custom GPTs
Copy the contents of `GEMINI.md` or `GPT.md` directly into the System Instructions / Instructions field of your agent.

---

## 🤝 Contributing

We welcome additions, fixes, and community contributions!
* Want to contribute a new skill? Check [**CONTRIBUTING.md**](CONTRIBUTING.md).
* Have a radio, web, or agent infrastructure pattern that solved a tricky bug? Send a Pull Request!
* Please ensure you include all multi-runtime files (`SKILL.md`, `CLAUDE.md`, `CURSOR.mdc`, `GEMINI.md`, `GPT.md`) and redact any private API keys or personal identifiers.

---

## 📄 License

Distributed under the **MIT License**. Free for commercial and personal use.
Maintained with ❤️ by [Grupo Plus Tech](https://grupoplustech.com).
