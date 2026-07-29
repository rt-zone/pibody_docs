---
title: Дисплей
---
# Display
Singleton — әрқашан бірдей дананы қайтарады.

---
## Негізгі қолдану

---
### `display`
Экран объектісі импорт кезінде жасалады. Оны импорттап, тікелей қолданыңыз — бұл класс **емес**,
сондықтан `display()` немесе `Display()` деп ешқашан жазбаңыз.

```python
from pibody import display

display.print("Hello")
```

---
### `.print(*args)`
*args* мәнін айналмалы экран консоліне шығарады.

Аргументтер бос орынмен біріктіріледі және ``">> "`` префиксімен қосылады.
Ұзын жолдар дисплей еніне сыйдыру үшін оралады.
``\\n`` таңбалары анық жол үзілімдерін тудырады.

**Аргументтер:**

- `*args (Any)` —
- `font (Any)` — мәтіндік қаріп модулі: **font_small**, **font_medium**, **font_large** немесе **font_bold**. Әдепкі: **display.font_medium**
- `color (Display.Color)` — мәтін түсі. Әдепкі: **display.WHITE**

```python
display.print("Сәлем,", "Әлем!")  # >> Сәлем, Әлем!
```

---
### `.text(text, x, y)`
*text* мәтінін (x, y) позициясында *font* қаріпімен жазады.

**Аргументтер:**

- `text (str | int | bytes)` — шығарылатын параметр
- `x (int)` — мәтін бағанының позициясы
- `y (int)` — мәтін жолының позициясы
- `font (Any)` — қаріп модулі: **font_small**, **font_medium**, **font_large** немесе **font_bold**. Әдепкі: **display.font_small**
- `fg (Display.Color)` — мәтін түсі. Әдепкі: **display.WHITE**
- `bg (Display.Color)` — мәтін фонының түсі. Әдепкі: **display.BLACK**

```python
display.text("PiBody", 50, 50, font = font_bold)  # PiBody
```

---
### `.clear()`
Дисплейді тазалап, айналмалы консоль күйін қалпына келтіреді.

```python
display.clear()
```

---
## Геометриялық фигуралар

---
### `.fill(color)`
Бүкіл дисплейді *color* түсімен толтырады.

**Аргументтер:**

- `color (Display.Color)` — алдын ала орнатылған түсті енгізіңіз немесе өзіңіздікін көрсетіңіз.

```python
display.fill(display.WHITE)
```

---
### `.pixel(x, y, color)`
(x, y) нүктесінде бір пикселді *color* түсіне орнатады.

**Аргументтер:**

- `x (int)` — пиксел бағаны (0 = сол жақ шет)
- `y (int)` — пиксел жолы (0 = жоғарғы шет)
- `color (Display.Color)` — пиксел түсі

```python
display.pixel(10, 10, display.WHITE)
```

---
### `.line(x0, y0, x1, y1, color)`
(x0, y0) бастап (x1, y1) дейін *color* түсімен сызық жүргізеді.

**Аргументтер:**

- `x0 (int)` — бастапқы баған
- `y0 (int)` — бастапқы жол
- `x1 (int)` — соңғы баған
- `y1 (int)` — соңғы жол
- `color (Display.Color)` — сызық түсі

```python
display.line(10, 10, 20, 20, display.BLUE)
```

---
### `.hline(x, y, length, color)`
(x, y) бастап ұзындығы *length* пиксел болатын жылдам көлденең сызық жүргізеді.

**Аргументтер:**

- `x (int)` — бастапқы баған
- `y (int)` — жол позициясы
- `length (int)` — сызық ұзындығы пикселмен
- `color (Display.Color)` — сызық түсі

```python
display.hline(10, 10, 15, display.BLACK)
```

---
### `.vline(x, y, length, color)`
(x, y) бастап ұзындығы *length* пиксел болатын жылдам тік сызық жүргізеді.

**Аргументтер:**

- `x (int)` — баған позициясы
- `y (int)` — бастапқы жол
- `length (int)` — сызық ұзындығы пикселмен
- `color (Display.Color)` — сызық түсі

