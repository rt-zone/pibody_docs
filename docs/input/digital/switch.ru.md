---
title: Переключатель
---
# Переключатель
Переключатель — это простой механизм, который управляет потоком электрического тока.

---
### `Switch(slot) -> Pin`
Чтобы создать объект Switch, вызовите `Switch(slot)`.

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "C", "D", "E", "F", "G", "H"), порт пина (0, 2 и т.д.), кортеж (0, Pin.IN).

**Возвращает:**
    Возвращает цифровой выход ``Pin`` для *slot*.
```python
from pibody import Switch

switch = Switch("A")
```

---
### `.read() -> int`
Возвращает **0 или 1** в зависимости от состояния.

```python
switch.read()
```

```python
from pibody import Switch

switch = Switch("A")

while True:
    if switch.read():
        print("Переключатель включён")
    else:
        print("Переключатель выключен")
```

---
### `.value() -> int`
То же, что и `.read()`, возвращает **0 или 1** в зависимости от состояния.

```python
value = switch.value()
print(value)
```
