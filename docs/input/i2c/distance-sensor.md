---
title: Distance Sensor
---
# Distance Sensor
Distance Sensor — is an active sensor that measures the distance to an object with high precision. The sensor uses an infrared laser and records the time it takes for the laser to return back.

---
## Basic usage

---
### `DistanceSensor(slot)`
To create DistanceSensor object call `DistanceSensor(slot)`.

Also you can use short alias `Distance(slot)`.

You can choose any other slot (except `"C"`, as it does not support I2C communication).

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a class ``VL53L0X`` for *slot*.
```python
from pibody import DistanceSensor

distance = DistanceSensor("A")
```

---
### `.read() -> int`
Perform a single ranging measurement.  
Returns distance in mm **[20, 2000]**.  
Returns `20` or `8190` if invalid measurement.

```python
from pibody import Distance   # short alias
distance = Distance('A')

data = distance.read()

print(data)
```

---
### `.is_valid(distance) -> bool`
Parameter `distance` is mandatory which should contained actual distance in mm.

Returns **True** or **False** if measurements between `.min_valid_mm` and `.max_valid_mm` are valid.  
`.min_valid_mm` by default is **30**.  
`.max_valid_mm` by default is **2000**.  
These variables can be changed.

```python
from pibody import Distance   # short alias
distance = Distance('A')

distance.min_valid_mm = 50
distance.max_valid_mm = 200

curr_dist = distance.read()

valid = distance.is_valid(curr_dist)
print(valid)
```

---
## Other Functions

---
### `.bar() -> string`
Return a text progress-bar of the current distance.

**Args**:

- `max_range (int | None)` - distance (mm) that corresponds to a full bar. By default is **200** mm
- `width (int | None)` - bar width in characters. By default is **20** symbols
- `fill_char (string | None)` - character used for the filled portion. By default is **“#”**
- `empty_char (string | None)` - character used for the empty portion. By default is **" "**

```python
from pibody import Distance   # short alias
distance = Distance('A')

bar = distance.bar()

print(bar) # [######  ] 75 mm
```

---
### `.add_close_trigger(threshold_mm, callback)`
Register a callback fired when an object is closer than *threshold_mm*.

**Args**:

- `threshold_mm (int)` - distance threshold in mm
- `callback` - called with the current distance (mm)

```python
distance.add_close_trigger(100, cb)
```

---
### `.add_motion_trigger(change_threshold_mm, callback, cooldown_ms)`
Register a callback fired when the distance changes by more than *change_threshold_mm* between consecutive check() calls.

**Args**:

- `change_threshold_mm (int)` - minimum delta (mm) to trigger
- `callback` - called with (distance_mm, delta_mm)
- `cooldown_ms` - minimum ms between consecutive triggers. By default is **500**

```python
distance.add_motion_trigger(100, cb)
```

---
### `.check()`
Read distance and fire any registered callbacks.

Should be called periodically from the main loop.
Invalid readings are silently ignored.

```python
distance.add_motion_trigger(100, cb)

while True:
    distance.check()				  
```
