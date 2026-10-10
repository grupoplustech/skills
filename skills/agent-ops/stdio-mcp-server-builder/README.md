# 🔌 Stdio Model Context Protocol (MCP) Server Engineering

Architectural guide and zero-dependency template for building robust stdio Model Context Protocol (MCP) servers in Node.js or Python, exposing internal tools, CLIs, and local databases to AI agents (Hermes, Claude Desktop, Cursor).

## 🎯 Use Cases
* Exposing private APIs, CLI utilities, or databases to AI models via standard input/output.
* Avoiding stream corruption: keeping stdout strictly reserved for JSON-RPC 2.0 messages (redirecting logs to stderr).
* Implementing token authentication and input schema validation for custom tools.

## 🛠️ Multi-Runtime Support
* Hermes Agent: `SKILL.md`
* Claude Code / Projects: `CLAUDE.md`
* Cursor: `CURSOR.mdc`
* Gemini AI Studio: `GEMINI.md`
* OpenAI GPTs: `GPT.md`
