---
title: Push Button
---
# Push Button
A button is a simple switching mechanism used to control the flow of current. When the button is pressed, it closes the electrical circuit, allowing current to pass through.

---
### `Button(slot) -> Pin`
To create Button object call `Button(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT).

**Returns:**
    Return a digital output ``Pin`` for *slot*.
```python
from pibody import Button

button = Button("A")
```

---
### `.read() -> int`
Returns `1` or `0` depending on its state.
```python
button.read()
```

```python
from pibody import Button

button = Button("A")

while True:
    if button.read():
        print("Button is pressed")
    else:
        print("Button is not pressed")
```

---
### `.value() -> int`
Same as `.read()`, returns `1` or `0` depending on its state.

```python
value = button.value()
print(value)
```
