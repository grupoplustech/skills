---
name: stdio-mcp-server-builder
description: Guide and boilerplate for developing stdio Model Context Protocol (MCP) servers in Node.js and Python. Covers JSON-RPC 2.0 framing, stdin/stdout buffering, and avoiding log contamination.
version: 1.0.0
metadata:
  category: agent-ops
  tags: [mcp, stdio, json-rpc, nodejs, python, tools, hermes, claude]
---

# Stdio Model Context Protocol (MCP) Server Engineering 🔌⚙️

## ⚠️ The Golden Rule of Stdio MCP

In a stdio MCP server, **`stdout` belongs exclusively to the JSON-RPC protocol parser**.
If your application, dependencies, or debugging statements call `console.log()` or `print()` to stdout, the JSON-RPC framing breaks instantly, causing `JSONParseError` on the client agent.
* **All logs, traces, and debug statements must be directed to `stderr` (`console.error()` or `sys.stderr.write()`).**

---

## 🛠️ Zero-Dependency Node.js MCP Server Template

```javascript
#!/usr/bin/env node

const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
  terminal: false
});

function logDebug(msg) {
  // Always log to stderr!
  process.stderr.write(`[MCP-DEBUG] ${msg}
`);
}

function sendResponse(id, result, error = null) {
  const payload = {
    jsonrpc: "2.0",
    id,
    ...(error ? { error } : { result })
  };
  process.stdout.write(JSON.stringify(payload) + "\n");
}

rl.on('line', (line) => {
  if (!line.trim()) return;
  try {
    const req = JSON.parse(line);
    const { id, method, params } = req;
    logDebug(`Received method: ${method}`);

    if (method === "tools/list") {
      sendResponse(id, {
        tools: [
          {
            name: "echo_tool",
            description: "Echoes back the received message",
            inputSchema: {
              type: "object",
              properties: { message: { type: "string" } },
              required: ["message"]
            }
          }
        ]
      });
    } else if (method === "tools/call") {
      const toolName = params?.name;
      if (toolName === "echo_tool") {
        sendResponse(id, {
          content: [{ type: "text", text: `Echo: ${params.arguments?.message}` }]
        });
      } else {
        sendResponse(id, null, { code: -32601, message: "Tool not found" });
      }
    }
  } catch (err) {
    logDebug(`Parse error: ${err.message}`);
  }
});
```
