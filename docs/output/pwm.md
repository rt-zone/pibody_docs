---
title: PWM
---
# PWM
PWM stands for Pulse Width Modulation. It may sound complicated, but it’s simply a smart way to control how much power is sent to devices like LEDs, buzzers, and servo motors.

PWM consists of two main parameters:

- Frequency
- Duty Cycle

---
## Basic usage

---
### `PWM(slot) -> Pin`
To create PWM object call `PWM(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a digital output ``Pin`` for *slot*.
```python
from pibody import PWM

pwm = PWM("A")
```

---
### `.freq(value | None) -> None | int`

**Args:**

- `value (int)` - parameter `value` is optional which sets the frequency of PWM. Useful range is **[20, 5000]**. By default `value` is **0**

If `value` is empty, method returns frequency thats used before.

```python
pwm.freq(100)

print(pwm.freq())  # 100
```

---
### `.duty(value | None) -> None | float`

**Args:**

- `value (float)` - parameter `value` is optional which sets the duty cycle of PWM. It can contains value in range **[0, 1.0]**. By default `value` is **0**

If `value` is empty, method returns duty cycle thats used before.

```python
pwm.duty(0.5)

print(pwm.duty())  # 0.5
```

---
### `.duty_u16(value | None) -> None | int`
Get or set the PWM duty cycle as a 16-bit value.

**Args:**

- `value (int)` - parameter `value` is optional which sets the duty cycle of PWM. It can contains value in range **[0, 65535]**. By default `value` is **32768**

If `value` is empty, method returns duty cycle thats used before.

```python
pwm.duty_u16(32768)

print(pwm.duty_u16())  # 32768
```

---
## Examples
You can control LED with PWM to change brightness using `.freq()` and `.duty()` functions.

Connect LED module to slot "A", and run code below. You will see how PWM affects the operation of LED.

```python
from pibody import PWM

pwm = PWM("A")  # put LED to "A"

pwm.freq(100)
pwm.duty(0.5)
```

---
## Other Functions

---
### `.deinit()`
Disable the PWM output and release the pin.

```python
pwm.deinit()
```

---
### `.duty_ns(value | None) -> None | int`
Get or set the PWM duty cycle in nanoseconds. The nanosecond value must be between 0 and the total period of your frequency. For example, if you set a frequency of **1000 Hz** (period = *1,000,000 ns*), `.duty_ns()` must fall in the range **[0, 1000000]**.

**Args:**

- `value (int)` - parameter `value` is optional which sets the duty cycle in nanoseconds

If `value` is empty, method returns duty cycle thats used before.

```python
data = pwm.duty_ns()
print(data)
```
