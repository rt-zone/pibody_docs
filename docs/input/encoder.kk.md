---
title: Энкодер
---
# Энкодер
Энкодер — бұл айналмалы қозғалысты цифрлық сигналға түрлендіретін құрылғы. Ол әртүрлі қолданбаларда кеңінен қолданылады — ас үй техникасы мен дыбыс деңгейін реттегіштерден бастап автомобильдер мен 3D принтерлерге дейін.

---
## Негізгі қолдану

---
### `Encoder(slot)`
Encoder объектісін жасау үшін `Encoder(slot)` шақырыңыз.

**Аргументтер:**

- `slot (string | int | tuple)` — слот белгісі ("A", "B", "C", "D", "E", "F", "G", "H"), пин порты (0, 2 және т.б.), кортеж (0, Pin.IN)

**Қайтарады:**
    *slot* үшін ``RotaryEncoder`` объектісін қайтарады.
```python
from pibody import Encoder

encoder = Encoder("A")
```

---
### `.read() -> int`
Энкодердың ағымдағы орнын қайтарады.

```python
data = encoder.read()
print(data)
```

---
### `.value() -> int`
`.read()` сияқты, энкодердің ағымдағы орнын қайтарады.

```python
value = encoder.value()
print(value)
```

---
### `.bound(min_val, max_val)`
Энкодер мәндерін **min_val** бастап **max_val** дейінгі диапазонмен шектейді.

**Аргументтер:**

- `min_val (int | float)` — энкодердің ең төменгі мәні. Әдепкі: **0**
- `max_val (int | float)` — энкодердің ең жоғарғы мәні. Әдепкі: **10**

```python
encoder.bound(1, 10)
```

---
### `.wrap(min_val, max_val)`
Энкодер мәндерін **min_val** бастап **max_val** дейінгі диапазонда айналдырады.

**Аргументтер:**

- `min_val (int | float)` — энкодердің ең төменгі мәні. Әдепкі: **0**
- `max_val (int | float)` — энкодердің ең жоғарғы мәні. Әдепкі: **10**

```python
encoder.wrap(1, 10)
```

---
### `.free()`
Bound және wrap режимдерін қалпына келтіріп, энкодерді шектеусіз режимге қайтарады.

```python
encoder.free()
```

---
## Басқа функциялар

---
### `.old_value() -> int`
Соңғы өзгеріске дейінгі энкодердің алдыңғы орнын қайтарады.

```python
data = encoder.old_value()
print(data)
```

---
### `.set_value(val)`
Энкодер мәнін орнатады.

**Аргументтер:**

- `val (int | float)` — энкодер мәні. Әдепкі: **0**

```python
encoder.set_value(0)
```

---
### `.reset()`
Энкодер мәнін **0**-ге қалпына келтіреді.

```python
encoder.reset()
```

---
### `.direction() -> int`
Айналу бағытын қайтарады:

- **1** — сағат тілімен
- **-1** — сағат тіліне қарсы
- **0** — қозғалыс жоқ

```python
direction = encoder.direction()
print(direction)
```

---
### `.toggle_direction()`
Айналу бағытын кері ауыстырады.

```python
encoder.toggle_direction()
```

---
### `.set_incr(incr)`
Энкодердің қадам мәнін өзгертеді.

**Аргументтер:**

- `incr (int | float)` — энкодердің өсу/кему қадамы. Әдепкі: **1**

```python
encoder.set_incr(0.1)
```

---
## API анықтамалығы

---
### `.set(value, min_val, incr, max_val, reverse, range_mode)`
Энкодер конфигурациясын орнатады. Берілмеген кез келген параметр өзгеріссіз қалады.

**Аргументтер:**

- `value (int | float)` — энкодердің ағымдағы мәні. Әдепкі: **0**
- `min_val (int | float)` — энкодердің ең төменгі мәні. Әдепкі: **0**
- `max_val (int | float)` — энкодердің ең жоғарғы мәні. Әдепкі: **10**
- `incr (int | float)` — энкодердің өсу/кему қадамы. Әдепкі: **1**
- `reverse (bool)` — **True** болса, айналу бағыты кері ауыстырылады. Әдепкі: **False**
- `range_mode` — мәндерді өңдеу режимін орнататын опционалды бүтін сан:

    - `RANGE_UNBOUNDED` (1) — мән шектеусіз өсе/кеми алады
    - `RANGE_WRAP` (2) — мән **min_val** және **max_val** арасында айналады
    - `RANGE_BOUNDED` (3) — мән **min_val** және **max_val** деңгейінде тоқтайды

    Әдепкі бойынша `range_mode` = `RANGE_UNBOUNDED`.

```python
encoder.set(value=0.5, min_val=0.1, incr=0.1, max_val=0.9, reverse=False, range_mode=3)
```

---
### `.close()`
Энкодер үзілімдерін өшіріп, мәндерді жаңартуды тоқтатады.

```python
encoder.close()
```

---
### `.bar(width, fill_char, empty_char) -> string`
**min_val** және **max_val** арасындағы ағымдағы мәннің орнын көрсететін мәтіндік прогресс жолағын қайтарады.

**Аргументтер:**

- `width (int)` — жол өлшемі. Әдепкі: **20**
- `fill_char (char)` — толтырылған бөлікке арналған таңба
- `empty_char (char)` — толтырылмаған бөлікке арналған таңба

```python
bar = encoder.bar()
print(bar)
```

---
### `.live_bar(width, fill_char, empty_char)`
Консольге нақты уақытта жаңартылатын прогресс жолағын шығарады.

**Аргументтер:**

- `width (int)` — жол өлшемі. Әдепкі: **20**
- `fill_char (char)` — толтырылған бөлікке арналған таңба
- `empty_char (char)` — толтырылмаған бөлікке арналған таңба

```python
encoder.live_bar()
```

---
### `.add_listener(callback)`
Функцияны аргумент ретінде қосады. Бұл функция энкодер бұрылғанда шақырылады.

```python
encoder.add_listener(cb)
```

---
### `.remove_listener(callback)`
Бұрын қосылған callback функциясын жояды. Callback табылмаса `ValueError` қатесін шығарады.

```python
encoder.remove_listener(cb)
```
