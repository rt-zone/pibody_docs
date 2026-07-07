---
title: Built-in components
---
# Built-in components

Some components are **integrated into the PiBody device** rather than plugged
into a slot. They are always available and take **no slot or pin argument** in
code. (The bare [carrier](carrier.md) board has no display; WiFi and Telegram
come from the Pico W and work on either board.)

| Component | Class | What it is |
|-----------|-------|------------|
| Display   | `Display()`     | On-board screen (SPI-wired). Print text, draw shapes. |
| WiFi      | `WiFi()`        | The Pico W's wireless radio. Connect to a network, get time. |
| Telegram  | `TelegramBot(token)` | Send/receive Telegram messages over WiFi. |

## Usage

Because these are built in, you never pass a slot:

```python
from pibody import Display, WiFi

screen = Display()      # NO slot
screen.print("Hello")

wifi = WiFi()           # NO slot
wifi.connect("ssid", "password")
```

`TelegramBot` is the one exception that takes an argument — the bot **token** —
but still no slot:

```python
from pibody import TelegramBot

bot = TelegramBot("123456:ABC-your-token")
bot.send_message("chat_id", "Hi from PiBody")
```

## Why they have no slot

Built-in components are wired to fixed GPIO pins on the board (the display uses
the SPI pins; WiFi/Telegram use the Pico W's internal wireless chip). Those pins
are **reserved** and never appear in the free-GPIO list — see
[Ports & GPIO](ports.md). Unlike kit modules, built-ins have no lesson/module id
and are not counted as "used modules" in a project.
