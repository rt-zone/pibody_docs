---
title: Ауыстырғыш
---
# Ауыстырғыш
Ауыстырғыш — бұл электр тогының ағынын басқаратын қарапайым механизм.

---
### `Switch(slot) -> Pin`
Switch объектісін жасау үшін `Switch(slot)` шақырыңыз.

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "C", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN).

**Қайтарады:**
    *slot* үшін сандық шығыс ``Pin`` қайтарады.
```python
from pibody import Switch

switch = Switch("A")
```

---
### `.read() -> int`
Күйіне байланысты **0 немесе 1** қайтарады.

```python
switch.read()
```

```python
from pibody import Switch

switch = Switch("A")

while True:
    if switch.read():
        print("Ауыстырғыш қосылды")
    else:
        print("Ауыстырғыш өшірілді")
```

---
### `.value() -> int`
`.read()` сияқты, күйіне байланысты **0 немесе 1** қайтарады.

```python
value = switch.value()
print(value)
```
