---
title: Joystick
---
# Joystick
Joystick is a small control lever that can be moved with your fingers. It is used in game controllers and robotics to move objects in different directions. Typically, it contains two potentiometers — one for left-right movement (X-axis) and one for up-down movement (Y-axis).

---
### `Joystick(slot)`
To create Joystick object call `Joystick(slot)`.

Only slot F on PiBody can handle two analog signals at the same time, so on other slots the joystick will not work correctly.

**Args:**

- `slot (string)` - slot label ("F")

**Returns:**
    Return a class output ``Joystick`` for *slot*.
```python
from pibody import Joystick

joystick = Joystick("F")
```

---
### `.read() -> (int, int)`
Return `(x, y)` normalised values in `[0.0, 1.0]`, or `None` per axis if unavailable.

```python
x, y = joystick.read()
print(x, y)
```

---
### `.read_x() -> int`
Return the normalised X-axis value, or `None` if the axis is unavailable.

```python
x = joystick.read_x()
print(x)
```

---
### `.read_y() -> int`
Return the normalised Y-axis value, or `None` if the axis is unavailable.

```python
y = joystick.read_y()
print(y)
```

---
## Examples

```python
from pibody import Joystick

joystick = Joystick("F")

while True:
    x, y = joystick.read()
    # get X axis
    print(x)

    # get X axis
    x1 = joystick.read_x()
    print(x1)

    # get X axis
    x2 = joystick.read()[0]
    print(x2)
```
