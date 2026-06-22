---
title: Қашықтық сенсоры
---
# Қашықтық сенсоры
Қашықтық сенсоры — бұл нысанға дейінгі қашықтықты жоғары дәлдікпен өлшейтін белсенді сенсор. Сенсор инфрақызыл лазерді пайдаланады және лазердің қайтып оралу уақытын жазып алады.

---
## Негізгі қолдану

---
### `DistanceSensor(slot)`
DistanceSensor объектісін жасау үшін `DistanceSensor(slot)` шақырыңыз.

Сондай-ақ `Distance(slot)` қысқа атауын пайдалануға болады.

Кез келген басқа слотты таңдауға болады (`"C"`-дан басқа, себебі ол I2C байланысын қолдамайды).

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN)

**Қайтарады:**
    *slot* үшін ``VL53L0X`` объектісін қайтарады.
```python
from pibody import DistanceSensor

distance = DistanceSensor("A")
```

---
### `.read() -> int`
Бір реттік қашықтық өлшеуді орындайды.  
Қашықтықты мм-мен қайтарады **[20, 2000]**.  
Қате өлшеу кезінде `20` немесе `8190` қайтарады.

```python
from pibody import Distance   # қысқа атау
distance = Distance('A')

data = distance.read()

print(data)
```

---
### `.is_valid(distance) -> bool`
`distance` параметрі міндетті және нақты қашықтықты мм-мен қамтуы керек.

Егер өлшеулер `.min_valid_mm` және `.max_valid_mm` аралығында болса, **True** немесе **False** қайтарады.  
`.min_valid_mm` әдепкі бойынша **30**.  
`.max_valid_mm` әдепкі бойынша **2000**.  
Бұл айнымалыларды өзгертуге болады.

```python
from pibody import Distance   # қысқа атау
distance = Distance('A')

distance.min_valid_mm = 50
distance.max_valid_mm = 200

curr_dist = distance.read()

valid = distance.is_valid(curr_dist)
print(valid)
```

---
## Басқа функциялар

---
### `.bar() -> string`
Ағымдағы қашықтықтың мәтіндік прогресс жолағын қайтарады.

**Аргументтер:**

- `max_range (int | None)` — толық жолаққа сәйкес келетін қашықтық (мм). Әдепкі: **200** мм
- `width (int | None)` — жолақ ені таңбалармен. Әдепкі: **20** таңба
- `fill_char (string | None)` — толтырылған бөлік үшін пайдаланылатын таңба. Әдепкі: **"#"**
- `empty_char (string | None)` — бос бөлік үшін пайдаланылатын таңба. Әдепкі: **" "**

```python
from pibody import Distance   # қысқа атау
distance = Distance('A')

bar = distance.bar()

print(bar) # [######  ] 75 mm
```

---
### `.add_close_trigger(threshold_mm, callback)`
Нысан *threshold_mm*-ден жақын болғанда шақырылатын callback тіркейді.

**Аргументтер:**

- `threshold_mm (int)` — қашықтық шегі мм-мен
- `callback` — ағымдағы қашықтықпен (мм) шақырылады

```python
distance.add_close_trigger(100, cb)
```

---
### `.add_motion_trigger(change_threshold_mm, callback, cooldown_ms)`
Тізбектей check() шақырулары арасында қашықтық *change_threshold_mm*-ден көп өзгергенде шақырылатын callback тіркейді.

**Аргументтер:**

- `change_threshold_mm (int)` — іске қосу үшін ең аз өзгеріс (мм)
- `callback` — (distance_mm, delta_mm) арқылы шақырылады
- `cooldown_ms` — тізбектей іске қосулар арасындағы ең аз уақыт мс. Әдепкі: **500**

```python
distance.add_motion_trigger(100, cb)
```

---
### `.check()`
Қашықтықты оқиды және барлық тіркелген callback'терді іске қосады.

Негізгі циклден мерзімді түрде шақырылуы керек.
Жарамсыз көрсеткіштер үнсіз еленбейді.

```python
distance.add_motion_trigger(100, cb)

while True:
    distance.check()				  
```