```python
display.vline(10, 10, 15, display.BLACK)
```

---
### `.crosshair(x, y, r, x_center, y_center, crosshair_radius)`
Ортасында добы бар көздеуіш крестін көрсетеді.  
x, y координаттары салыстырмалы және -1 мен 1 аралығында, мұнда 0 — көздеуіштің ортасы.

**Аргументтер:**

- `x (float)` — салыстырмалы X позициясы **(-1 = солға, 0 = орта, 1 = оңға)**
- `y (float)` — салыстырмалы Y позициясы **(-1 = төмен, 0 = орта, 1 = жоғары)**
- `r (int)` — радиус
- `x_center (int)` — сол-орта тірек нүктесінің X
- `y_center (int)` — сол-орта тірек нүктесінің Y
- `crosshair_radius (int)` — ішкі радиус пикселмен
- `color (Display.Color | None)` — көздеуіштің негізгі түсі. Әдепкі: **display.RED**
- `border_color (Display.Color | None)` — жиек түсі. Әдепкі: **display.WHITE**
- `background_color (Display.Color | None)` — фон түсі. Әдепкі: **display.BLACK**

```python
display.crosshair(50, 50, 20, 0, 0, 5, background_color = display.GREEN)
```

---
### `.rect(x, y, width, height, color)`
Жоғарғы сол жақ бұрышы (x, y) болатын тіктөртбұрыштың контурын жүргізеді.

**Аргументтер:**

- `x (int)` — жоғарғы сол жақ баған
- `y (int)` — жоғарғы сол жақ жол
- `width (int)` — тіктөртбұрыш ені
- `height (int)` — тіктөртбұрыш биіктігі
- `color (Display.Color)` — тіктөртбұрыш жиегінің түсі

```python
display.rect(50, 50, 10, 20, display.GREEN)
```

---
### `.fill_rect(x, y, width, height, color)`
Жоғарғы сол жақ бұрышы (x, y) болатын толтырылған тіктөртбұрыш жүргізеді.

**Аргументтер:**

- `x (int)` — жоғарғы сол жақ баған
- `y (int)` — жоғарғы сол жақ жол
- `width (int)` — тіктөртбұрыш ені
- `height (int)` — тіктөртбұрыш биіктігі
- `color (Display.Color)` — толтыру түсі

```python
display.fill_rect(50, 50, 10, 20, display.GREEN)
```

---
### `.circle(x, y, r, color)`
Центрі (x, y) және радиусы *r* болатын шеңбер контурын жүргізеді.

**Аргументтер:**

- `x (int)` — центр бағаны
- `y (int)` — центр жолы
- `r (int)` — шеңбер радиусы
- `color (Display.Color)` — шеңбер жиегінің түсі

```python
display.circle(50, 50, 10, display.GREEN)
```

---
### `.fill_circle(x, y, r, color)`
Центрі (x, y) және радиусы *r* болатын толтырылған шеңбер жүргізеді.

**Аргументтер:**

- `x (int)` — центр бағаны
- `y (int)` — центр жолы
- `r (int)` — шеңбер радиусы
- `color (Display.Color)` — толтыру түсі

```python
display.fill_circle(50, 50, 10, display.GREEN)
```

---
### `.arc(color, center_x, center_y, r)`
Доға жүргізеді (шеңбердің қалың контур сегменті).

**Аргументтер:**

- `color (Display.Color)` — доғаның негізгі түсі
- `center_x (int)` — центрдің X
- `center_y (int)` — центрдің Y
- `r (int)` — ішкі радиус пикселмен
- `width (int | None)` — радиалды қалыңдық пикселмен. Әдепкі: **1**
- `start_angle (int | None)` — доғаның басталуы градуспен. Әдепкі: **0**
- `end_angle (int | None)` — доғаның аяқталуы градуспен. Әдепкі: **360**

```python
display.arc(display.WHITE, 50, 50, 20)
```

---
## Көпбұрыштарды салу

---
### `.draw_polygon(center_x, center_y, r, n)`
Ретті *n*-бұрышты опционалды шеткі дөңестікпен жүргізеді.

**Аргументтер:**

