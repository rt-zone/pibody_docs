---
title: LED Tower
canonical: led-tower
class_name: LEDTower
lesson_id: 62
category: output
interface: GPIO
ports: [G, H, 8, 9]
prompt_note: "NeoPixel strip (write/fill)"
---
# LED Tower
LED Tower — is a strip consisting of 8 LEDs. Each LED can be controlled individually by changing its color. This module is perfect for creating indicators and light animations.

---
## Basic usage

---
### `LEDTower(slot) -> NeoPixel`
To create a LEDTower object, call `LEDTower(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (8, 9, 0, 1 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a ``NeoPixel`` object for the addressable-LED strip on *slot*.
```python
from pibody import LEDTower

tower = LEDTower(8)
```

---
### `.write()`
Sends the color data to the LED strip. Must be called after setting LED colors to apply changes.

```python
tower.write()
```

---
### `.fill(color)`
Use the `.fill()` function to make all 8 LEDs on the tower light up in a specific color.

See color list ad *Additional info*.

```python
tower.fill(tower.GREEN)  # green
tower.write()            # update state
```

---
## Other Functions

---
### Set up one LED item
Sets the color of an individual LED. Accepts color tuple **(r, g, b)** or you can use preset colors.

```python
tower[0] = tower.GREEN  # green

tower[0] = (0, 255, 0)  # also green

tower.write()            # don't forget to update state
```

---
### Get one LED item
Returns color tuple **(r, g, b)** of the LED.

```python
led0 = tower[0]
print(led0)
```

---
## Additional info

---
### LEDTower preset colors
| Title | Tuple |
|---|---|
| LEDTower.<span style="color: #FFFFFF; font-weight: bold;">WHITE</span>   | (255, 255, 255) |
| LEDTower.<span style="color: #000000; font-weight: bold;">BLACK</span>   | (0, 0, 0)       |
| LEDTower.<span style="color: #FF0000; font-weight: bold;">RED</span>     | (255, 0, 0)     |
| LEDTower.<span style="color: #00FF00; font-weight: bold;">GREEN</span>   | (0, 255, 0)     |
| LEDTower.<span style="color: #0000FF; font-weight: bold;">BLUE</span>    | (0, 0, 255)     |
| LEDTower.<span style="color: #FFFF00; font-weight: bold;">YELLOW</span>  | (255, 255, 0)   |
| LEDTower.<span style="color: #00FFFF; font-weight: bold;">CYAN</span>    | (0, 255, 255)   |
| LEDTower.<span style="color: #FF00FF; font-weight: bold;">MAGENTA</span> | (255, 0, 255)   |
| LEDTower.<span style="color: #FFA500; font-weight: bold;">ORANGE</span>  | (255, 165, 0)   |
| LEDTower.<span style="color: #800080; font-weight: bold;">PURPLE</span>  | (128, 0, 128)   |
| LEDTower.<span style="color: #FFC0CB; font-weight: bold;">PINK</span>    | (255, 192, 203) |
| LEDTower.<span style="color: #00FF80; font-weight: bold;">LIME</span>    | (0, 255, 128)   |
| LEDTower.<span style="color: #008080; font-weight: bold;">TEAL</span>    | (0, 128, 128)   |
| LEDTower.<span style="color: #8B4513; font-weight: bold;">BROWN</span>   | (139, 69, 19)   |
