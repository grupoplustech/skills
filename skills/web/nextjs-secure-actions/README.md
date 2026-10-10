# 🛡️ Next.js Secure Server Actions Architecture & Audit

Security blueprint and validation pattern for hardening Next.js Server Actions against authorization bypass, IDOR (Insecure Direct Object Reference), CSRF, and unvalidated payloads.

## 🎯 Use Cases
* Hardening `'use server'` mutations against malicious direct POST requests.
* Validating input parameters at runtime with Zod before processing database mutations.
* Enforcing user session authentication and permission gates on the server boundary.
* Preventing Server Action timing attacks and unthrottled abuse with rate-limiting.

## 🛠️ Multi-Runtime Support
* Hermes Agent: `SKILL.md`
* Claude Code / Projects: `CLAUDE.md`
* Cursor: `CURSOR.mdc`
* Gemini AI Studio: `GEMINI.md`
* OpenAI GPTs: `GPT.md`