- `center_x (int)` — сол-орта тірек нүктесінің X
- `center_y (int)` — сол-орта тірек нүктесінің Y
- `r (int)` — сыртқы шеңбер радиусы пикселмен
- `n (int)` — қабырғалар саны
- `bump (float | None)` — r-ге қатысты жиектің дөңестік коэффициенті (1.0 = жазық). Әдепкі: **1.0**
- `angle_offset (float | None)` — градустағы бұрылу ығысуы; None болса автоматты түрде есептеледі. Әдепкі: **None**
- `color (Display.Color | None)` — контур/толтыру түсі. Әдепкі: **display.WHITE**
- `fill (bool | None)` — **True** болса толтырылған көпбұрыш, **False** болса тек контур. Әдепкі: **False**

```python
display.draw_polygon(50, 50, 20, 4, color = display.GREEN)
```

---
### `.polygon_center(polygon) -> (int, int)`
Тұйық дөңес *polygon* центрін ``(x, y)`` қайтарады.

**Аргументтер:**

- `polygon (list[tuple[int, int]])` — координаттар тізімі. [(0, 0), (10, 0), (10, 10), (0, 10)]

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

center_x, center_y = display.polygon_center(poly)

print(center_x, center_y)
```

---
### `.polygon(polygon, x, y, color)`
(x, y) нүктесіне жылжытылған көпбұрыш контурын жүргізеді, опционалды түрде (center_x, center_y) айналасында *angle* радианға бұрылады.

**Аргументтер:**

- `polygon (list[tuple[int, int]])` — координаттар тізімі. [(0, 0), (10, 0), (10, 10), (0, 10)]
- `x (int)` — жылжыту ығысуы баған
- `y (int)` — жылжыту ығысуы жол
- `color (Display.Color)` — көпбұрыштың негізгі түсі
- `angle (float)` — бұрылу бұрышы. Әдепкі: **0.0**
- `center_x (int)` — бұрылу центрінің бағаны. Әдепкі: **0**
- `center_y (int)` — бұрылу центрінің жолы. Әдепкі: **0**

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

display.polygon(poly, 0, 0, display.RED, angle = 45)
```

---
### `.fill_polygon(polygon, x, y, color)`
(x, y) нүктесіне жылжытылған толтырылған көпбұрышты жүргізеді, опционалды түрде (center_x, center_y) айналасында *angle* радианға бұрылады.

**Аргументтер:**

- `polygon (list[tuple[int, int]])` — координаттар тізімі. [(0, 0), (10, 0), (10, 10), (0, 10)]
- `x (int)` — жылжыту ығысуы баған
- `y (int)` — жылжыту ығысуы жол
- `color (Display.Color)` — көпбұрыштың негізгі түсі
- `angle (float)` — бұрылу бұрышы. Әдепкі: **0.0**
- `center_x (int)` — бұрылу центрінің бағаны. Әдепкі: **0**
- `center_y (int)` — бұрылу центрінің жолы. Әдепкі: **0**

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

