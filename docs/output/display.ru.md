---
title: Дисплей
---
# Display
Одиночка (Singleton) — всегда возвращает один и тот же экземпляр.

---
## Базовое использование

---
### `display`
Объект экрана создаётся при импорте. Импортируйте его и используйте напрямую — это **не** класс,
поэтому никогда не пишите `display()` или `Display()`.

```python
from pibody import display

display.print("Hello")
```

---
### `.print(*args)`
Выводит *args* на прокручиваемую экранную консоль.

Аргументы объединяются пробелами и предваряются ``">> "``.
Длинные строки переносятся по ширине дисплея.
Символы ``\\n`` вызывают принудительный перенос строки.

**Аргументы:**

- `*args (Any)` —
- `font (Any)` — модуль шрифта: **font_small**, **font_medium**, **font_large** или **font_bold**. По умолчанию: **display.font_medium**
- `color (Display.Color)` — цвет текста. По умолчанию: **display.WHITE**

```python
display.print("Привет,", "Мир!")  # >> Привет, Мир!
```

---
### `.text(text, x, y)`
Пишет *text* в позиции (x, y) с использованием *font*.

**Аргументы:**

- `text (str | int | bytes)` — параметр для вывода
- `x (int)` — позиция колонки текста
- `y (int)` — позиция строки текста
- `font (Any)` — модуль шрифта: **font_small**, **font_medium**, **font_large** или **font_bold**. По умолчанию: **display.font_small**
- `fg (Display.Color)` — цвет текста. По умолчанию: **display.WHITE**
- `bg (Display.Color)` — цвет фона текста. По умолчанию: **display.BLACK**

```python
display.text("PiBody", 50, 50, font = font_bold)  # PiBody
```

---
### `.clear()`
Очищает дисплей и сбрасывает состояние прокручиваемой консоли.

```python
display.clear()
```

---
## Геометрические фигуры

---
### `.fill(color)`
Заполняет весь дисплей *color*.

**Аргументы:**

- `color (Display.Color)` — введите предустановленный цвет или укажите свой.

```python
display.fill(display.WHITE)
```

---
### `.pixel(x, y, color)`
Устанавливает один пиксель в (x, y) с цветом *color*.

**Аргументы:**

- `x (int)` — колонка пикселя (0 = левый край)
- `y (int)` — строка пикселя (0 = верхний край)
- `color (Display.Color)` — цвет пикселя

```python
display.pixel(10, 10, display.WHITE)
```

---
### `.line(x0, y0, x1, y1, color)`
Рисует линию от (x0, y0) до (x1, y1) цветом *color*.

**Аргументы:**

- `x0 (int)` — начальная колонка
- `y0 (int)` — начальная строка
- `x1 (int)` — конечная колонка
- `y1 (int)` — конечная строка
- `color (Display.Color)` — цвет линии

```python
display.line(10, 10, 20, 20, display.BLUE)
```

---
### `.hline(x, y, length, color)`
Рисует быструю горизонтальную линию длиной *length* пикселей, начиная с (x, y).

**Аргументы:**

- `x (int)` — начальная колонка
- `y (int)` — позиция строки
- `length (int)` — длина линии в пикселях
- `color (Display.Color)` — цвет линии

```python
display.hline(10, 10, 15, display.BLACK)
```

---
### `.vline(x, y, length, color)`
Рисует быструю вертикальную линию длиной *length* пикселей, начиная с (x, y).

**Аргументы:**

- `x (int)` — позиция колонки
- `y (int)` — начальная строка
- `length (int)` — длина линии в пикселях
- `color (Display.Color)` — цвет линии

```python
display.vline(10, 10, 15, display.BLACK)
```

---
### `.crosshair(x, y, r, x_center, y_center, crosshair_radius)`
Рисует перекрестие с шаром в центре.
Координаты x, y относительные и находятся в диапазоне от -1 до 1, где 0 — середина перекрестия.

**Аргументы:**

- `x (float)` — относительная позиция X **(-1 = влево, 0 = центр, 1 = вправо)**
- `y (float)` — относительная позиция Y **(-1 = вниз, 0 = центр, 1 = вверх)**
- `r (int)` — радиус
- `x_center (int)` — X опорной точки левого центра
- `y_center (int)` — Y опорной точки левого центра
- `crosshair_radius (int)` — внутренний радиус в пикселях
- `color (Display.Color | None)` — основной цвет перекрестия. По умолчанию: **display.RED**
- `border_color (Display.Color | None)` — цвет границы. По умолчанию: **display.WHITE**
- `background_color (Display.Color | None)` — цвет фона. По умолчанию: **display.BLACK**

