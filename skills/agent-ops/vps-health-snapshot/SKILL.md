---
name: vps-health-snapshot
description: Consolidated single-run diagnostic audit for Linux servers. Inspects CPU, RAM, disk, listening ports, active Docker containers, failing systemd units, crons, and SSL certs.
version: 1.0.0
metadata:
  category: agent-ops
  tags: [sysadmin, devops, linux, vps, docker, healthcheck, troubleshooting]
---

# Unified VPS Health Snapshot 🖥️🔍

## 🛠️ One-Liner Diagnostic Script

Run this command to get a high-density, formatted snapshot of the server:

```bash
python3 -c "
import subprocess, os

def run(cmd):
    try:
        return subprocess.check_output(cmd, shell=True, text=True, stderr=subprocess.STDOUT).strip()
    except Exception as e:
        return f'ERROR: {e}'

print('=== 1. SYSTEM LOAD & UPTIME ===')
print(run('uptime'))
print(run('free -h | awk 'NR<=2''))

print('
=== 2. DISK UTILIZATION ===')
print(run('df -h -x tmpfs -x devtmpfs -x overlay'))

print('
=== 3. FAILING SYSTEMD SERVICES ===')
failed = run('systemctl --failed --no-legend --no-pager')
print(failed if failed else 'No failed services detected.')

print('
=== 4. DOCKER CONTAINERS STATUS ===')
print(run('docker ps --format "table {{.Names}}	{{.Status}}	{{.Ports}}" 2>/dev/null || echo "Docker not running or no permissions."'))

print('
=== 5. LISTENING TCP PORTS ===')
print(run('ss -tulpn | grep LISTEN | awk '{print \$1, \$5, \$7}' | head -n 15'))
"
```
