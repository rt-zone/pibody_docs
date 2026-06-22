---
title: Гиро Аксель
---
# Гиро Аксель
Гироскоп және акселерометр модулі — бұл екі маңызды сенсорды біріктіретін шағын құрылғы: 3 осьті акселерометр (сызықтық қозғалысты өлшейді) және 3 осьті гироскоп (айналуды өлшейді). Ол робототехникада, дрондарда, смартфондарда және ойын контроллерлерінде қозғалыс пен бағдарды анықтау үшін кеңінен қолданылады.

---
## Негізгі қолдану

---
### `GyroAccel(slot)`
GyroAccel объектісін жасау үшін `GyroAccel(slot)` шақырыңыз.

Кез келген басқа слотты таңдауға болады (`"C"`-дан басқа, себебі ол I2C байланысын қолдамайды).

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.OUT)

**Қайтарады:**
    *slot* үшін ``MPU6050`` класын қайтарады. Ескі PiBody жинақтарында ескірген функциялары бар ``LSM6DS3`` болуы мүмкін.
```python
from pibody import GyroAccel

imu = GyroAccel("A")
```

---
### `.read() -> (float, tuple, tuple)`
Келесі кілт-мәндері бар сөздікті қайтарады:

- `temp (float)` — температура °C **[-40, 85]**
- `accel (float, float, float)` — үдеу g **[-2, 2]** кортеж түрінде **(ax, ay, az)**
- `gyro (float, float, float)` — бұрыштық жылдамдық °/с **[-250, 250]** кортеж түрінде **(gx, gy, gz)**

```python
from pibody import GyroAccel
imu = GyroAccel('A')

data = imu.read()

print(data)
```

---
### `.read_accel() -> (float, float, float)`
Үдеуді g **[-2, 2]** қайтарады.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

x, y, z = imu.read_accel()
print(x, y, z)
```

---
### `.read_gyro() -> (float, float, float)`
Бұрыштық жылдамдықты °/с **[-250, 250]** қайтарады.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

x, y, z = imu.read_gyro()
print(x, y, z)
```

---
### `.read_temperature() -> float`
Температураны °C **[-40, 85]** қайтарады.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

temp = imu.read_temperature()
print(temp)
```

---
## Басқа функциялар

---
### `.sleep()`
Сенсорды ұйқы режиміне ауыстырады.

```python
imu.sleep()
```

---
### `.wake()`
Сенсорды ұйқы режимінен оятады.

```python
imu.wake()
```

---
### `.add_tilt_listener(direction, callback)`
Еңкейту бағыты үшін callback тіркейді.

**Аргументтер:**

- `direction (string)` — **"forward"**, **"backward"**, **"left"**, **"right"** біреуі
- `callback` — еңкейту анықталғанда шақырылатын аргументсіз шақырылатын функция

**Қате:**
- ValueError: Егер *direction* төрт жолдың біреуі болмаса.

```python
imu.add_tilt_listener('forward', cb)
```

---
### `.check_tilt()`
Акселерометрді оқиды және барлық тіркелген еңкейту callback'терін іске қосады.

Негізгі циклден мерзімді түрде шақырылуы керек.

```python
from pibody import GyroAccel
from time import sleep

imu = GyroAccel('A')

forward = lambda: print('алға')
backward = lambda: print('артқа')
left = lambda: print('солға')
right = lambda: print('оңға')

imu.add_tilt_listener('forward', forward)
imu.add_tilt_listener('backward', backward)
imu.add_tilt_listener('left', left)
imu.add_tilt_listener('right', right)

while True:
    imu.check_tilt()
    sleep(0.1)
```