```python
display.crosshair(50, 50, 20, 0, 0, 5, background_color = display.GREEN)
```

---
### `.rect(x, y, width, height, color)`
Рисует контур прямоугольника с верхним левым углом в (x, y).

**Аргументы:**

- `x (int)` — верхняя левая колонка
- `y (int)` — верхняя левая строка
- `width (int)` — ширина прямоугольника
- `height (int)` — высота прямоугольника
- `color (Display.Color)` — цвет границы прямоугольника

```python
display.rect(50, 50, 10, 20, display.GREEN)
```

---
### `.fill_rect(x, y, width, height, color)`
Рисует заполненный прямоугольник с верхним левым углом в (x, y).

**Аргументы:**

- `x (int)` — верхняя левая колонка
- `y (int)` — верхняя левая строка
- `width (int)` — ширина прямоугольника
- `height (int)` — высота прямоугольника
- `color (Display.Color)` — цвет заливки прямоугольника

```python
display.fill_rect(50, 50, 10, 20, display.GREEN)
```

---
### `.circle(x, y, r, color)`
Рисует контур окружности с центром в (x, y) и радиусом *r*.

**Аргументы:**

- `x (int)` — колонка центра
- `y (int)` — строка центра
- `r (int)` — радиус окружности
- `color (Display.Color)` — цвет границы окружности

```python
display.circle(50, 50, 10, display.GREEN)
```

---
### `.fill_circle(x, y, r, color)`
Рисует заполненную окружность с центром в (x, y) и радиусом *r*.

**Аргументы:**

- `x (int)` — колонка центра
- `y (int)` — строка центра
- `r (int)` — радиус окружности
- `color (Display.Color)` — цвет заливки

```python
display.fill_circle(50, 50, 10, display.GREEN)
```

---
### `.arc(color, center_x, center_y, r)`
Рисует дугу (толстый сегмент контура окружности).

**Аргументы:**

- `color (Display.Color)` — основной цвет дуги
- `center_x (int)` — X центра
- `center_y (int)` — Y центра
- `r (int)` — внутренний радиус в пикселях
- `width (int | None)` — радиальная толщина в пикселях. По умолчанию: **1**
- `start_angle (int | None)` — начало дуги в градусах. По умолчанию: **0**
- `end_angle (int | None)` — конец дуги в градусах. По умолчанию: **360**

```python
display.arc(display.WHITE, 50, 50, 20)
```

---
## Рисование полигонов

---
### `.draw_polygon(center_x, center_y, r, n)`
Рисует правильный *n*-угольник с опциональным выпуклым искажением по краям.

**Аргументы:**

- `center_x (int)` — X опорной точки левого центра
- `center_y (int)` — Y опорной точки левого центра
- `r (int)` — радиус описанной окружности в пикселях
- `n (int)` — количество сторон
- `bump (float | None)` — коэффициент выпуклости края относительно r (1.0 = плоский). По умолчанию: **1.0**
- `angle_offset (float | None)` — смещение поворота в градусах; вычисляется автоматически, если None. По умолчанию: **None**
- `color (Display.Color | None)` — цвет контура / заливки. По умолчанию: **display.WHITE**
- `fill (bool | None)` — залитый полигон, если **True**, только контур, если **False**. По умолчанию: **False**

```python
display.draw_polygon(50, 50, 20, 4, color = display.GREEN)
```

---
### `.polygon_center(polygon) -> (int, int)`
Возвращает центроид ``(x, y)`` замкнутого выпуклого *polygon*.

**Аргументы:**

- `polygon (list[tuple[int, int]])` — список координат. [(0, 0), (10, 0), (10, 10), (0, 10)]

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

center_x, center_y = display.polygon_center(poly)

print(center_x, center_y)
```

---
### `.polygon(polygon, x, y, color)`
Рисует контур полигона, смещённый в (x, y), с опциональным поворотом на *angle* радиан вокруг (center_x, center_y).

**Аргументы:**

- `polygon (list[tuple[int, int]])` — список координат. [(0, 0), (10, 0), (10, 10), (0, 10)]
- `x (int)` — смещение по колонке
- `y (int)` — смещение по строке
- `color (Display.Color)` — основной цвет полигона
- `angle (float)` — угол поворота. По умолчанию: **0.0**
- `center_x (int)` — колонка центра поворота. По умолчанию: **0**
- `center_y (int)` — строка центра поворота. По умолчанию: **0**

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

display.polygon(poly, 0, 0, display.RED, angle = 45)
```

