---
title: Жанасу сенсоры
---
# Жанасу сенсоры
Жанасу сенсоры — бұл саусақтың немесе өткізгіш заттың тиюін анықтайтын түйме. Механикалық түймелерден айырмашылығы, оның қозғалатын бөліктері жоқ, бұл оны берік әрі сенімді етеді.

---
### `TouchSensor(slot) -> Pin`
TouchSensor объектісін жасау үшін `TouchSensor(slot)` шақырыңыз.

Сондай-ақ `Touch(slot)` қысқа атауын пайдалануға болады.

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "C", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN).

**Қайтарады:**
    *slot* үшін сандық шығыс ``Pin`` қайтарады.
```python
from pibody import TouchSensor

touch = TouchSensor("A")
```

---
### `.read() -> int`
Күйіне байланысты **0 немесе 1** қайтарады.

```python
touch.read()
```

```python
from pibody import Touch  # қысқа атау

touch = Touch("A")

while True:
    if touch.read():
        print("Сенсор басылды")
    else:
        print("Сенсор басылмады")
```

---
### `.value() -> int`
`.read()` сияқты, күйіне байланысты **0 немесе 1** қайтарады.

```python
value = touch.value()
print(value)
```
