---
title: Color Sensor
---
# Color Sensor
Color Sensor — a high-precision device that measures the color of an object and the intensity of ambient light (similar to a light sensor). It determines the intensity of the 3 primary light spectra — red, green, and blue (RGB). Ideal for color detection and monitoring light intensity.

---
## Basic usage

---
### `ColorSensor(slot)`
To create ColorSensor object call `ColorSensor(slot)`.

Also you can use short alias `Color(slot)`.

You can choose any other slot (except `"C"`, as it does not support I2C communication).

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a class ``VEML6040`` for *slot*.
```python
from pibody import ColorSensor

color = ColorSensor("A")
```

---
### `.read() -> dict`
Return a combined RGB + HSV reading.  
Returns dictionary with the following key-values:

- `red` - red int value **[0, 255]**
- `green` - green int value **[0, 255]**
- `blue` - blue int value **[0, 255]**
- `hue` - hue float value **[0, 360]**
- `sat` - sat float value **[0, 1]**
- `val` - value (brightness) float value **[0, 1]**

```python
from pibody import Color   # short alias
color = Color('A')

data = color.read()				  

print(data)
```

---
### `.readRGB() -> (int, int, int)`
Return colour-corrected (r, g, b) in **[0, 255]**.

```python
from pibody import Color
color = Color('A')

r, g, b = color.readRGB()
print(r, g, b)
```

---
### `.readHSV() -> (int, int, int)`
Returns (hue, saturation, value) derived from `readRGB()`.  
HSV values in range **[0, 255]**.

```python
from pibody import Color
color = Color('A')

h, s, v = color.readHSV()
print(h, s, v)
```

---
### `.detectColor() -> string`
Classify the detected colour by nearest hue.

**Args:**

- `hues (string | int | tuple | None)` - dict mapping colour name - hue in degrees. Default is **red/yellow/green/light-blue/blue/magenta**
- `min_brightness (float | None)` - optional parameter which is used to determine the minimum brightness at which a color is detected. By default is **0.5**

```python
from pibody import Color
color = Color('A')

detected_color = color.detectColor()
print(detected_color)  # ex. red
```

---
## Other Functions

---
### `.lux() -> float`
Return ambient light level in lux. Output in range **[0, 16494]**.

```python
from pibody import Color
color = Color('A')

lux = color.lux()
print(lux)
```

---
### `.readRawData() -> dict`
Returns raw red, green and blue readings, ambient light [Lux] and colour temperature [K].

Returns dictionary with the following key-values:

- `red` - red int value **[0, 65535]**
- `green` - green int value **[0, 65535]**
- `blue` - blue int value **[0, 65535]**
- `white` - white float value **[0, 65535]**
- `als` - als float value **[0, 16494]**
- `cct` - cct float value

```python
from pibody import Color
color = Color('A')

data = color.readRawData()
print(data)
```

---
## Additional info

### Default colour hues for `detectColor()`

The table below shows the default hue values used by `detectColor()` to classify a colour. You can override these by passing a custom `hues` dict to the method.

| Colour      | Hue (°) |
|-------------|---------|
| <span style="color: #FF0000; font-weight: bold;">Red</span>        | 0       |
| <span style="color: #FFFF00; font-weight: bold;">Yellow</span>     | 60      |
| <span style="color: #00FF00; font-weight: bold;">Green</span>      | 120     |
| <span style="color: #00FFFF; font-weight: bold;">Light Blue</span> | 180     |
| <span style="color: #0000FF; font-weight: bold;">Blue</span>       | 240     |
| <span style="color: #FF00FF; font-weight: bold;">Magenta</span>    | 300     |
