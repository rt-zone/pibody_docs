---
title: Encoder
---
# Encoder
Encoder is a device that converts rotational movement into a digital signal. It is widely used in various applications — from kitchen appliances and volume knobs to cars and 3D printers.

---
## Basic usage

---
### `Encoder(slot)`
To create a Encoder object, call `Encoder(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a ``RotaryEncoder`` object for *slot*.
```python
from pibody import Encoder

encoder = Encoder("A")
```

---
### `.read() -> int`
Returns the current position of the encoder.

```python
data = encoder.read()
print(data)
```

---
### `.value() -> int`
Same as `.read()` returns the current position of the encoder.

```python
value = encoder.value()
print(value)
```

---
### `.bound(min_val, max_val)`
Bounds encoder values in a range from **min_val** to **max_val**.

**Args**:

- `min_val (int | float)` - minimum value of encoder. By default, it is **0**
- `max_val (int | float)` - maximum value of encoder. By default, it is **10**

```python
encoder.bound(1, 10)
```

---
### `.wrap(min_val, max_val)`
Wraps encoder values in a range from **min_val** to **max_val**.

**Args**:

- `min_val (int | float)` - minimum value of encoder. By default, it is **0**
- `max_val (int | float)` - maximum value of encoder. By default, it is **10**

```python
encoder.wrap(1, 10)
```

---
### `.free()`
Resets bound and wrap mode to default unbounded mode of encoder.

```python
encoder.free()
```

---
## Other Functions

---
### `.old_value() -> int`
Returns the previous position of the encoder before the last change.

```python
data = encoder.old_value()
print(data)
```

---
### `.set_value(val)`
Set's value of encoder to value variable.

**Args**:

- `val (int | float)` - value of encoder. By default, it is **0**

```python
encoder.set_value(0)
```

---
### `.reset()`
Resets encoder value to **0**.

```python
encoder.reset()
```

---
### `.direction() -> int`
Returns rotation direction:

- **1** → clockwise
- **-1** → counter-clockwise
- **0** → no movement

```python
direction = encoder.direction()
print(direction)
```

---
### `.toggle_direction()`
Reverse the rotation direction.

```python
encoder.toggle_direction()
```

---
### `.set_incr(incr)`
Changes increment value of encoder to incr.

**Args**:

- `incr (int | float)` - - increment/decrement step of encoder. By default, it is **1**

```python
encoder.set_incr(0.1)
```

---
## API reference

---
### `.set(value, min_val, incr, max_val, reverse, range_mode)`
Set encoder's configuration. Any parameter not provided will remain unchanged.

**Args**:

- `value (int | float)` - current value of encoder. By default, it is **0**
- `min_val (int | float)` - minimum value of encoder. By default, it is **0**
- `max_val (int | float)` - maximum value of encoder. By default, it is **10**
- `incr (int | float)` - - increment/decrement step of encoder. By default, it is **1**
- `reverse (bool)` - if **True**, rotation direction will be inverted. By default, it is **False**
- `range_mode` - is optional integer which sets the value handling mode:

    - `RANGE_UNBOUNDED` (1) → value can increase/decrease without limit
    - `RANGE_WRAP` (2) → value wraps around between **min_val** and **max_val**
    - `RANGE_BOUNDED` (3) → value stops at **min_val** and **max_val**

    By default `range_mode` is `RANGE_UNBOUNDED`.

```python
encoder.set(value=0.5, min_val=0.1, incr=0.1, max_val=0.9, reverse=False, range_mode=3)
```

---
### `.close()`
Disables rotary encoder interrupts and stops value updates.

```python
encoder.close()
```

---
### `.bar(width, fill_char, empty_char) -> string`
Returns a text-based progress bar representing the current value position between **min_val** and **max_val**.

**Args**:

- `width (int)` - optional string size. By default `width` is **20**
- `fill_char (char)` - char, filled for done progress
- `empty_char (char)` - char, filled for undone progress

```python
bar = encoder.bar()
print(bar)
```

---
### `.live_bar(width, fill_char, empty_char)`
Prints a live-updating progress bar to the console.

**Args**:

- `width (int)` - optional string size. By default `width` is **20**
- `fill_char (char)` - char, filled for done progress
- `empty_char (char)` - char, filled for undone progress

```python
encoder.live_bar()
```

---
### `.add_listener(callback)`
Append function as an argument. This function will be invoked once encoder is rotated.

```python
encoder.add_listener(cb)
```

---
### `.remove_listener(callback)`
Removes a previously added callback function. Raises `ValueError` if the callback is not found.

```python
encoder.remove_listener(cb)
```
