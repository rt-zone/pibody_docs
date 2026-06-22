---
title: LED Tower
---
# LED Tower
LED Tower — 8 жарықдиодтан тұратын лента. Әрбір жарықдиодты оның түсін өзгерту арқылы жеке басқаруға болады. Бұл модуль индикаторлар мен жарық анимацияларын жасау үшін өте қолайлы.

---
## Негізгі қолдану

---
### `LEDTower(slot) -> NeoPixel`
LEDTower объектісін жасау үшін `LEDTower(slot)` шақырыңыз.

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "C", "D", "E", "F", "G", "H"), пин порты (8, 9, 0, 1 және т.б.), кортеж (0, Pin.OUT)

**Қайтарады:**
    *slot* мекенжайланатын жарықдиодты лента үшін ``NeoPixel`` объектісін қайтарады.
```python
from pibody import LEDTower

tower = LEDTower(8)
```

---
### `.write()`
Түс деректерін жарықдиодты лентаға жібереді. Өзгерістерді қолдану үшін жарықдиодтардың түстерін орнатқаннан кейін шақырылуы керек.

```python
tower.write()
```

---
### `.fill(color)`
Мұнарадағы барлық 8 жарықдиодты белгілі бір түсте жағу үшін `.fill()` функциясын пайдаланыңыз.

Түстер тізімін *Қосымша ақпарат* бөлімінен қараңыз.

```python
tower.fill(tower.GREEN)  # жасыл
tower.write()            # күйді жаңарту
```

---
## Басқа функциялар

---
### Бір жарықдиодты орнату
Жеке жарықдиодтың түсін орнатады. Түс кортежін **(r, g, b)** немесе алдын ала орнатылған түстерді пайдалануға болады.

```python
tower[0] = tower.GREEN  # жасыл

tower[0] = (0, 255, 0)  # жасыл (альтернатива)

tower.write()            # күйді жаңартуды ұмытпаңыз
```

---
### Бір жарықдиодты алу
Жарықдиодтың түс кортежін **(r, g, b)** қайтарады.

```python
led0 = tower[0]
print(led0)
```

---
## Қосымша ақпарат

---
### LEDTower алдын ала орнатылған түстері
| Атауы | Кортеж |
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
