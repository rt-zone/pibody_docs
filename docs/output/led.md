---
title: LED Control
---
# LED
The `pibody.LED()` factory function returns a `Pin` object configured as a digital output. Use it to drive an LED, a relay, or any on/off load connected to a PiBody slot.

---
## Basic usage

---
### `LED(slot) -> Pin`
To create LED object call `LED(slot)`.

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
## Other Functions

---
### `.value(value | None) -> None | float`
Get or set Pin value.

**Args:**

- `value (float)` - is optional which turns on or off depending on its state: `1 or 0`

Returns the current state `(1 or 0)` when called with no argument, otherwise sets value and returns None.

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
## PWM
You can use [`pibody.PWM`](pwm.md) class to control a LED module.

The LED can simulate different brightness levels using PWM. Fast blinking creates a dimmed light effect.

```python
from pibody import PWM

led = PWM("A")

led.freq(1000)  # Blinks 1000 times per second
led.duty(0.5)   # The LED is off for half of each cycle
```

`.freq(1000)` means the LED blinks 1000 times per second, and `.duty(0.5)` means the LED is on for half of the time.

---
## API reference

### Configuration

`Pin` objects have several class-level constants that select the operating mode. When
`pibody.LED()` returns a pin it is already configured as an output, but you can change
the mode at any time with `init()`.

`.init(mode=-1, pull=-1, *, value=None, alt=None)`


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
