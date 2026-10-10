---
name: hermes-subagent-pattern
description: Architecture and execution pattern for isolated subagents with independent context, dedicated Hermes profiles, task delegation, and verified handoffs.
version: 1.0.0
metadata:
  category: agent-ops
  tags: [hermes, subagents, multi-agent, delegation, architecture, prompt-engineering]
---

# Hermes Subagent Isolation Pattern 👥🤖

## 📐 Core Architecture

In multi-agent systems, the supervisor agent must remain responsive and concise. Heavy reasoning or multi-step execution belongs to isolated child agents:

1. **Context Boundary:** Subagents spawn with a clean slate. They inherit zero conversation history from the parent turn, preventing context pollution.
2. **Explicit Background:** All necessary paths, constraints, and target outputs must be explicitly passed in the subagent's invocation context.
3. **Verifiable Deliverables:** Children are self-reporting; the parent agent must verify generated artifacts (files created, HTTP status, exit codes) before confirming success to the end user.

---

## ⚙️ Configuration & Profile Structure

Under `~/.hermes/profiles/<subagent-name>/`:
```text
~/.hermes/profiles/devops/
├── config.yaml          # Profile-specific model, timeout, and tool configuration
├── memories/
│   ├── MEMORY.md        # Specialized facts and guidelines
│   └── USER.md          # User operational constraints
└── skills/              # Specialized domain skills for this subagent
```

### Delegation Invocation Example
```python
delegate_task(
    tasks=[
        {
            "goal": "Audit Nginx configuration and verify SSL certificate expiration dates",
            "context": "Server is Ubuntu 24.04. Check /etc/nginx/sites-enabled/ and certbot certificates. Produce a summary markdown report in /tmp/ssl-audit.md."
        }
    ]
)
```
