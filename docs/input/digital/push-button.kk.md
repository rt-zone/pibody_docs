---
title: Түйме
---
# Түйме
Түйме — бұл ток ағынын басқару үшін қолданылатын қарапайым ауыстыру механизмі. Түйме басылғанда, электр тізбегі тұйықталып, токтың өтуіне мүмкіндік береді.

---
### `Button(slot) -> Pin`
Button объектісін жасау үшін `Button(slot)` шақырыңыз.

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "C", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN).

**Қайтарады:**
    *slot* үшін сандық шығыс ``Pin`` қайтарады.
```python
from pibody import Button

button = Button("A")
```

---
### `.read() -> int`
Күйіне байланысты **0 немесе 1** қайтарады.

```python
button.read()
```

```python
from pibody import Button

button = Button("A")

while True:
    if button.read():
        print("Түйме басылды")
    else:
        print("Түйме басылмады")
```

---
### `.value() -> int`
`.read()` сияқты, күйіне байланысты **0 немесе 1** қайтарады.

```python
value = button.value()
print(value)
```
