---
title: Gyro Accel
---
# Gyro Accel
The Gyroscope and Accelerometer module is a tiny device that combines two important sensors: a 3-axis accelerometer (measures linear motion) and a 3-axis gyroscope (measures rotation). It is widely used in robotics, drones, smartphones, and game controllers to detect motion and orientation.

---
## Basic usage

---
### `GyroAccel(slot)`
To create GyroAccel object call `GyroAccel(slot)`.

You can choose any other slot (except `"C"`, as it does not support I2C communication).

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a class ``MPU6050`` for *slot*. In old PiBody kits may be ``LSM6DS3`` with deprecated functions.
```python
from pibody import GyroAccel

imu = GyroAccel("A")
```

---
### `.read() -> (float, tuple, tuple)`
Returns dictionary with the following key-values:

- `temp (float)` - temperature in ºC `[-40, 85]`
- `accel (float, float, float)` - acceleration in g `[-2, 2]` as a tuple `(ax, ay, az)`
- `gyro (float, float, float)` - angular speed in º/s `[-250, 250]` as a tuple `(gx, gy, gz)`

```python
from pibody import GyroAccel
imu = GyroAccel('A')

data = imu.read()

print(data)
```

---
### `.read_accel() -> (float, float, float)`
Returns acceleration in g `[-2, 2]`.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

x, y, z = imu.read_accel()
print(x, y, z)
```

---
### `.read_gyro() -> (float, float, float)`
Returns angular speed in º/s `[-250, 250]`.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

x, y, z = imu.read_gyro()
print(x, y, z)
```

---
### `.read_temperature() -> float`
Returns temperature in ºC `[-40, 85]`.

```python
from pibody import GyroAccel
imu = GyroAccel('A')

temp = imu.read_temperature()
print(temp)
```

---
## Other Functions

---
### `.sleep()`
Put the sensor into sleep mode.

```python
imu.sleep()
```

---
### `.wake()`
Wake the sensor from sleep mode.

```python
imu.wake()
```

---
### `.add_tilt_listener(direction, callback)`
Register a callback for a tilt direction.

**Args**:

- `direction (string)` - one of `"forward"`, `"backward"`, `"left"`, `"right"`
- `callback` - zero-argument callable invoked when tilt is detected

**Raises**:
- ValueError: If *direction* is not one of the four valid strings.

```python
imu.add_tilt_listener('forward', cb)
```

---
### `.check_tilt()`
Read accelerometer and fire any registered tilt callbacks.

Should be called periodically from the main loop.

```python
from pibody import GyroAccel
from time import sleep

imu = GyroAccel('A')

forward = lambda: print('forward')
backward = lambda: print('backward')
left = lambda: print('left')
right = lambda: print('right')

imu.add_tilt_listener('forward', forward)
imu.add_tilt_listener('backward', backward)
imu.add_tilt_listener('left', left)
imu.add_tilt_listener('right', right)

while True:
    imu.check_tilt()
    sleep(0.1)
```
