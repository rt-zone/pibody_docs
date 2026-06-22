---
title: Touch Sensor
---
# Touch Sensor
Touch Sensor — is a button that detects the touch of a finger or a conductive object. Unlike mechanical buttons, it has no moving parts, making it more durable and reliable.

---
### `TouchSensor(slot) -> Pin`
To create a TouchSensor object, call `TouchSensor(slot)`.

Also you can use short alias `Touch(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.IN).

**Returns:**
    Return a digital input ``Pin`` for *slot*.
```python
from pibody import TouchSensor

touch = TouchSensor("A")
```

---
### `.read() -> int`
Returns **0 or 1** depending on its state.

```python
touch.read()
```

```python
from pibody import Touch  # short alias

touch = Touch("A")

while True:
    if touch.read():
        print("Touch is pressed")
    else:
        print("Touch is not pressed")
```

---
### `.value() -> int`
Same as `.read()`, returns **0 or 1** depending on its state.

```python
value = touch.value()
print(value)
```
