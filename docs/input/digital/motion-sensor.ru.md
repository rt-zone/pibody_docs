---
title: Датчик движения
---
# Датчик движения
Датчик движения — это устройство, которое обнаруживает движение.

---
### `MotionSensor(slot) -> Pin`
Чтобы создать объект MotionSensor, вызовите `MotionSensor(slot)`.

Также можно использовать короткий вызов `Motion(slot)`.

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "C", "D", "E", "F", "G", "H"), порт пина (0, 2 и т.д.), кортеж (0, Pin.IN).

**Возвращает:**
    Возвращает цифровой выход ``Pin`` для *slot*.

```python
from pibody import MotionSensor

motion = MotionSensor("A")
```

---
### `.read() -> int`
Возвращает **0 или 1** в зависимости от состояния.

```python
motion.read()
```

```python
from pibody import Motion  # короткий вызов

motion = Motion("A")

while True:
    if motion.read():
        print("Движение обнаружено")
    else:
        print("Движение не обнаружено")
```

---
### `.value() -> int`
То же, что и `.read()`, возвращает **0 или 1** в зависимости от состояния.

```python
value = motion.value()
print(value)
```
