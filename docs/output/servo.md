---
title: Servo
canonical: servo
class_name: Servo
lesson_id: 63
category: output
interface: PWM
ports: [8, 9, 12]
prompt_note: "servo motor (angle/duty)"
---
# Servo
Servo motor — is a motor that can rotate to a specific set angle. Unlike a regular motor, it cannot spin freely (so you can’t make a fan or a car motor out of it), but with a microcontroller, you can precisely set the rotation angle of the servo drive with an accuracy of half a degree, and it will hold the set position.

---
## Basic usage

---
### `Servo(pin) -> Servo`
To create Servo object call `Servo(pin)`.

**Args:**

- `pin (int)` - pin port (8, 9 or 12)

**Returns:**
    Return a `Servo` object for *pin*.

Internally the servo is driven by PWM at **50 Hz** (period = 20 ms). The frequency is set automatically — you don't need to configure it yourself.

```python
from pibody import Servo

servo = Servo(9)
```

---
### `.angle(angle | None) -> None | int`
Get or set the servo angle **(0–180 degrees)**.

**Args:**

- `angle (float)` - is optional which sets a servo angle in range **[0, 180]** degrees

Returns the current angle **[0, 180]** when called with no argument, otherwise sets angle and returns None.

The getter returns the last angle set through the object (not read back from the hardware). If no angle has been set yet, it returns `None`.

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
### `servo(angle | None) -> None | int`
A `Servo` object is callable — calling it works exactly like `.angle()`.

**Args:**

- `angle (float)` - is optional which sets a servo angle in range **[0, 180]** degrees

`servo(90)` sets the angle, `servo()` returns the current angle.

```python
from pibody import Servo

servo = Servo(9)

servo(90)       # same as servo.angle(90)
print(servo())  # 90
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
servo.off()
```

---
## Direct control via PWM

The `Servo` class no longer exposes `duty`, `duty_u16` or `freq`. If you need low-level control, create a PWM object directly instead of a `Servo`:

```python
from pibody import PWM

servo = PWM(8)
servo.freq(50)  # must be set manually
```

Servo position is controlled by the **pulse width** of the PWM signal, not the duty cycle directly. For example, a standard 180° servo expects a pulse between **0.5 ms** (0°) and **2.5 ms** (180°), repeated every **20 ms** (50 Hz).

The `freq` sets how often the pulse repeats — for servos this must be **50 Hz** (period = 20 ms). The `duty` sets what fraction of that period the signal is high. To convert an angle to a duty value:

```
pulse_width = (angle / 180) * 2 + 0.5   # 0.5–2.5 ms
duty = pulse_width / SERVO_PERIOD_MS    # fraction of 20 ms
```

In PiBody kit **SERVO_PERIOD_MS = 20** (equal to **1000 // freq**).

Going **above** the recommended range (e.g. pulse > 2.5 ms for a 180° servo) won't damage the servo — most models simply ignore the excess and hold at their maximum angle. Some may emit a faint hum at the mechanical stop; this is normal. Values **below** the 0.5 ms minimum are also clamped by the servo hardware to the 0° position.

The methods below are methods of [`pibody.PWM`](pwm.md), shown here as applied to a servo.

---
### `.duty(value | None) -> None | float`
You can set angle through duty. To control at first convert angle to pulse width:  
```pulse_width = (angle / 180) * 2 + 0.5```

After that convert pulse width to duty cycle:  
```duty = pulse_width / SERVO_PERIOD_MS```

*Use value int range* **[0.025, 0.125]**.
*Value* **0** *will turn off Servo.*

**Args:**

- `value (float)` - parameter `value` is optional which sets the duty cycle of PWM. It can contains value in range **[0, 0.125]**. By default `value` is **0**

If `value` is empty, method returns duty cycle thats used before.

```python
from pibody import PWM
SERVO_PERIOD_MS = 20

servo = PWM(8)
servo.freq(50)

angle = 90
pulse_width = (angle / 180) * 2 + 0.5  # 1.5

duty = pulse_width / SERVO_PERIOD_MS   # 0.075
servo.duty(duty)

print(servo.duty())  # 0.075
```

---
### `.duty_u16(value | None) -> None | int`
Same as `.duty()`, you can set angle through duty_u16. **u16** means *16-bit* value.

*Use value int range* **[1638, 8191]**
*Value* **0** *will turn off Servo.*

**Args:**

- `value (int)` - parameter `value` is optional which sets the duty cycle of [`pibody.PWM`](pwm.md). It can contains value in range **[1638, 8191]**. By default `value` is **0**

If `value` is empty, method returns duty cycle thats used before.

```python
from pibody import PWM
SERVO_PERIOD_MS = 20

servo = PWM(8)
servo.freq(50)

angle = 90
pulse_width = (angle / 180) * 2 + 0.5  # 1.5

duty = pulse_width / SERVO_PERIOD_MS   # 0.075 (normalized)
duty_u16 = int(duty * 65535)           # ~4915
servo.duty_u16(duty_u16)

print(servo.duty_u16())  # 4915
```

---
### `.freq(value | None) -> None | int`
The `freq` sets how often the pulse repeats — for servos this must be **50 Hz** (period = 20 ms).

**Args:**

- `value (int)` - parameter `value` is optional which sets the frequency of PWM. By default `value` is `50`

If `value` is empty, method returns frequency thats used before.

```python
pwm.freq(50)

print(pwm.freq())  # 50
```
