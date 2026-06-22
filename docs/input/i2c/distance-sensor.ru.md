---
title: Датчик расстояния
---
# Датчик расстояния
Датчик расстояния — это активный датчик, который измеряет расстояние до объекта с высокой точностью. Датчик использует инфракрасный лазер и фиксирует время, за которое лазер возвращается обратно.

---
## Базовое использование

---
### `DistanceSensor(slot)`
Чтобы создать объект DistanceSensor, вызовите `DistanceSensor(slot)`.

Также можно использовать короткий псевдоним `Distance(slot)`.

Вы можете выбрать любой другой слот (кроме `"C"`, так как он не поддерживает связь по I2C).

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "D", "E", "F", "G", "H"), порт пина (0, 2 и т.д.), кортеж (0, Pin.IN)

**Возвращает:**
    Возвращает объект ``VL53L0X`` для *slot*.
```python
from pibody import DistanceSensor

distance = DistanceSensor("A")
```

---
### `.read() -> int`
Выполняет одно измерение дальности.  
Возвращает расстояние в мм **[20, 2000]**.  
Возвращает `20` или `8190` при некорректном измерении.

```python
from pibody import Distance   # короткий псевдоним
distance = Distance('A')

data = distance.read()

print(data)
```

---
### `.is_valid(distance) -> bool`
Параметр `distance` обязателен и должен содержать фактическое расстояние в мм.

Возвращает **True** или **False**, если измерения находятся в диапазоне между `.min_valid_mm` и `.max_valid_mm`.  
`.min_valid_mm` по умолчанию равен **30**.  
`.max_valid_mm` по умолчанию равен **2000**.  
Эти переменные можно изменять.

```python
from pibody import Distance   # короткий псевдоним
distance = Distance('A')

distance.min_valid_mm = 50
distance.max_valid_mm = 200

curr_dist = distance.read()

valid = distance.is_valid(curr_dist)
print(valid)
```

---
## Другие функции

---
### `.bar() -> string`
Возвращает текстовый индикатор выполнения текущего расстояния.

**Аргументы:**

- `max_range (int | None)` — расстояние (мм), соответствующее полной шкале. По умолчанию: **200** мм
- `width (int | None)` — ширина индикатора в символах. По умолчанию: **20** символов
- `fill_char (string | None)` — символ, используемый для заполненной части. По умолчанию: **"#"**
- `empty_char (string | None)` — символ, используемый для пустой части. По умолчанию: **" "**

```python
from pibody import Distance   # короткий псевдоним
distance = Distance('A')

bar = distance.bar()

print(bar) # [######  ] 75 mm
```

---
### `.add_close_trigger(threshold_mm, callback)`
Регистрирует callback, вызываемый, когда объект находится ближе *threshold_mm*.

**Аргументы:**

- `threshold_mm (int)` — порог расстояния в мм
- `callback` — вызывается с текущим расстоянием (мм)

```python
distance.add_close_trigger(100, cb)
```

---
### `.add_motion_trigger(change_threshold_mm, callback, cooldown_ms)`
Регистрирует callback, вызываемый, когда расстояние изменяется более чем на *change_threshold_mm* между последовательными вызовами check().

**Аргументы:**

- `change_threshold_mm (int)` — минимальное изменение (мм) для срабатывания
- `callback` — вызывается с (distance_mm, delta_mm)
- `cooldown_ms` — минимальное время в мс между последовательными срабатываниями. По умолчанию: **500**

```python
distance.add_motion_trigger(100, cb)
```

---
### `.check()`
Читает расстояние и запускает все зарегистрированные callback'и.

Должен вызываться периодически из основного цикла.
Некорректные показания игнорируются.

```python
distance.add_motion_trigger(100, cb)

while True:
    distance.check()				  
```