display.fill_polygon(poly, 0, 0, display.RED, angle = 45)
```

---
### `.bounding() -> (int, int, int, int)`
Dirty-тіктөртбұрышты бақылауды қосу/өшіру және нәтижелерді сұрау.

True немесе False беру бақыланатын тіктөртбұрышты қалпына келтіреді және сәйкесінше бақылауды қосады/өшіреді.

**(min_x, min_y, max_x, max_y)** немесе, егер *as_rect* True болса, **(min_x, min_y, width, height)** қайтарады.

**Аргументтер:**

- `status (bool | None)` — Әдепкі: **None**
- `as_rect (bool | None)` — Әдепкі: **False**

```python
data = display.bounding()
print(data)
```

---
## Bitmap

---
### `.blit_buffer(buffer, x, y, width, height)`
Шикі RGB565 буферін дисплейге (x, y) позициясында көшіреді.

*buffer* **width * height * 2** байттан тұруы керек.

**Аргументтер:**

- `buffer (bytes | bytearray)` — буфер
- `x (int)` — жоғарғы сол жақ баған
- `y (int)` — жоғарғы сол жақ жол
- `width (int)` — тіктөртбұрыш ені
- `height (int)` — тіктөртбұрыш биіктігі

```python
display.blit_buffer(buf, 50, 50, 60, 60)
```

---
### `.bitmap(bitmap, x, y)`
(x, y) позициясында bitmap модулін көрсетеді (imgtobitmap.py немесе monofont2bitmap.py көмегімен жасалған). Multi-bitmap модульдерінен таңдау үшін *index* пайдаланыңыз.

**Аргументтер:**

- `bitmap (Any)` — bitmap
- `x (int)` — жоғарғы сол жақ баған
- `y (int)` — жоғарғы сол жақ жол
- `index (int | None)` — multi-bitmap индексі. Әдепкі: **0**

```python
display.bitmap(bitmap, 0, 0)
```

---
## Суреттер

---
### `.jpg(jpg, x, y)`
(x, y) позициясында JPEG көрсетеді.

**Аргументтер:**

- `jpg (str | bytes | bytearray)` — файл атауының жолы немесе JPEG деректері бар буфер болуы мүмкін
- `x (int)` — жоғарғы сол жақ баған
- `y (int)` — жоғарғы сол жақ жол
- `method (int)` — рендеринг әдісі. Бос RAM-нан асатын суреттер үшін **display.SLOW** пайдаланыңыз. Әдепкі: **display.FAST**

```python
display.jpg("dog.jpg", 0, 0)
```

---
### `.jpg_decode(jpg) -> (bytearray, int, int)`
JPEG декодтап, **(buffer, width, height)** қайтарады.

**Аргументтер:**

- `jpg (str | bytes | bytearray)` — blit_buffer үшін қолайлы RGB565 bytearray
- `x (int | None)` — кадрлаудың бастапқы бағаны. Әдепкі: **0**
- `y (int | None)` — кадрлаудың бастапқы жолы. Әдепкі: **0**
- `width (int | None)` — декодталған суретті кадрлау ені. Әдепкі: **None**
- `height (int | None)` — декодталған суретті кадрлау биіктігі. Әдепкі: **None**

```python
display.jpg_decode("dog.jpg")
```

---
### `.png(png, x, y)`
(x, y) позициясында PNG файлын көрсетеді. Мөлдірлік қолданылмайды, егер *mask* True болмаса; бұл жағдайда нөлдік альфасы бар пикселдер өткізіледі (баяулау, жол-жолмен сызылады).

**Аргументтер:**

- `png (str | bytes | bytearray)` — blit_buffer үшін қолайлы RGB565 bytearray
- `x (int)` — жоғарғы сол жақ баған
- `y (int)` — жоғарғы сол жақ жол
- `mask (bool = False)` — мөлдірлік режимі

```python
display.png("dog.jpg", 0, 0, mask = True)
```

---
## Мәтін

---
### `.write(font, s, x, y) -> int`
(x, y) позициясында пропорционалды bitmap *font* қаріпімен UTF-8 *s* мәтінін жазады. *Пропорционалды / TrueType bitmap қаріптері*.

Көрсетілген жолдың енін пикселмен қайтарады.

**Аргументтер:**

- `font (Any)` — bitmap қаріп модулі: **font_small**, **font_medium**, **font_large** немесе **font_bold**. Әдепкі: **display.font_medium**
- `s (str)` — көрсетілетін мәтін
- `x (int)` — мәтін бағанының позициясы
- `y (int)` — мәтін жолының позициясы

```python
display.write(display.font_medium, "Сәлем", 10, 10)
```

---
### `.write_len(font, s) -> int`
*s* мәтінінің *font* қаріпімен көрсетілгендегі пикселдік ұзындығын қайтарады. *Пропорционалды / TrueType bitmap қаріптері*.

**Аргументтер:**

- `font (Any)` — bitmap қаріп модулі: **font_small**, **font_medium**, **font_large** немесе **font_bold**. Әдепкі: **display.font_medium**
- `s (str)` — көрсетілетін мәтін

```python
length = display.write_len(display.font_medium, "PiBody")
print(length)
```

---
### `.draw(font, s, x, y)`
*s* мәтінін Hershey векторлық *font* қаріпімен жүргізеді, (x, y) мәтіннің *төменгі сол жақ* бұрышы ретінде. *scale* > 0 болуы керек. *Hershey векторлық қаріптері*.

**Аргументтер:**

- `font (Any)` — bitmap қаріп модулі: **font_small**, **font_medium**, **font_large** немесе **font_bold**. Әдепкі: **display.font_medium**
- `s (str)` — көрсетілетін мәтін
- `x (int)` — төменгі сол жақ баған
- `y (int)` — төменгі сол жақ жол
- `fg (Display.Color | None)` — мәтін түсі. Әдепкі: **display.WHITE**
- `scale (float | None)` — масштаб. Әдепкі: **1.0**

```python
display.draw(display.font_medium, "PiBody", 15, 15)
```

---
### `.draw_len(font, s)`
*s* мәтінінің *font* қаріпімен *scale* масштабында жүргізілгендегі пикселдік ұзындығын қайтарады. *Hershey векторлық қаріптері*.

**Аргументтер:**

- `font (Any)` — bitmap қаріп модулі: **font_small**, **font_medium**, **font_large** немесе **font_bold**. Әдепкі: **display.font_medium**
- `s (str)` — көрсетілетін мәтін
- `scale (float | None)` — масштаб. Әдепкі: **1.0**

```python
length = display.draw_len(display.font_medium, "PiBody", 15, 15)
print(length)
```

---
## Прогресс жолағы

---
### `.linear_bar(x, y, value, min_value, max_value)`
*y* бойынша тігінен центрленген көлденең прогресс жолағын жүргізеді.

**Аргументтер:**

- `x (int)` — сол-орта тірек нүктесінің X
- `y (int)` — сол-орта тірек нүктесінің Y
- `value (float)` — ағымдағы мән (min_value–max_value шегінде)
- `min_value (float)` — бос жолаққа сәйкес келетін мән
- `max_value (float)` — толық жолаққа сәйкес келетін мән
- `length (int | None)` — жолақтың жалпы ұзындығы пикселмен. Әдепкі: **100**
- `height (int | None)` — жолақ биіктігі пикселмен. Әдепкі: **5**
- `border (bool | None)` — **True** болса, тіктөртбұрышты жиек жүргізіп, бос аймақты толтырады; **False** болса, шеткі қақпақтар мен центр сызығын жүргізеді. Әдепкі: **False**
- `bar_color (Display.Color | None)` — толтырылған бөліктің түсі. Әдепкі: **display.GREEN**
- `border_color (Display.Color | None)` — жиек/шеткі қақпақтар/центр сызығының түсі. Әдепкі: **display.WHITE**
- `background_color (Display.Color | None)` — толтырылмаған бөліктің түсі. Әдепкі: **display.BLACK**

```python
display.linear_bar(50, 50, 5, 0, 10)
```

---
### `.circular_bar(center_x, center_y, r, value, min_value, max_value)`
Дөңгелек прогресс жолағын жүргізеді.

Толтырылған доға (-90° бастап есептелген бұрышқа дейін) *color* түсімен, қалғаны *background_color* түсімен жүргізіледі.

**Аргументтер:**

- `center_x (int)` — центрдің X
- `center_y (int)` — центрдің Y
- `r (int)` — ішкі радиус пикселмен
- `value (float)` — ағымдағы мән (min_value–max_value шегінде)
- `min_value (float)` — бос жолаққа сәйкес келетін мән
- `max_value (float)` — толық жолаққа сәйкес келетін мән
- `width (int | None)` — радиалды қалыңдық пикселмен. Әдепкі: **2**
- `color (Display.Color | None)` — толтырылған бөліктің түсі. Әдепкі: **display.GREEN**
- `background_color (Display.Color | None)` — толтырылмаған бөліктің түсі. Әдепкі: **display.WHITE**

```python
display.circular_bar(50, 50, 20, 5, 0, 10)
```

---
## Басқа функциялар

---
### `.sleep_mode(value)`
Ұйқы режиміне кіру (True) немесе шығу (False).  
Ұйқы кезінде дисплей мазмұны сақталмауы мүмкін.

**Аргументтер:**

- `value (bool)` — ұйқы режимі қосу/өшіру

```python
display.sleep_mode(True)
```

---
### `.logo()`
(x, y) позициясында *r* радиусымен Artisan Education өнім логотипін жүргізеді.

Жүргізу алдында экранды ақ түспен толтырады.

**Аргументтер:**

- `x (int | None)` — центр бағаны
- `y (int | None)` — центр жолы
- `r (int | None)` — логотип радиусы

```python
display.logo()
```

---
### `.hsv(h, s, v) -> Display.Color`
HSV мәнін оралған RGB565 түс мәніне түрлендіреді.  
color() әдісіне ұқсас, бірақ реңк, қанықтылық, жарықтықты кіріс ретінде пайдаланады.

**Аргументтер:**

- `h (float)` — реңк **[0, 360]** диапазонында
- `s (float)` — қанықтылық **[0.0, 1.0]** диапазонында
- `v (float)` — жарықтық **[0.0, 1.0]** диапазонында

```python
text_color = display.hsv(200, 0.8, 1.0)