---
### `.fill_polygon(polygon, x, y, color)`
Рисует залитый полигон, смещённый в (x, y), с опциональным поворотом на *angle* радиан вокруг (center_x, center_y).

**Аргументы:**

- `polygon (list[tuple[int, int]])` — список координат. [(0, 0), (10, 0), (10, 10), (0, 10)]
- `x (int)` — смещение по колонке
- `y (int)` — смещение по строке
- `color (Display.Color)` — основной цвет полигона
- `angle (float)` — угол поворота. По умолчанию: **0.0**
- `center_x (int)` — колонка центра поворота. По умолчанию: **0**
- `center_y (int)` — строка центра поворота. По умолчанию: **0**

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

display.fill_polygon(poly, 0, 0, display.RED, angle = 45)
```

---
### `.bounding() -> (int, int, int, int)`
Включает / отключает отслеживание dirty-прямоугольника и запрашивает результаты.

Передача True или False сбрасывает отслеживаемый прямоугольник и соответственно включает / отключает отслеживание.

Возвращает **(min_x, min_y, max_x, max_y)** или, если *as_rect* равно True, **(min_x, min_y, width, height)**.

**Аргументы:**

- `status (bool | None)` — По умолчанию: **None**
- `as_rect (bool | None)` — По умолчанию: **False**

```python
data = display.bounding()
print(data)
```

---
## Bitmap

---
### `.blit_buffer(buffer, x, y, width, height)`
Копирует сырой RGB565 буфер на дисплей в позицию (x, y).

*buffer* должен содержать **width * height * 2** байт.

**Аргументы:**

- `buffer (bytes | bytearray)` — буфер
- `x (int)` — верхняя левая колонка
- `y (int)` — верхняя левая строка
- `width (int)` — ширина прямоугольника
- `height (int)` — высота прямоугольника

```python
display.blit_buffer(buf, 50, 50, 60, 60)
```

---
### `.bitmap(bitmap, x, y)`
Рисует bitmap-модуль (созданный imgtobitmap.py или monofont2bitmap.py) в позиции (x, y). Используйте *index* для выбора из multi-bitmap модулей.

**Аргументы:**

- `bitmap (Any)` — bitmap
- `x (int)` — верхняя левая колонка
- `y (int)` — верхняя левая строка
- `index (int | None)` — индекс multi-bitmap. По умолчанию: **0**

```python
display.bitmap(bitmap, 0, 0)
```

---
## Изображения

---
### `.jpg(jpg, x, y)`
Рисует JPEG в позиции (x, y).

**Аргументы:**

- `jpg (str | bytes | bytearray)` — может быть строкой имени файла или буфером, содержащим данные JPEG
- `x (int)` — верхняя левая колонка
- `y (int)` — верхняя левая строка
- `method (int)` — метод рендеринга. Используйте **display.SLOW** для изображений, превышающих доступную свободную RAM. По умолчанию: **display.FAST**

```python
display.jpg("dog.jpg", 0, 0)
```

---
### `.jpg_decode(jpg) -> (bytearray, int, int)`
Декодирует JPEG и возвращает **(buffer, width, height)**.

**Аргументы:**

- `jpg (str | bytes | bytearray)` — bytearray RGB565, подходящий для **blit_buffer**
- `x (int | None)` — начальная колонка кадрирования. По умолчанию: **0**
- `y (int | None)` — начальная строка кадрирования. По умолчанию: **0**
- `width (int | None)` — ширина кадрирования декодированного изображения. По умолчанию: **None**
- `height (int | None)` — высота кадрирования декодированного изображения. По умолчанию: **None**

```python
display.jpg_decode("dog.jpg")
```

---
### `.png(png, x, y)`
Рисует PNG файл в позиции (x, y). Прозрачность не поддерживается, если только *mask* не равен True; в этом случае пиксели с нулевой альфой пропускаются (медленнее, рисуется построчно).

**Аргументы:**

- `png (str | bytes | bytearray)` — bytearray RGB565, подходящий для **blit_buffer**
- `x (int)` — верхняя левая колонка
- `y (int)` — верхняя левая строка
- `mask (bool = False)` — режим прозрачности

```python
display.png("dog.jpg", 0, 0, mask = True)
```

---
## Текст

---
### `.write(font, s, x, y) -> int`
Пишет UTF-8 *s*, используя пропорциональный bitmap *font* в позиции (x, y). *Пропорциональные / TrueType bitmap шрифты*.

Возвращает `width` отрисованной строки в пикселях.

**Аргументы:**

- `font (Any)` — модуль bitmap шрифта: **font_small**, **font_medium**, **font_large** или **font_bold**. По умолчанию: **display.font_medium**
- `s (str)` — отображаемый текст
- `x (int)` — позиция колонки текста
- `y (int)` — позиция строки текста

```python
display.write(display.font_medium, "Привет", 10, 10)
```

---
### `.write_len(font, s) -> int`
Возвращает длину *s* в пикселях при отрисовке шрифтом *font*. *Пропорциональные / TrueType bitmap шрифты*.

**Аргументы:**

- `font (Any)` — модуль bitmap шрифта: **font_small**, **font_medium**, **font_large** или **font_bold**. По умолчанию: **display.font_medium**
- `s (str)` — отображаемый текст

```python
length = display.write_len(display.font_medium, "PiBody")
print(length)
```

---
### `.draw(font, s, x, y)`
Рисует *s* с использованием векторного шрифта Hershey *font*, где (x, y) — *нижний левый* угол текста. *scale* должен быть > 0. *Векторные шрифты Hershey*.

**Аргументы:**

- `font (Any)` — модуль bitmap шрифта: **font_small**, **font_medium**, **font_large** или **font_bold**. По умолчанию: **display.font_medium**
- `s (str)` — отображаемый текст
- `x (int)` — нижняя левая колонка
- `y (int)` — нижняя левая строка
- `fg (Display.Color | None)` — цвет текста. По умолчанию: **display.WHITE**
- `scale (float | None)` — масштаб. По умолчанию: **1.0**

```python
display.draw(display.font_medium, "PiBody", 15, 15)
```

---
### `.draw_len(font, s)`
Возвращает длину *s* в пикселях при рисовании шрифтом *font* с масштабом *scale*. *Векторные шрифты Hershey*.

**Аргументы:**

- `font (Any)` — модуль bitmap шрифта: **font_small**, **font_medium**, **font_large** или **font_bold**. По умолчанию: **display.font_medium**
- `s (str)` — отображаемый текст
- `scale (float | None)` — масштаб. По умолчанию: **1.0**

```python
length = display.draw_len(display.font_medium, "PiBody", 15, 15)
print(length)
```

---
## Индикатор выполнения

---
### `.linear_bar(x, y, value, min_value, max_value)`
Рисует горизонтальный индикатор выполнения, центрированный по вертикали на *y*.

**Аргументы:**

- `x (int)` — X опорной точки левого центра
- `y (int)` — Y опорной точки левого центра
- `value (float)` — текущее значение (ограничено min_value–max_value)
- `min_value (float)` — значение, соответствующее пустому индикатору
- `max_value (float)` — значение, соответствующее полному индикатору
- `length (int | None)` — общая длина индикатора в пикселях. По умолчанию: **100**
- `height (int | None)` — высота индикатора в пикселях. По умолчанию: **5**
- `border (bool | None)` — если `True`, рисует прямоугольную границу и заливает пустую область; если **False**, рисует конечные колпачки и центральную линию. По умолчанию: **False**
- `bar_color (Display.Color | None)` — цвет заполненной части. По умолчанию: **display.GREEN**
- `border_color (Display.Color | None)` — цвет границы / колпачков / центральной линии. По умолчанию: **display.WHITE**
- `background_color (Display.Color | None)` — цвет незаполненной части. По умолчанию: **display.BLACK**

```python
display.linear_bar(50, 50, 5, 0, 10)
```

---
### `.circular_bar(center_x, center_y, r, value, min_value, max_value)`
Рисует круговой индикатор выполнения.

Заполненная дуга (от -90° до вычисленного угла) рисуется цветом *color*; остаток рисуется цветом *background_color*.

**Аргументы:**

- `center_x (int)` — X центра
- `center_y (int)` — Y центра
- `r (int)` — внутренний радиус в пикселях
- `value (float)` — текущее значение (ограничено min_value–max_value)
- `min_value (float)` — значение, соответствующее пустому индикатору
- `max_value (float)` — значение, соответствующее полному индикатору
- `width (int | None)` — радиальная толщина в пикселях. По умолчанию: **2**
- `color (Display.Color | None)` — цвет заполненной части. По умолчанию: **display.GREEN**
- `background_color (Display.Color | None)` — цвет незаполненной части. По умолчанию: **display.WHITE**

```python
display.circular_bar(50, 50, 20, 5, 0, 10)
```

---
## Другие функции

---
### `.sleep_mode(value)`
Вход (True) или выход (False) из режима сна.
Содержимое дисплея может не сохраняться во время сна.

**Аргументы:**

- `value (bool)` — режим сна вкл/выкл

```python
display.sleep_mode(True)
```

---
### `.logo()`
Рисует логотип продукта Artisan Education в позиции (x, y) с радиусом *r*.

Перед рисованием заполняет экран белым.

**Аргументы:**

- `x (int | None)` — колонка центра
- `y (int | None)` — строка центра
- `r (int | None)` — радиус логотипа

```python
display.logo()
```

---
### `.hsv(h, s, v) -> Display.Color`
Преобразует HSV в упакованное значение цвета RGB565.
Аналогично методу color(), но использует тон, насыщенность, яркость в качестве входных данных.

**Аргументы:**

- `h (float)` — тон в диапазоне **[0, 360]**
- `s (float)` — насыщенность в диапазоне **[0.0, 1.0]**
- `v (float)` — яркость в диапазоне **[0.0, 1.0]**

```python
text_color = display.hsv(200, 0.8, 1.0)

