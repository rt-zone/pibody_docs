---
title: Telegram Bot
---
# Telegram Bot
Базовое подключение Telegram-бота для ваших IoT-проектов. Вам необходимо получить собственный `API_TOKEN` у официального бота Telegram [BotFather](https://telegram.me/BotFather).

---
### `TelegramBot(token, auth_chat_id)`
Чтобы создать объект TelegramBot, вызовите `TelegramBot(token)`.

**Аргументы:**

- `token (string)` — API-токен Telegram Bot
- `auth_chat_id (string | int | None)` — ID чата по умолчанию для отправки сообщений

**Возвращает:**
    Возвращает объект ``TelegramBot``.

```python
from pibody import TelegramBot

bot = TelegramBot("token")
```

---
### `.send_message(message, chat_id)`
Отправляет текстовое сообщение.  
Использует *chat_id*, если он указан, иначе использует ``auth_chat_id``.  
Ничего не делает, если нет доступного ID.

**Аргументы:**

- `message (string)` — текст для отправки
- `chat_id (string | int | None)` — переопределяет ID чата получателя только для этого вызова

```python
bot.send_message("привет", 10000000)
```

---
### `.request_data() -> (message, sender_id)`
Опрашивает последнее входящее сообщение (long-poll, таймаут 5 с).  
Сдвигает внутренний offset, чтобы каждое обновление возвращалось только один раз.

**Возвращает:**
    ``(text, sender_id)`` последнего сообщения или
    ``(None, None)`` при ошибке или отсутствии новых сообщений.

```python
(message, sender_id) = bot.request_data()

print(message, sender_id)  # "привет", 10000000
```
