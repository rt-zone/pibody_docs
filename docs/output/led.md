---
title: LED Control
---
# LED
The `pibody.LED()` factory function returns a `Pin` object configured as a digital output. Use it to drive an LED, a relay, or any on/off load connected to a PiBody slot.

---
## Basic usage

---
### `LED(slot) -> Pin`
To create a LED object, call `LED(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a digital output ``Pin`` for *slot*.
```python
from pibody import LED

led = LED("A")
```

---
### `.on()`
Turns connected led on.
```python
led.on()  # turns on
```

---
### `.off()`
Turns connected led off.
```python
led.off()  # turns off
```

---
### `.value(value | None) -> None | float`
Get or set Pin value.

**Args:**

- `value (float)` - is optional which turns on or off depending on its state: **0 or 1**

Returns the current state **(0 or 1)** when called with no argument, otherwise sets value and returns None.

```python
# Turns on, same as led.on()
led.value(1)
print(led.value())  # 1

# Turns off, same as led.off()
led.value(0)
print(led.value())  # 0
```

---
### `.toggle()`
Changes the state of LED to opposite of current state. 
```python
led.on()            # turns on

led.toggle()        # turns off

print(led.value())  # 0
```

---
## Other Functions

### `.high()`

Set the high output level with these equivalent method:

```python
# Same as led.on()
led.high()
```

### `.low()`

Set the low output level with these equivalent method:

```python
# Same as led.off()
led.low()
```

---
## PWM
You can use [`pibody.PWM`](pwm.md) to control an LED module and adjust its brightness — not just on/off.

The LED rapidly turns on and off faster than the eye can see. The brain averages this into a perceived brightness level.

### Parameters

- **`freq`** — how many times per second the LED blinks
    
    - Below **50 Hz** — visible flickering (useful for attention effects)
    - **100–200 Hz** — mostly stable, may still flicker in peripheral vision
    - **500–5000 Hz** — looks fully steady to the human eye. Start at **1000 Hz**
    - Higher values are fine but won't look different; they use more CPU

- **`duty`** — what fraction of each blink the LED is on (0.0 to 1.0)

    - **0** = fully off
    - **0.25** = dim
    - **0.5** = half brightness
    - **0.75** = bright
    - **1.0** = fully on (same as `led.on()`)

### Basic example

```python
from pibody import PWM

led = PWM("A")

led.freq(1000)   # 1 kHz — steady to the eye
led.duty(0.5)    # half brightness
```

### Smooth fade effect

```python
from pibody import PWM
from time import sleep

led = PWM("A")
led.freq(1000)

while True:
    for i in range(0, 101, 1):       # ramp up
        led.duty(i / 100)
        sleep(0.01)
    for i in range(100, -1, -1):     # ramp down
        led.duty(i / 100)
        sleep(0.01)
```
