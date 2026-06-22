---
title: Гироскоп-Акселерометр
---
# Гироскоп-Акселерометр
Модуль гироскопа и акселерометра — это миниатюрное устройство, объединяющее два важных датчика: 3-осевой акселерометр (измеряет линейное движение) и 3-осевой гироскоп (измеряет вращение). Широко используется в робототехнике, дронах, смартфонах и игровых контроллерах для обнаружения движения и ориентации.

---
## Базовое использование

---
### `GyroAccel(slot)`
Чтобы создать объект GyroAccel, вызовите `GyroAccel(slot)`.

Вы можете выбрать любой другой слот (кроме `"C"`, так как он не поддерживает связь по I2C).

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "D", "E", "F", "G", "H"), порт пина (0, 2 и т.д.), кортеж (0, Pin.IN)

**Возвращает:**
    Возвращает объект ``MPU6050`` для *slot*. В старых наборах PiBody может быть ``LSM6DS3`` с устаревшими функциями.
```python
from pibody import GyroAccel

imu = GyroAccel("A")
```

---
### `.read() -> (float, tuple, tuple)`
Возвращает словарь со следующими ключами:

- `temp (float)` — температура в °C **[-40, 85]**
- `accel (float, float, float)` — ускорение в g **[-2, 2]** в виде кортежа **(ax, ay, az)**
- `gyro (float, float, float)` — угловая скорость в °/с **[-250, 250]** в виде кортежа **(gx, gy, gz)**

```python
from pibody import GyroAccel
imu = GyroAccel('A')

data = imu.read()

print(data)
```

---
### `.read_accel() -> (float, float, float)`
Возвращает ускорение в g **[-2, 2]**.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

x, y, z = imu.read_accel()
print(x, y, z)
```

---
### `.read_gyro() -> (float, float, float)`
Возвращает угловую скорость в °/с **[-250, 250]**.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

x, y, z = imu.read_gyro()
print(x, y, z)
```

---
### `.read_temperature() -> float`
Возвращает температуру в °C **[-40, 85]**.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

temp = imu.read_temperature()
print(temp)
```

---
## Другие функции

---
### `.sleep()`
Переводит датчик в режим сна.

```python
imu.sleep()
```

---
### `.wake()`
Пробуждает датчик из режима сна.

```python
imu.wake()
```

---
### `.add_tilt_listener(direction, callback)`
Регистрирует callback для направления наклона.

**Аргументы:**

- `direction (string)` — одно из **"forward"**, **"backward"**, **"left"**, **"right"**
- `callback` — вызываемый объект без аргументов, вызываемый при обнаружении наклона

**Вызывает:**
- ValueError: Если *direction* не является одной из четырёх допустимых строк.

```python
imu.add_tilt_listener('forward', cb)
```

---
### `.check_tilt()`
Читает акселерометр и запускает все зарегистрированные callback'и наклона.

Должен вызываться периодически из основного цикла.

```python
from pibody import GyroAccel
from time import sleep

imu = GyroAccel('A')

forward = lambda: print('вперёд')
backward = lambda: print('назад')
left = lambda: print('влево')
right = lambda: print('вправо')

imu.add_tilt_listener('forward', forward)
imu.add_tilt_listener('backward', backward)
imu.add_tilt_listener('left', left)
imu.add_tilt_listener('right', right)

while True:
    imu.check_tilt()
    sleep(0.1)
```
