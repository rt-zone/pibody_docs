---
title: LED Tower
---
# LED Tower
LED Tower — это лента из 8 светодиодов. Каждый светодиод можно управлять индивидуально, изменяя его цвет. Этот модуль отлично подходит для создания индикаторов и световых анимаций.

---
## Базовое использование

---
### `LEDTower(slot) -> NeoPixel`
Чтобы создать объект LEDTower, вызовите `LEDTower(slot)`.

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "C", "D", "E", "F", "G", "H"), порт пина (8, 9, 0, 1 и т.д.), кортеж (0, Pin.OUT)

**Возвращает:**
    Возвращает объект ``NeoPixel`` для адресуемой светодиодной ленты на *slot*.
```python
from pibody import LEDTower

tower = LEDTower(8)
```

---
### `.write()`
Отправляет данные о цвете на светодиодную ленту. Должен вызываться после установки цветов LED для применения изменений.

```python
tower.write()
```

---
### `.fill(color)`
Используйте функцию `.fill()`, чтобы зажечь все 8 светодиодов на башне определённым цветом.

См. список цветов в разделе *Дополнительная информация*.

```python
tower.fill(tower.GREEN)  # зелёный
tower.write()            # обновить состояние
```

---
## Другие функции

---
### Установка одного светодиода
Устанавливает цвет отдельного светодиода. Принимает кортеж цвета **(r, g, b)** или可以使用 предустановленные цвета.

```python
tower[0] = tower.GREEN  # зелёный

tower[0] = (0, 255, 0)  # тоже зелёный

tower.write()            # не забудьте обновить состояние
```

---
### Получение одного светодиода
Возвращает кортеж цвета **(r, g, b)** светодиода.

```python
led0 = tower[0]
print(led0)
```

---
## Дополнительная информация

---
### Предустановленные цвета LEDTower
| Название | Кортеж |
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
