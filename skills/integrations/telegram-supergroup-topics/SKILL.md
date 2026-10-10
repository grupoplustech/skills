---
name: telegram-supergroup-topics
description: Discovery, mapping, and message routing for Telegram Supergroup Forum Topics. Covers extracting message_thread_id, webhook configuration, and cron delivery targeting.
version: 1.0.0
metadata:
  category: integrations
  tags: [telegram, bot, api, topics, supergroups, notifications, integrations]
---

# Telegram Supergroup Forum Topics Discovery & Routing 📢🧵

## ⚙️ The Problem: Hidden Thread IDs in Telegram UI

Telegram Forum supergroups organize conversations into Topics. However, the standard Telegram UI does not display numerical `message_thread_id` values. Without this ID, bots default to posting in the "General" thread.

---

## 🔍 Discovery Handshake Protocol

To extract the exact `thread_id`:

1. **Send a Test Message:** Have a user or bot send a message inside the desired topic thread (e.g., `#ping`).
2. **Poll `getUpdates` via Bot API:**
```bash
curl -s "https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates" | jq '.result[] | select(.message.message_thread_id != null) | {chat_id: .message.chat.id, thread_id: .message.message_thread_id, text: .message.text}'
```
3. **Capture the `message_thread_id`:** The returned integer is the permanent identifier for that topic.

---

## 🚀 Sending Messages to a Specific Topic

When calling `sendMessage`, supply both `chat_id` and `message_thread_id`:

```bash
curl -s -X POST "https://api.telegram.org/bot<YOUR_BOT_TOKEN>/sendMessage"   -d "chat_id=<CHAT_ID>"   -d "message_thread_id=<THREAD_ID>"   -d "text=🚨 <b>Automated Alert:</b> Database backup completed successfully."   -d "parse_mode=HTML"
```
