---
title: Carrier board
---
# Carrier board

The **carrier** is a second board included in the PiBody kit. It exposes the
same **A–H slots** and runs the same `pibody` library as the full
[PiBody](pibody.md) device, but it is stripped down for building a finished
project into a compact case:

- **All eight ports A–H via JST** — every port is a keyed **JST** connector,
  including A–F (on PiBody, A–F are magnetic).
- **No display**, **no GP20/GP21 buttons** — those are PiBody-only.
- **No enclosure** — it is a bare board you integrate into your own build.
- **Swappable Pico W** — like PiBody, the Pico plugs in and can be replaced.

It still keeps the essentials for a running build: a **RESET** button, an
**on/off slide switch**, a **battery JST** connector, and a **servo header**
(the `S / + / −` pins for positions 8, 9, 12). Like PiBody, it also breaks out
**every Pico GPIO and power pin** to a row of holes beside the Pico, so any pin
can be wired directly (see [Ports & GPIO](ports.md#pico-header-breakout)).

The workflow is: **prototype on PiBody** (snap modules on with magnets, use the
display and buttons to test), then **move the same modules to the carrier** and
wire everything through JST to assemble a compact, permanent project.

## Slots A–H

The carrier carries the same eight general-purpose slots, **A** through **H**,
with the same GPIO mapping as PiBody. Each carries two signal lines; what a slot
can do depends on which GPIO pins it is wired to (see [Ports & GPIO](ports.md)
for the exact mapping):

| Capability | Slots | Why |
|------------|-------|-----|
| Digital in/out, PWM | A, B, C, D, E, F, G, H | every slot has digital-capable pins |
| Analog input (ADC)  | **C, F only** | only these slots reach the RP2040 ADC pins |
| Two analog lines (Joystick) | **F only** | F exposes two ADC lines simultaneously |
| I²C bus | any **except C** | C's second line is shared with the ADC mux |
| NeoPixel (LED Tower) | G, H or positions 8, 9 | |

## Fixed positions

Beyond the A–H slots, the board has dedicated positions for servos and the
LED Tower:

- **Servo positions 8, 9, 12** — a servo is created by its numeric position,
  e.g. `Servo(8)`, not by a letter slot. The LED Tower can also use positions
  8, 9 (or slots G, H).

The **display** and **GP20/GP21 buttons** are part of the PiBody device only and
are **not** present on the carrier — see [PiBody](pibody.md) and
[built-in components](built-in.md).

## Choosing a slot in code

The code is identical on either board — you pass the slot the module is plugged
into:

```python
from pibody import LED, LightSensor

led = LED("A")            # any digital slot
light = LightSensor("C")  # ADC slot only (C or F)
```

If a module needs a capability a slot cannot provide (e.g. analog on a
non-ADC slot), it will not work correctly. Match the module to a valid slot from
the table above — each module page lists its valid ports.
