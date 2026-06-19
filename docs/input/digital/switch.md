---
title: Switch
---
# Switch
Switch - is a simple mechanism that controls the flow of electric current.

---
### `Switch(slot) -> Pin`
To create Switch object call `Switch(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.IN).

**Returns:**
    Return a digital output ``Pin`` for *slot*.
```python
from pibody import Switch

switch = Switch("A")
```

---
### `.read() -> int`
Returns **0 or 1** depending on its state.

```python
switch.read()
```

```python
from pibody import Switch

switch = Switch("A")

while True:
    if switch.read():
        print("switch is turned on")
    else:
        print("switch is turned off")
```

---
### `.value() -> int`
Same as `.read()`, returns **0 or 1** depending on its state.

```python
value = switch.value()
print(value)
```
