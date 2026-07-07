---
title: PiBody
---
# PiBody

**PiBody** is an educational electronics kit built around the
[Raspberry Pi Pico W](https://www.raspberrypi.com/products/raspberry-pi-pico/)
microcontroller. Students write **MicroPython** using the `pibody` library,
which wraps the low-level hardware in a friendly, slot-based API.

## The core

- **Microcontroller:** Raspberry Pi Pico W (RP2040 + on-board wireless).
- **Firmware:** MicroPython with the `pibody` library preloaded.
- **Language:** MicroPython (a subset of Python 3 for microcontrollers).

## The PiBody device

PiBody is a self-contained device in a 3D-printed plastic and acrylic
enclosure. Everything a student needs to prototype is on board:

- **Swappable Pico W** — the Pico W plugs into the outside of the board and can
  be replaced if needed.
- **Display** — an on-board screen for text and shapes (see
  [built-in components](built-in.md)).
- **Micro USB** — for power and flashing code.
- **Removable battery** — connects through a cable, so PiBody can run untethered.
- **On/off switch** — cuts power to the whole device.
- **Buttons** — **GP20**, **GP21**, and a **Reset** button.

Because the display and the GP20/GP21 buttons are wired to fixed pins, they take
no slot in code — see [built-in components](built-in.md) and
[Ports & GPIO](ports.md).

## Ports

PiBody breaks the Pico's GPIO out into labelled, keyed connectors so modules
attach without wiring mistakes. The pin mapping for every slot is on the
[Ports & GPIO](ports.md) page.

- **A, B, C, D, E, F — magnetic ports.** Sensor modules (each in its own
  3D-printed case) snap on with magnets, which makes connecting and swapping
  them easy for students.
- **G (16, 17), H (18, 19) — 4-pin JST.** Exposed as JST connectors rather than
  magnetic ports.
- **8, 9, 12 — servo / LED Tower.** Dedicated positions for driving a servo or a
  NeoPixel LED Tower; a servo is addressed by its numeric position, e.g.
  `Servo(8)`.

Every module **except the servo** also carries a JST port of its own, so modules
can be chained or wired directly as well as snapped onto a magnetic port.

Alongside the Pico W, **every GPIO and power pin is broken out to a row of holes**
(like a breadboard rail), so you can wire a jumper or connector to any pin
directly — the escape hatch for anything the A–H slots don't cover. See
[Ports & GPIO](ports.md#pico-header-breakout).

## How it fits together

- Each **module** (a sensor or actuator) plugs into a slot. In code you create it
  by its class name and its slot, e.g. `LED("A")` or `LightSensor("C")`.
- A few components are **[built into](built-in.md)** the board (Display, WiFi,
  Telegram) and take no slot.
- The **[carrier](carrier.md)** is a second, bare board in the kit: once a
  project is prototyped on PiBody, the same modules can be moved to the carrier
  and built into a compact enclosure.
- The **[Ports & GPIO](ports.md)** page documents exactly which GPIO pins each
  slot maps to, and which pins are left free for external parts.

## The `pibody` library

Every module page in this documentation describes one `pibody` class: its
constructor, the valid slots it accepts, and its methods. The frontmatter on
each page also carries machine-readable metadata (canonical name, class name,
valid ports, aliases, lesson id) so tooling can stay in sync with the docs from a
single source.
