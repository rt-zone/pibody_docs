---
title: Telegram Bot
---
# Telegram Bot
IoT жобаларыңыз үшін Telegram Bot негізгі қосылуы. Ресми [BotFather](https://telegram.me/BotFather) Telegram-да өзіңіздің `API_TOKEN` алуыңыз керек.

---
### `TelegramBot(token, auth_chat_id)`
TelegramBot объектісін жасау үшін `TelegramBot(token)` шақырыңыз.

**Аргументтер:**

- `token (string)` — Telegram Bot API токені
- `auth_chat_id (string | int | None)` — хабарламаларды жіберу үшін әдепкі чат ID

**Қайтарады:**
    ``TelegramBot`` класын қайтарады.

```python
from pibody import TelegramBot

bot = TelegramBot("token")
```

---
### `.send_message(message, chat_id)`
Мәтіндік хабарлама жібереді.  
*chat_id* берілсе, соны пайдаланады, әйтпесе ``auth_id``-ға оралады.  
Қолжетімді ID болмаса, ештеңе жасамайды.

**Аргументтер:**

- `message (string)` — жіберілетін мәтін
- `chat_id (string | int | None)` — тек осы шақыру үшін алушы чат ID-ін қайта анықтайды

```python
bot.send_message("сәлем", 10000000)
```

---
### `.request_data() -> (message, sender_id)`
Соңғы кіріс хабарламаны сұрайды (long-poll, таймаут 5 с).  
Ішкі offset-ті жылжытады, сондықтан әр жаңарту тек бір рет қайтарылады.

**Қайтарады:**
    Соңғы хабарламаның ``(text, sender_id)`` мәні немесе
    қате немесе жаңа хабарламалар болмаса ``(None, None)``.

```python
(message, sender_id) = bot.request_data()

print(message, sender_id)  # "сәлем", 10000000
```
