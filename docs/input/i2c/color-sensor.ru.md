---
title: Датчик цвета
---
# Датчик цвета
Датчик цвета — это высокоточное устройство, которое измеряет цвет объекта и интенсивность окружающего света (аналогично датчику освещённости). Он определяет интенсивность 3 основных спектров света — красного, зелёного и синего (RGB). Идеально подходит для определения цвета и контроля интенсивности света.

---
## Базовое использование

---
### `ColorSensor(slot)`
Чтобы создать объект ColorSensor, вызовите `ColorSensor(slot)`.

Также можно использовать короткий вызов `Color(slot)`.

Вы можете выбрать любой другой слот (кроме `"C"`, так как он не поддерживает связь по I2C).

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "D", "E", "F", "G", "H"), порт пина (0, 2 и т.д.), кортеж (0, Pin.OUT)

**Возвращает:**
    Возвращает класс ``VEML6040`` для *slot*.
```python
from pibody import ColorSensor

color = ColorSensor("A")
```

---
### `.read() -> dict`
Возвращает комбинированное показание RGB + HSV.  
Возвращает словарь со следующими ключами:

- `red` — красный int значение **[0, 255]**
- `green` — зелёный int значение **[0, 255]**
- `blue` — синий int значение **[0, 255]**
- `hue` — тон float значение **[0, 360]**
- `sat` — насыщенность float значение **[0, 1]**
- `val` — яркость float значение **[0, 1]**

```python
from pibody import Color   # короткий вызов
color = Color('A')

data = color.read()				  

print(data)
```

---
### `.readRGB() -> (int, int, int)`
Возвращает скорректированные значения (r, g, b) в **[0, 255]**.

```python
from pibody import Color
color = Color('A')

r, g, b = color.readRGB()
print(r, g, b)
```

---
### `.readHSV() -> (int, int, int)`
Возвращает (hue, saturation, value), полученные из `readRGB()`.  
Значения HSV в диапазоне **[0, 255]**.

```python
from pibody import Color
color = Color('A')

h, s, v = color.readHSV()
print(h, s, v)
```

---
### `.detectColor() -> string`
Классифицирует обнаруженный цвет по ближайшему тону.

**Аргументы:**

- `hues (string | int | tuple | None)` — словарь, сопоставляющий название цвета с тоном в градусах. По умолчанию: **red/yellow/green/light-blue/blue/magenta**
- `min_brightness (float | None)` — необязательный параметр для определения минимальной яркости, при которой обнаруживается цвет. По умолчанию: **0.5**

```python
from pibody import Color
color = Color('A')

detected_color = color.detectColor()
print(detected_color)  # например, red
```

---
## Другие функции

---
### `.lux() -> float`
Возвращает уровень окружающего освещения в люксах. Диапазон вывода **[0, 16494]**.

```python
from pibody import Color
color = Color('A')

lux = color.lux()
print(lux)
```

---
### `.readRawData() -> dict`
Возвращает сырые значения красного, зелёного и синего каналов, освещённость [Люкс] и цветовую температуру [K].

Возвращает словарь со следующими ключами:

- `red` — красный int значение **[0, 65535]**
- `green` — зелёный int значение **[0, 65535]**
- `blue` — синий int значение **[0, 65535]**
- `white` — белый float значение **[0, 65535]**
- `als` — освещённость float значение **[0, 16494]**
- `cct` — цветовая температура float значение

```python
from pibody import Color
color = Color('A')

data = color.readRawData()
print(data)
```

---
## Дополнительная информация

### Стандартные оттенки цветов для `detectColor()`

В таблице ниже приведены стандартные значения тонов, используемые `detectColor()` для классификации цвета. Вы можете переопределить их, передав собственный словарь `hues` в метод.

| Цвет          | Тон (°) |
|---------------|---------|
| <span style="color: #FF0000; font-weight: bold;">Красный</span>     | 0       |
| <span style="color: #FFFF00; font-weight: bold;">Жёлтый</span>     | 60      |
| <span style="color: #00FF00; font-weight: bold;">Зелёный</span>     | 120     |
| <span style="color: #00FFFF; font-weight: bold;">Голубой</span>     | 180     |
| <span style="color: #0000FF; font-weight: bold;">Синий</span>       | 240     |
| <span style="color: #FF00FF; font-weight: bold;">Пурпурный</span>   | 300     |