display.print("Сәлем", font = text_color)
```

---
## Конфигурация

---
### `.width() -> int`
Ағымдағы логикалық дисплей енін пикселмен қайтарады.

```python
width = display.width()
print(width)
```

---
### `.height() -> int`
Ағымдағы логикалық дисплей биіктігін пикселмен қайтарады.

```python
height = display.height()
print(height)
```

---
### `.rotation(r)`
Логикалық дисплейді сағат тіліне қарсы бұрады.

- `0` = Портрет **(0°)**
- `1` = Ландшафт **(90°)**
- `2` = Кері портрет **(180°)**
- `3` = Кері ландшафт **(270°)**

**Аргументтер:**

- `r` — **0** бастап **3** дейінгі бұру режимі

```python
display.rotation(2)
```

---
### `.offset(x_start, y_start)`
Баған/жол бастапқы ығысуын қайта анықтайды.

Стандартты емес панель макеті үшін реттеу қажет болса, `rotation()` *кейін* шақырыңыз.

**Аргументтер:**

- `x_start (int)` — бағанның бастапқы ығысуы
- `y_start (int)` — жолдың бастапқы ығысуы

```python
display.offset(10, 10)
```

---
### `.inversion_mode(value)`
Дисплей түстерінің инверсиясын қосу **(True)** немесе өшіру **(False)**.

**Аргументтер:**

- `value (bool)` — инверсия күйі

```python
display.inversion_mode(True)
```

---
### `.madctl(value | None) -> None | int`
MADCTL регистрінің мәнін алу (аргументсіз) немесе орнату (аргументпен).  
Аппараттық деңгейде бұрылуды және түс ретін басқарады.

**Аргументтер:**

- `value (int)` — MADCTL регистрінің мәні

Аргументсіз шақырғанда ағымдағы мәнді қайтарады, әйтпесе мәнді орнатып, None қайтарады.

```python
display.madctl()
```

---
## Қосымша ақпарат

### Display.Color алдын ала орнатылған түстері

`Display.Color` кез келген сурет салу әдісімен пайдалануға болатын бірнеше алдын ала орнатылған түстерді ұсынады.

| Атауы | Сипаттамасы |
|---|---|
| <span style="color: #000000; font-weight: bold;">display.BLACK</span>   | таза қара |
| <span style="color: #0000FF; font-weight: bold;">display.BLUE</span>    | көк |
| <span style="color: #FF0000; font-weight: bold;">display.RED</span>     | қызыл |
| <span style="color: #00FF00; font-weight: bold;">display.GREEN</span>   | жасыл |
| <span style="color: #00FFFF; font-weight: bold;">display.CYAN</span>    | көгілдір |
| <span style="color: #FF00FF; font-weight: bold;">display.MAGENTA</span> | қызғылт |
| <span style="color: #FFFF00; font-weight: bold;">display.YELLOW</span>  | сары |
| <span style="color: #FFFFFF; font-weight: bold;">display.WHITE</span>   | таза ақ |
