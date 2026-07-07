---
title: Potentiometer
canonical: potentiometer
class_name: Potentiometer
lesson_id: 39
category: input
subcategory: analog
interface: ADC
aliases: [Pot]
ports: [C, F]
prompt_note: "ADC input (read/read_u16)"
---
# Potentiometer
Potentiometer (variable resistor) is similar to a regular resistor, but its resistance can be adjusted. By turning the knob, you regulate the amount of resistance.

---
### `Potentiometer(slot) -> ADC`
To create a Potentiometer object, call `Potentiometer(slot)`.

Also you can use short alias `Pot(slot)`.

Since the potentiometer is analog, it can only be inserted into slots with an ADC (analog-to-digital converter), and there are only 2 such slots on the PiBody: `"C"` and `"F"`.

**Args:**

- `slot (string)` - slot label ("C", "F").

**Returns:**
    Return an ``ADC`` object for the analogue pin of *slot*.

```python
from pibody import Potentiometer

pot = Potentiometer("C")
```

---
### `.read() -> float`
Returns value in range **[0, 1.0]**.

```python
pot.read()
```

```python
from pibody import Pot  # short alias

pot = Pot("C")

while True:
    print("potentiometer value:", pot.read())
```

---
### `.read_u16() -> int`
Read the raw ADC value in range **[0, 65535]**.

```python
data = pot.read_u16()
print(data)
```

---
### `.read_uv() -> int`
Read the ADC value converted to microvolts.

```python
data = pot.read_uv()
print(data)
```

---
### `.deinit()`
Disable the ADC and release the pin for alternative use.

```python
pot.deinit()
```
