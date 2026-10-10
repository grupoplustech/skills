---
name: composio-sdk-quirks
description: Troubleshooting playbook for Composio SDK 1.0+ and MCP tool router. Solves project mismatch errors, zero-account sync bugs, and 401/502 API triage.
version: 1.0.0
metadata:
  category: integrations
  tags: [composio, mcp, sdk, tools, troubleshooting, integrations]
---

# Composio SDK & MCP Tool Router Quirks 🧩⚠️

## 🔍 Critical Pitfalls & Solutions

### 1. The "Zero Connected Accounts" Ghost Bug
* **Symptom:** `composio whoami` shows your user, but `composio apps` or connected accounts returns `0 accounts` even though OAuth was completed in the web dashboard.
* **Root Cause:** In SDK 1.0+, connections are scoped by `project_id`. If the local CLI created a default project different from the web UI active project, accounts do not sync.
* **Fix:**
```bash
# Check current active project
composio projects list
# Set active project explicitly
composio projects set <PROJECT_ID>
```

---

### 2. Triaging 401 Unauthorized vs 502 Gateway Errors
* **401 Unauthorized:** Indicates token expiry at the third-party provider (e.g., Google OAuth refresh token invalidated). Re-authenticate via `composio add <app>`.
* **502 Bad Gateway:** Composio backend proxy failed to contact the downstream API. Do not re-authenticate immediately; implement exponential backoff retry logic.
