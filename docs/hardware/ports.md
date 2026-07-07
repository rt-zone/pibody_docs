---
title: Ports & GPIO
slots:
  A: [0, 1]
  B: [2, 3]
  C: [28, 22]
  D: [4, 5]
  E: [6, 7]
  F: [26, 27]
  G: [16, 17]
  H: [18, 19]
reserved:
  SERVO: [8, 9, 12]
  BUTTON: [20, 21]
  DISPLAY: [10, 11, 13, 14, 15]
gpio_all: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 26, 27, 28]
---
# Ports & GPIO

This page is the **single source of truth** for how PiBody wires its ports onto
the Raspberry Pi Pico W GPIO pins. The **[PiBody](pibody.md)** device and the
bare **[carrier](carrier.md)** board share this same mapping — only the physical
connector differs (PiBody uses magnets for A–F and JST for G/H; the carrier uses
JST throughout). The `slots`, `reserved` and `gpio_all` values in the
frontmatter above are read by the code-generation tooling; the tables below are
the human-readable view of the same data.

## Kit slots (A–H)

Each general-purpose slot carries two signal lines wired to two GPIO pins:

| Slot | GPIO pins   | Notes                                   |
|------|-------------|-----------------------------------------|
| A    | GPIO0, GPIO1 | digital / PWM                          |
| B    | GPIO2, GPIO3 | digital / PWM                          |
| C    | GPIO28, GPIO22 | **ADC-capable** (analog input)       |
| D    | GPIO4, GPIO5 | digital / PWM                          |
| E    | GPIO6, GPIO7 | digital / PWM                          |
| F    | GPIO26, GPIO27 | **ADC-capable**, two analog lines (Joystick) |
| G    | GPIO16, GPIO17 | digital / NeoPixel (4-pin JST on PiBody) |
| H    | GPIO18, GPIO19 | digital / NeoPixel (4-pin JST on PiBody) |

- **Analog (ADC)** inputs work only on **C** and **F** (the ADC-wired pins).
- **I²C** works on any slot **except C** (C's second line is shared with the
  ADC mux and cannot drive a clean I²C bus).
- **NeoPixel (LED Tower)** runs on slots **G, H** or positions **8, 9**
  (position 12 is servo-only).

## Fixed-function pins (reserved)

These GPIO pins are hard-wired to on-board peripherals and are **never** free for
external wiring:

| Function | GPIO pins            |
|----------|----------------------|
| Servo / LED Tower | GPIO8, GPIO9, GPIO12 (positions 8, 9, 12) |
| Buttons  | GPIO20, GPIO21 (GP20/GP21, PiBody only; the carrier has RESET but no GP20/GP21) |
| Display  | GPIO10, GPIO11, GPIO13, GPIO14, GPIO15 (SPI; PiBody only) |

## Pico header breakout

On both boards the Pico W plugs into the middle, and **every one of its pins is
broken out to a row of holes** running down **both sides** of it — like a
breadboard rail. Each GPIO (and the power pins: VBUS, VSYS, 3V3, GND) is
duplicated on the adjacent row, so you can attach a jumper or connector to
**any** pin directly, without going through an A–H slot.

This is the escape hatch for anything the slot API doesn't cover: wiring your own
part, tapping a signal, or reaching a pin that is otherwise reserved. Two
cautions:

- A pin exposed here is the **same electrical pin** as the slot/servo/display it
  belongs to — driving it from the breakout **and** from a module at the same
  time will conflict.
- Only the **free** pins below are safe for external parts. Reserved pins
  (servo, display, buttons) are broken out too, but are already in use.

## Free GPIO pins

Any GPIO in `gpio_all` that is **not** in `reserved` is available for wiring an
external (non-kit) component: GPIO0–7, GPIO16–19, GPIO22, GPIO26–28. External
parts must only be wired to these free pins — never to a servo, display, or
button pin.

See also [PiBody](pibody.md), [Carrier board](carrier.md), and
[Built-in components](built-in.md).
