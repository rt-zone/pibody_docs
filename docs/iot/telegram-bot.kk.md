---
title: Telegram Bot
---
# Telegram Bot
IoT жобаларыңызға арналған Telegram-ботпен негізгі қосылу. Ресми Telegram [BotFather](https://telegram.me/BotFather) ботынан өз `API_TOKEN` токеніңізді алуыңыз қажет.

---
### `TelegramBot(token, auth_chat_id)`
TelegramBot объектісін жасау үшін `TelegramBot(token)` шақырыңыз.

**Аргументтер:**

- `token (string)` — Telegram Bot API токені
- `auth_chat_id (string | int | None)` — хабарламаларды жіберу үшін әдепкі чат ID

**Қайтарады:**
    ``TelegramBot`` объектісін қайтарады.

```python
from pibody import TelegramBot

bot = TelegramBot("token")
```

---
### `.send_message(message, chat_id)`
Мәтіндік хабарлама жібереді.  
*chat_id* берілсе, соны пайдаланады, әйтпесе ``auth_chat_id``-ға оралады.  
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
