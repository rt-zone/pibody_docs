---
title: Light Sensor
---
# Light Sensor
Light Sensor is an analog sensor capable of reading the level of light falling on it.

---
### `LightSensor(slot) -> ADC`
To create LightSensor object call `LightSensor(slot)`.

Also you can use short alias `Light(slot)`.

Since the light sensor is analog, it can only be inserted into slots with an ADC (analog-to-digital converter), and there are only 2 such slots on the PiBody: `"C"` and `"F"`.

**Args:**

- `slot (string)` - slot label ("C", "F").

**Returns:**
    Return an ``ADC`` object for the analogue pin of *slot*.

```python
from pibody import LightSensor

light = LightSensor("C")
```

---
### `.read() -> float`
Returns value in range `[0, 1.0]`.

```python
light.read()
```

```python
from pibody import Light  # short alias

light = Light("C")

while True:
    print("light value:", light.read())
```

---
### `.read_u16() -> int`
Read the raw ADC value in range `[0, 65535]`.

```python
data = light.read_u16()
print(data)
```

---
### `.read_uv() -> int`
Read the ADC value converted to microvolts.

```python
data = light.read_uv()
print(data)
```

---
### `.deinit()`
Disable the ADC and release the pin for alternative use.

```python
light.deinit()
```
