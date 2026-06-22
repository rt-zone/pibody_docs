---
title: Motion Sensor
---
# Motion Sensor
Motion Sensor - is a device that detects movement.

---
### `MotionSensor(slot) -> Pin`
To create a MotionSensor object, call `MotionSensor(slot)`.

Also you can use short alias `Motion(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.IN).

**Returns:**
    Return a digital input ``Pin`` for *slot*.

```python
from pibody import MotionSensor

motion = MotionSensor("A")
```

---
### `.read() -> int`
Returns **0 or 1** depending on its state.

```python
motion.read()
```

```python
from pibody import Motion  # short alias

motion = Motion("A")

while True:
    if motion.read():
        print("Motion is detected")
    else:
        print("Motion is not detected")
```

---
### `.value() -> int`
Same as `.read()`, returns **0 or 1** depending on its state.

```python
value = motion.value()
print(value)
```
