---
title: Жарық сенсоры
---
# Жарық сенсоры
Жарық сенсоры — бұл аналогты сенсор, оған түсетін жарық деңгейін өлшей алады.

---
### `LightSensor(slot) -> ADC`
LightSensor объектісін жасау үшін `LightSensor(slot)` шақырыңыз.

Сондай-ақ `Light(slot)` қысқа атауын пайдалануға болады.

Жарық сенсоры аналогты болғандықтан, оны тек АЦП (аналогты-цифрлық түрлендіргіш) бар слоттарға қосуға болады, ал PiBody-де осындай 2 слот бар: `"C"` және `"F"`.

**Аргументтер:**

- `slot (string)` — слот белгісі ("C", "F").

**Қайтарады:**
    *slot* аналогты пины үшін ``ADC`` объектісін қайтарады.

```python
from pibody import LightSensor

light = LightSensor("C")
```

---
### `.read() -> float`
**[0, 1.0]** диапазонындағы мәнді қайтарады.

```python
light.read()
```

```python
from pibody import Light  # қысқа атау

light = Light("C")

while True:
    print("жарық мәні:", light.read())
```

---
### `.read_u16() -> int`
АЦП өңделмеген мәнін **[0, 65535]** диапазонында оқиды.

```python
data = light.read_u16()
print(data)
```

---
### `.read_uv() -> int`
Микровольтқа түрлендірілген АЦП мәнін оқиды.

```python
data = light.read_uv()
print(data)
```

---
### `.deinit()`
АЦП өшіріп, пиноты балама пайдалану үшін босатады.

```python
light.deinit()
```
