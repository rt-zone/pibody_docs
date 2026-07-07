---
title: Telegram Bot
canonical: telegram-bot
class_name: TelegramBot
category: iot
interface: UART
ports: []
built_in: true
prompt_note: "Telegram (send_message/request_data)"
---
# Telegram Bot
Provides a basic Telegram Bot connection for your IoT projects. You need to obtain your own `API_TOKEN` from the official Telegram [BotFather](https://telegram.me/BotFather).

---
### `TelegramBot(token, auth_chat_id)`
To create TelegramBot object call `TelegramBot(token)`.

**Args:**

- `token (string)` - Telegram Bot API token
- `auth_chat_id (string | int | None)` - default chat ID to send messages to

**Returns:**
    Return a ``TelegramBot`` object.

```python
from pibody import TelegramBot

bot = TelegramBot("token")
```

---
### `.send_message(message, chat_id)`
Send a text message.  
Uses *chat_id* if provided, otherwise falls back to ``auth_chat_id``.  
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
