---
name: agent-state-backup
description: Safe, automated Git mirroring and disaster recovery backups for AI agent runtime directories (~/.hermes). Prevents secret leaks, avoids SQLite WAL locks, and maintains clean state mirrors.
version: 1.1.0
metadata:
  category: agent-ops
  tags: [devops, backup, hermes, disaster-recovery, git, sqlite, agent-ops]
---

# AI Agent Live State Backup & Disaster Recovery 🛡️💾

## ⚠️ The Three Critical Hazards of Agent Backups

1. **Secret Leakage:** Agents store OAuth tokens, Telegram bot tokens, and API keys in `.env` and subdirectories (`secrets/`, `keys/`). A naive `git add .` publishes secrets to the remote repo.
2. **SQLite WAL Corruption:** Running tools or naive tarballs against active SQLite databases (such as `~/.hermes/state.db`) while the gateway is active can unlink WAL files (`DeletedWalGenerationError`), hanging the agent.
3. **Bloat from Cache & Logs:** Subagent execution caches, audio recordings, and temporary scratch files easily exceed hundreds of megabytes.

---

## 🔒 Safe `.gitignore` Template for Agent Runtimes

Place this in the agent runtime root (`~/.hermes/.gitignore`):

```gitignore
# NEVER COMMIT SECRETS OR SENSITIVE TOKENS
.env*
*.env
secrets/
keys/
credentials.json
*.key
*.pem

# SENSITIVE CACHES & MEDIA
cache/scratch/
audio_cache/
*.mp3
*.wav
*.ogg

# RUNTIME STATE & DATABASES
state.db*
*.sqlite*
logs/
run/
*.pid

# PLATFORM ARTIFACTS
__pycache__/
*.pyc
node_modules/
```

---

## 🔄 Daily Backup Sync Script

```bash
#!/usr/bin/env bash
set -euo pipefail

TARGET_DIR="${HOME}/.hermes"
BACKUP_REPO_DIR="${HOME}/backups/hermes-state"

mkdir -p "${BACKUP_REPO_DIR}"
cd "${TARGET_DIR}"

# 1. Sync tracked config, memories, and skills (ignoring excluded files)
rsync -av --delete   --exclude-from="${TARGET_DIR}/.gitignore"   "${TARGET_DIR}/" "${BACKUP_REPO_DIR}/"

# 2. Commit and push
cd "${BACKUP_REPO_DIR}"
if [[ -d .git ]]; then
  git add -A
  if ! git diff-index --quiet HEAD --; then
    git commit -m "chore(backup): automated state snapshot $(date -u +'%Y-%m-%d %H:%M:%SZ')"
    git push origin main
  fi
fi
```
