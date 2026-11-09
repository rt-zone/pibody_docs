---
title: Servo 360
canonical: servo-360
class_name: Servo
lesson_id: 63
blockly_lesson_id: 612
category: output
interface: PWM
ports: [8, 9]
prompt_note: "continuous-rotation servo: angle(90) stops, 0/180 spin at full speed either way"
---
# Servo 360
A 360° servo (continuous-rotation servo) spins freely like a small geared motor — you can make wheels for a robot car out of it. Unlike a regular [servo](servo.md), it does not hold an angle: the same signal sets its **speed and direction**. It is controlled with the same `Servo` class.

---
## Basic usage

---
### `Servo(pin) -> Servo`
To create a Servo object call `Servo(pin)`.

**Args:**

- `pin (int)` - pin port (8 or 9)

**Returns:**
    Return a `Servo` object for *pin*.

```python
from pibody import Servo

wheel = Servo(8)
```

---
### `.angle(angle | None) -> None | int`
Set the speed and direction of rotation through the angle value **(0–180)**.

**Args:**

- `angle (float)` - `90` stops the servo, `180` is full speed in one direction, `0` is full speed in the other; values in between set a lower speed (for example `135` is half speed).

Returns the last value set when called with no argument, otherwise sets it and returns None.

```python
from pibody import Servo
from time import sleep

wheel = Servo(8)

wheel.angle(180)  # full speed forward
sleep(2)
wheel.angle(90)   # stop
sleep(1)
wheel.angle(0)    # full speed backward
sleep(2)
wheel.angle(90)
```

---
### `.off()`
Stop sending pulses — the servo stops. The last value is kept: `.angle()` still returns it.

Servos on pins **8 and 9 share one PWM unit**, so `.off()` on one of them stops both.

```python
wheel.off()
```

---
### `.on()`
Resume the output with the last value — the servo spins again at the same speed. Setting a new `.angle()` also turns the output back on.

```python
wheel.on()
```
