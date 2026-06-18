---
title: Telegram Bot
---
# Telegram Bot
Basic Telegram Bot connection for your IOT projects. You need to get your own `API_TOKEN` in official Telegram Bot `BotFather`.

---
### `TelegramBot(token, auth_chat_id)`
To create TelegramBot object call `TelegramBot(token)`.

**Args:**

- `token (string)` - Telegram Bot API token
- `auth_chat_id (string | int | None)` - default chat ID to send messages to

**Returns:**
    Return a class ``TelegramBot``.

```python
from pibody import TelegramBot

bot = TelegramBot("token")
```

---
### `.send_message(message, chat_id)`
Send a text message.  
Uses *chat_id* if provided, otherwise falls back to ``auth_id``.  
Silently does nothing if no target ID is available.

**Args:**

- `message (string)` - text to send
- `chat_id (string | int | None)` - override recipient chat ID for this call only

```python
bot.send_message("hello", 10000000)
```

---
### `.request_data() -> (message, sender_id)`
Poll for the latest incoming message (long-poll, timeout 5 s).  
Advances the internal offset so each update is returned only once.

**Returns**:
    ``(text, sender_id)`` of the latest message, or
    ``(None, None)`` on error or if there are no new messages.

```python
(message, sender_id) = bot.request_data()

print(message, sender_id)  # "hello", 10000000
```
