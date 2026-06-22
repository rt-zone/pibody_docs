---
title: Push Button
---
# Push Button
A button is a simple switching mechanism used to control the flow of current. When the button is pressed, it closes the electrical circuit, allowing current to pass through.

---
### `Button(slot) -> Pin`
To create a Button object, call `Button(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.IN).

**Returns:**
    Return a digital input ``Pin`` for *slot*.
```python
from pibody import Button

button = Button("A")
```

---
### `.read() -> int`
Returns **0 or 1** depending on its state.

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
Same as `.read()`, returns **0 or 1** depending on its state.

```python
value = button.value()
print(value)
```
