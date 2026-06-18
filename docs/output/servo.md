---
title: Servo
---
# Servo
Servo motor — is a motor that can rotate to a specific set angle. Unlike a regular motor, it cannot spin freely (so you can’t make a fan or a car motor out of it), but with a microcontroller, you can precisely set the rotation angle of the servo drive with an accuracy of half a degree, and it will hold the set position.

---
## Basic usage

---
### `Servo(pin) -> PWM`
To create Servo object call `Servo(pin)`.

**Args:**

- `pin (int)` - pin port (8, 9 or 12)

**Returns:**
    Return a output [`pibody.PWM`](pwm.md) for *pin*.
```python
from pibody import Servo

servo = Servo(9)
```

---
### `.angle(val | None) -> None | int`
Get or set the servo angle `(0–180 degrees)`.

**Args:**

- `val (float)` - is optional which sets the angle `(0–180 degrees)`

Returns the current angle `(0–180)` when called with no argument, otherwise sets angle and returns None.

```python
from pibody import Servo
from time import sleep

servo = Servo(8)

servo.angle(180)
sleep(1)

print(servo.angle())  # 180

servo.angle(90)
sleep(1)
servo.angle(0)
sleep(1)

print(servo.angle())  # 0
```

---
## Other Functions

---
### `.freq(value | None) -> None | int`

**Args:**

- `value (int)` - parameter `value` is optional which sets the frequency of PWM. By default `value` is `50`

If `value` is empty, method returns frequency thats used before.

```python
servo.freq(50)

print(servo.freq())  # 50
```

---
### `.duty_u16(value | None) -> None | int`

**Args:**

- `value (int)` - parameter `value` is optional which sets the duty cycle of [`pibody.PWM`](pwm.md). It can contains value in range [0, 65535]. By default `value` is `32768`

If `value` is empty, method returns duty cycle thats used before.

```python
servo.duty_u16(32768)

print(servo.duty_u16())  # 32768
```

---
### `.on()`
Re-initialise the PWM output (enable the servo).

```python
servo.on()
```

---
### `.off()`
De-initialise the PWM output (disable the servo).

```python
servo.on()
```
