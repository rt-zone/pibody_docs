---
title: Түс сенсоры
---
# Түс сенсоры
Түс сенсоры — бұл нысанның түсін және қоршаған орта жарығының қарқындылығын өлшейтін жоғары дәлдікті құрылғы (жарық сенсорына ұқсас). Ол жарықтың 3 негізгі спектрінің — қызыл, жасыл және көк (RGB) қарқындылығын анықтайды. Түсті анықтау және жарық қарқындылығын бақылау үшін өте қолайлы.

---
## Негізгі қолдану

---
### `ColorSensor(slot)`
ColorSensor объектісін жасау үшін `ColorSensor(slot)` шақырыңыз.

Сондай-ақ `Color(slot)` қысқа атауын пайдалануға болады.

Кез келген басқа слотты таңдауға болады (`"C"`-дан басқа, себебі ол I2C байланысын қолдамайды).

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN)

**Қайтарады:**
    *slot* үшін ``VEML6040`` объектісін қайтарады.
```python
from pibody import ColorSensor

color = ColorSensor("A")
```

---
### `.read() -> dict`
Біріктірілген RGB + HSV көрсеткішін қайтарады.  
Келесі кілт-мәндері бар сөздікті қайтарады:

- `red` — қызыл int мәні **[0, 255]**
- `green` — жасыл int мәні **[0, 255]**
- `blue` — көк int мәні **[0, 255]**
- `hue` — реңк float мәні **[0, 360]**
- `sat` — қанықтылық float мәні **[0, 1]**
- `val` — жарықтық float мәні **[0, 1]**

```python
from pibody import Color   # қысқа атау
color = Color('A')

data = color.read()				  

print(data)
```

---
### `.readRGB() -> (int, int, int)`
Түзетілген (r, g, b) мәндерін **[0, 255]** қайтарады.

```python
from pibody import Color
color = Color('A')

r, g, b = color.readRGB()
print(r, g, b)
```

---
### `.readHSV() -> (int, int, int)`
`readRGB()`-ден алынған (hue, saturation, value) мәндерін қайтарады.  
HSV мәндері **[0, 255]** диапазонында.

```python
from pibody import Color
color = Color('A')

h, s, v = color.readHSV()
print(h, s, v)
```

---
### `.detectColor() -> string`
Анықталған түсті ең жақын реңк бойынша жіктейді.

**Аргументтер:**

- `hues (string | int | tuple | None)` — түс атауын реңк градусымен сәйкестендіретін сөздік. Әдепкі: **red/yellow/green/light-blue/blue/magenta**
- `min_brightness (float | None)` — түс анықталатын ең төменгі жарықтықты анықтауға арналған параметр. Әдепкі: **0.5**

```python
from pibody import Color
color = Color('A')

detected_color = color.detectColor()
print(detected_color)  # мыс., red
```

---
## Басқа функциялар

---
### `.lux() -> float`
Қоршаған орта жарық деңгейін люкспен қайтарады. Шығыс диапазоны **[0, 16494]**.

```python
from pibody import Color
color = Color('A')

lux = color.lux()
print(lux)
```

---
### `.readRawData() -> dict`
Қызыл, жасыл және көк арналардың өңделмеген мәндерін, жарықтандыруды [Люкс] және түс температурасын [K] қайтарады.

Келесі кілт-мәндері бар сөздікті қайтарады:

- `red` — қызыл int мәні **[0, 65535]**
- `green` — жасыл int мәні **[0, 65535]**
- `blue` — көк int мәні **[0, 65535]**
- `white` — ақ float мәні **[0, 65535]**
- `als` — жарықтандыру float мәні **[0, 16494]**
- `cct` — түс температурасы float мәні

```python
from pibody import Color
color = Color('A')

data = color.readRawData()
print(data)
```

---
## Қосымша ақпарат

### `detectColor()` үшін стандартты түс реңктері

Төмендегі кестеде `detectColor()` түсті жіктеу үшін пайдаланатын стандартты реңк мәндері көрсетілген. Оларды әдіске өзіңіздің `hues` сөздігін беру арқылы ауыстыруға болады.

| Түс            | Реңк (°) |
|----------------|---------|
| <span style="color: #FF0000; font-weight: bold;">Қызыл</span>      | 0       |
| <span style="color: #FFFF00; font-weight: bold;">Сары</span>       | 60      |
| <span style="color: #00FF00; font-weight: bold;">Жасыл</span>      | 120     |
| <span style="color: #00FFFF; font-weight: bold;">Көгілдір</span>   | 180     |
| <span style="color: #0000FF; font-weight: bold;">Көк</span>        | 240     |
| <span style="color: #FF00FF; font-weight: bold;">Қызғылт</span>    | 300     |
