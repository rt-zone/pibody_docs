---
title: Кнопка
---
# Кнопка
Кнопка — это простой механизм переключения, используемый для управления потоком тока. При нажатии кнопки электрическая цепь замыкается, позволяя току проходить.

---
### `Button(slot) -> Pin`
Чтобы создать объект Button, вызовите `Button(slot)`.

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "C", "D", "E", "F", "G", "H"), порт пина (0, 2 и т.д.), кортеж (0, Pin.IN).

**Возвращает:**
    Возвращает цифровой вход ``Pin`` для *slot*.
```python
from pibody import Button

button = Button("A")
```

---
### `.read() -> int`
Возвращает **0 или 1** в зависимости от состояния.

```python
button.read()
```

```python
from pibody import Button

button = Button("A")

while True:
    if button.read():
        print("Кнопка нажата")
    else:
        print("Кнопка не нажата")
```

---
### `.value() -> int`
То же, что и `.read()`, возвращает **0 или 1** в зависимости от состояния.

```python
value = button.value()
print(value)
```
