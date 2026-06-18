---
title: Climate Sensor
---
# Climate Sensor
Climate sensor is a smart device that can measure temperature, atmospheric pressure, and humidity.

---
## Basic usage

---
### `ClimateSensor(slot)`
To create ClimateSensor object call `ClimateSensor(slot)`.

Also you can use short alias `Climate(slot)`.

You can choose any other slot (except `"C"`, as it does not support I2C communication).

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a class ``BME280`` for *slot*.
```python
from pibody import ClimateSensor

climate = ClimateSensor("A")
```

---
### `.read() -> (float, float, float)`
Returns dictionary with the following key-values:

- `temperature` - temperature in °C `[-40, 85]`
- `humidity` - humidity in %RH `[0, 100]`
- `pressure` - pressure in hPa `[0, 20000]`

```python
from pibody import Climate  # short alias
climate = Climate('A')

data = climate.read() 

temp = data['temperature']
hum = data['humidity']
pres = data['pressure']					  

print(f"temp: {temp}, hum: {hum}, pres: {pres}")
```

---
### `.read_temperature() -> float`
Return compensated temperature in °C `[-40, 85]`.

```python
temp = climate.read_temperature()
print(temp)
```

---
### `.read_humidity() -> float`
Return compensated relative humidity in %RH `[0, 100]`.

```python
hum = climate.read_humidity()
print(hum)
```

---
### `.read_pressure() -> float`
Return compensated pressure in hPa `[0, 20000]`.

```python
press = climate.read_pressure()
print(press)
```

---
## Other Functions

---
### `.read_raw_temp() -> int`
Return the raw (uncompensated) temperature ADC value.

```python
temp = climate.read_raw_temp()
print(press)
```

---
### `.read_raw_humidity() -> int`
Return the raw (uncompensated) humidity ADC value.

```python
hum = climate.read_raw_humidity()
print(hum)
```

---
### `.read_raw_pressure() -> int`
Return the raw (uncompensated) pressure ADC value.

```python
press = climate.read_raw_pressure()
print(press)
```
