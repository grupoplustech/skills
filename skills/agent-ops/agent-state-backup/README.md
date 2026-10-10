# 🛡️ Agent Live State Backup & Disaster Recovery

Battle-tested procedure for creating safe, versioned Git mirrors and disaster recovery snapshots of an AI agent's active runtime directory (`~/.hermes`, `~/.openclaw`, etc.) without leaking secrets or corrupting SQLite WAL files.

## 🎯 Use Cases
* Daily automated backups of agent memory, skills, cron jobs, and config to a private Git repository.
* Preventing secrets (`.env`, auth tokens, API keys) from accidentally entering Git history.
* Safe handling of active SQLite databases (`state.db`) avoiding WAL-reset lockups.
* Fast disaster recovery from tarball or Git clone on a new server.

## 🛠️ Multi-Runtime Support
* Hermes Agent: `SKILL.md`
* Claude Code / Projects: `CLAUDE.md`
* Cursor: `CURSOR.mdc`
* Gemini AI Studio: `GEMINI.md`
* OpenAI GPTs: `GPT.md`
