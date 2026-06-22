---
title: Датчик климата
---
# Датчик климата
Датчик климата — это интеллектуальное устройство, которое может измерять температуру, атмосферное давление и влажность.

---
## Базовое использование

---
### `ClimateSensor(slot)`
Чтобы создать объект ClimateSensor, вызовите `ClimateSensor(slot)`.

Также можно использовать короткий псевдоним `Climate(slot)`.

Вы можете выбрать любой другой слот (кроме `"C"`, так как он не поддерживает связь по I2C).

**Аргументы:**

- `slot (string | int | tuple)` — метка слота ("A", "B", "D", "E", "F", "G", "H"), порт пина (0, 2 и т.д.), кортеж (0, Pin.IN)

**Возвращает:**
    Возвращает объект ``BME280`` для *slot*.
```python
from pibody import ClimateSensor

climate = ClimateSensor("A")
```

---
### `.read() -> (float, float, float)`
Возвращает словарь со следующими ключами:

- `temperature` — температура в °C **[-40, 85]**
- `humidity` — влажность в %RH **[0, 100]**
- `pressure` — давление в гПа **[0, 20000]**

```python
from pibody import Climate  # короткий псевдоним
climate = Climate('A')

data = climate.read() 

temp = data['temperature']
hum = data['humidity']
pres = data['pressure']					  

print(f"temp: {temp}, hum: {hum}, pres: {pres}")
```

---
### `.read_temperature() -> float`
Возвращает компенсированную температуру в °C **[-40, 85]**.

```python
temp = climate.read_temperature()
print(temp)
```

---
### `.read_humidity() -> float`
Возвращает компенсированную относительную влажность в %RH **[0, 100]**.

```python
hum = climate.read_humidity()
print(hum)
```

---
### `.read_pressure() -> float`
Возвращает компенсированное давление в гПа **[0, 20000]**.

```python
press = climate.read_pressure()
print(press)
```

---
## Другие функции

---
### `.read_raw_temp() -> int`
Возвращает сырое (некомпенсированное) значение АЦП температуры. Диапазон вывода **[0, 1048575]**.

```python
temp = climate.read_raw_temp()
print(temp)
```

---
### `.read_raw_humidity() -> int`
Возвращает сырое (некомпенсированное) значение АЦП влажности. Диапазон вывода **[0, 65535]**.

```python
hum = climate.read_raw_humidity()
print(hum)
```

---
### `.read_raw_pressure() -> int`
Возвращает сырое (некомпенсированное) значение АЦП давления. Диапазон вывода **[0, 1048575]**.

```python
press = climate.read_raw_pressure()
print(press)
```