display.print("Привет", font = text_color)
```

---
## Конфигурация

---
### `.width() -> int`
Возвращает текущую логическую ширину дисплея в пикселях.

```python
width = display.width()
print(width)
```

---
### `.height() -> int`
Возвращает текущую логическую высоту дисплея в пикселях.

```python
height = display.height()
print(height)
```

---
### `.rotation(r)`
Поворачивает логический дисплей против часовой стрелки.

- `0` = Портрет **(0°)**
- `1` = Ландшафт **(90°)**
- `2` = Обратный портрет **(180°)**
- `3` = Обратный ландшафт **(270°)**

**Аргументы:**

- `r` — режим поворота от **0** до **3**

```python
display.rotation(2)
```

---
### `.offset(x_start, y_start)`
Переопределяет начальные смещения колонки/строки.

Вызывайте *после* `rotation()`, если требуется настроить для нестандартной панели.

**Аргументы:**

- `x_start (int)` — начальное смещение колонки
- `y_start (int)` — начальное смещение строки

```python
display.offset(10, 10)
```

---
### `.inversion_mode(value)`
Включает **(True)** или отключает **(False)** инверсию цветов дисплея.

**Аргументы:**

- `value (bool)` — состояние инверсии

```python
display.inversion_mode(True)
```

---
### `.madctl(value | None) -> None | int`
Получить (без аргумента) или установить (с аргументом) значение регистра MADCTL.
Управляет поворотом и порядком цветов на аппаратном уровне.

**Аргументы:**

- `value (int)` — значение регистра MADCTL

Возвращает текущее значение при вызове без аргумента, иначе устанавливает значение и возвращает None.

```python
display.madctl()
```

---
## Дополнительная информация

### Предустановленные цвета Display.Color

`Display.Color` предоставляет несколько предустановленных цветов, которые можно использовать с любым методом рисования.

| Имя | Описание |
|---|---|
| <span style="color: #000000; font-weight: bold;">display.BLACK</span>   | чистый чёрный |
| <span style="color: #0000FF; font-weight: bold;">display.BLUE</span>    | синий |
| <span style="color: #FF0000; font-weight: bold;">display.RED</span>     | красный |
| <span style="color: #00FF00; font-weight: bold;">display.GREEN</span>   | зелёный |
| <span style="color: #00FFFF; font-weight: bold;">display.CYAN</span>    | голубой |
| <span style="color: #FF00FF; font-weight: bold;">display.MAGENTA</span> | пурпурный |
| <span style="color: #FFFF00; font-weight: bold;">display.YELLOW</span>  | жёлтый |
| <span style="color: #FFFFFF; font-weight: bold;">display.WHITE</span>   | чистый белый |
