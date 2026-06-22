---
title: Климат сенсоры
---
# Климат сенсоры
Климат сенсоры — бұл температураны, атмосфералық қысымды және ылғалдылықты өлшей алатын ақылды құрылғы.

---
## Негізгі қолдану

---
### `ClimateSensor(slot)`
ClimateSensor объектісін жасау үшін `ClimateSensor(slot)` шақырыңыз.

Сондай-ақ `Climate(slot)` қысқа атауын пайдалануға болады.

Кез келген басқа слотты таңдауға болады (`"C"`-дан басқа, себебі ол I2C байланысын қолдамайды).

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN)

**Қайтарады:**
    *slot* үшін ``BME280`` объектісін қайтарады.
```python
from pibody import ClimateSensor

climate = ClimateSensor("A")
```

---
### `.read() -> (float, float, float)`
Келесі кілт-мәндері бар сөздікті қайтарады:

- `temperature` — температура °C **[-40, 85]**
- `humidity` — ылғалдылық %RH **[0, 100]**
- `pressure` — қысым гПа **[0, 20000]**

```python
from pibody import Climate  # қысқа атау
climate = Climate('A')

data = climate.read() 

temp = data['temperature']
hum = data['humidity']
pres = data['pressure']					  

print(f"temp: {temp}, hum: {hum}, pres: {pres}")
```

---
### `.read_temperature() -> float`
Компенсацияланған температураны °C **[-40, 85]** қайтарады.

```python
temp = climate.read_temperature()
print(temp)
```

---
### `.read_humidity() -> float`
Компенсацияланған салыстырмалы ылғалдылықты %RH **[0, 100]** қайтарады.

```python
hum = climate.read_humidity()
print(hum)
```

---
### `.read_pressure() -> float`
Компенсацияланған қысымды гПа **[0, 20000]** қайтарады.

```python
press = climate.read_pressure()
print(press)
```

---
## Басқа функциялар

---
### `.read_raw_temp() -> int`
Шикі (компенсацияланбаған) температура АЦП мәнін қайтарады. Шығыс диапазоны **[0, 1048575]**.

```python
temp = climate.read_raw_temp()
print(temp)
```

---
### `.read_raw_humidity() -> int`
Шикі (компенсацияланбаған) ылғалдылық АЦП мәнін қайтарады. Шығыс диапазоны **[0, 65535]**.

```python
hum = climate.read_raw_humidity()
print(hum)
```

---
### `.read_raw_pressure() -> int`
Шикі (компенсацияланбаған) қысым АЦП мәнін қайтарады. Шығыс диапазоны **[0, 1048575]**.

```python
press = climate.read_raw_pressure()
print(press)
```
