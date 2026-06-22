---
title: Қозғалыс сенсоры
---
# Қозғалыс сенсоры
Қозғалыс сенсоры — бұл қозғалысты анықтайтын құрылғы.

---
### `MotionSensor(slot) -> Pin`
MotionSensor объектісін жасау үшін `MotionSensor(slot)` шақырыңыз.

Сондай-ақ `Motion(slot)` қысқа атауын пайдалануға болады.

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "C", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN).

**Қайтарады:**
    *slot* үшін сандық шығыс ``Pin`` қайтарады.

```python
from pibody import MotionSensor

motion = MotionSensor("A")
```

---
### `.read() -> int`
Күйіне байланысты **0 немесе 1** қайтарады.

```python
motion.read()
```

```python
from pibody import Motion  # қысқа атау

motion = Motion("A")

while True:
    if motion.read():
        print("Қозғалыс анықталды")
    else:
        print("Қозғалыс анықталмады")
```

---
### `.value() -> int`
`.read()` сияқты, күйіне байланысты **0 немесе 1** қайтарады.

```python
value = motion.value()
print(value)
```
