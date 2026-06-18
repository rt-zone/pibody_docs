# Display
## Встроенные методы

### `.sleep_mode(bool)`

`bool` принимает значения False и True

Если `True` экран выключается и ничего не показывает Если `False` экран включается, показывая всё что было до этого (учитывая команды написанные во время “сна”)

### `.fill(color)`

Заполняет весь экран указанным цветом

`color` принимает десятеричное число с репрезентацией rgb c 16 битами (565) (00000 000000 00000)

### `.pixel(x, y, color)`

Рисует пиксель в указанном месте с определенным цветом

`x`, `y` — координаты

`color` — цвет

### `.hline(x, y, length, color)`

Рисует горизонтальную линию с указанной длиной

### `.vline(x, y, length, color)`

Рисует вертикальную линию с указанной длиной

### `.rect(x, y, width, height, color)`

Рисует полый квадрат с указанными шириной и высотой, у которого левый верхний угол начинается на x, y

### `.fill_rect(x, y, width, height, color)`

Рисует заполненный квадрат с указанными шириной и высотой, у которого левый верхний угол начинается на x, y

### `.circle(x, y, r, color)`

Рисует круг с радиусом `r`, центр которого находится на `x`, `y`

### `.fill_circle(x, y, r, color)`

Рисует заполненный круг с радиусом `r`, центр которого находится на `x`, `y`

### `.blit_buffer(buffer, x, y, width, height)`

Copy bytes() or bytearray() content to the screen internal memory. Note: every color requires 2 bytes in the array

### `.text(text, x, y[, font, fg, bg])` (Наша имплементация)

Пишет текст, у которого левый верхний угол начинается на x, y.

`fg` - цвет текста (по дефолту он белый)

`bg` - цвет фона (по дефолту он черный)

`font` - шрифт (по дефолту он `font_small`)

### `.write(bitmap_font, s, x, y[, fg, bg, background_tuple, fill_flag])`

Write text to the display using the specified proportional or Monospace bitmap font module with the coordinates as the upper-left corner of the text. The foreground and background colors of the text can be set by the optional arguments `fg` and `bg`, otherwise the foreground color defaults to `WHITE` and the background color defaults to `BLACK`.

Transparency can be emulated by providing a `background_tuple` containing (bitmap_buffer, width, height). This is the same format used by the jpg_decode method. See examples/T-DISPLAY/clock/clock.py for an example.

See the `README.md` in the `truetype/fonts` directory for example fonts. Returns the width of the string as printed in pixels. Accepts UTF8 encoded strings.

The `font2bitmap` utility creates compatible 1 bit per pixel bitmap modules from Proportional or Monospaced True Type fonts. The character size, foreground, background colors, and characters in the bitmap module may be specified as parameters. Use the -h option for details. If you specify a buffer_size during the display initialization, it must be large enough to hold the widest character (HEIGHT * MAX_WIDTH * 2).

### `.write_len(bitap_font, s)`

Returns the string's width in pixels if printed in the specified font.

### ~~`.draw(vector_font, s, x, y[, fg, scale])`~~ (Использует векторные фонты)

Draw text to the display using the specified Hershey vector font with the coordinates as the lower-left corner of the text. The foreground color of the text can be set by the optional argument `fg`. Otherwise the foreground color defaults to `WHITE`. The size of the text can be scaled by specifying a `scale` value. The `scale` value must be larger than 0 and can be a floating-point or an integer value. The `scale` value defaults to 1.0. See the [README.md](http://README.md) in the `vector/fonts` directory, for example fonts and the utils directory for a font conversion program.

### `.jpg_decode(jpg_filename [, x, y, width, height])`

Decode a jpg file and return it or a portion of it as a tuple composed of (buffer, width, height). The buffer is a color565 blit_buffer compatible byte array. The buffer will require width * height * 2 bytes of memory.

If the optional x, y, width, and height parameters are given, the buffer will only contain the specified area of the image. See examples/T-DISPLAY/clock/clock.py examples/T-DISPLAY/toasters_jpg/toasters_jpg.py for examples.

### `.png(png_filename, x, y [, mask])`

Draw a PNG file on the display with upper left corner of the image at the given `x` and `y` coordinates. The PNG will be clipped if it is not able to fit fully on the display. The PNG will be drawn one line at a time. Since the driver does not contain a frame buffer, transparency is not supported. Providing a `True` value for the `mask` parameter will prevent pixels with a zero alpha channel value from being displayed. Drawing masked PNG's is slower than non-masked as each visible line segment is drawn separately. For an example of using a mask, see the [alien.py](http://alien.py) program in the examples/png folder.

### `.polygon_center(polygon)`

Возвращает центр полигона в виде картежа (x, y)

`polygon` - список координат вершин полигона в виде картежа (x, y)

### `.fill_polygon(polygon, x, y, color[, angle, center_x, center_y])`

Рисует заполненный полигон `polygon` at the `x`, and `y` coordinates in the `color` given. The polygon may be rotated `angle` radians about the `center_x` and `center_y` point. The polygon should consist of a list of (x, y) tuples forming a closed convex polygon.

### …soon

## Наши методы

### `.text(text, x, y, font, fg, bg)` (Наша имплементация)

Пишет текст, у которого левый верхний угол начинается на x, y.

`fg` - цвет текста (по дефолту он белый)
`bg` - цвет фона (по дефолту он черный)

`font` - шрифт (по дефолту он `font_small`)

### `.color(r, g, b)`

Возвращает кодировку цвета в 565 формате (ffff - белый цвет)

`r`, `g`, `b` - принимает значения от 0 до 255

### `.draw_circle(color, center_x, center_y, r, [width, start_angle, end_angle])`

Рисует круг с радиусом `r` и шириной `wigth` с центром в координатах `center_x`, `center_y`.

`start_angle` - принимает значение, с которого начинает рисоваться круг (по дефолту это 0)

`end_angle` _-_ принимает значение, с которого закончится рисоваться круг (по дефолту это 360)

`width` _-_ принимает значение, которое определяет ширину окружности (по дефолту это 1)

### `.linear_bar(x, y, length, value, min_value, max_value, [height, border, color, border_color, background_color])`

Рисует квадратный индикатор прогресса на координатах `x`, `y`

`length` - принимает значение, которое определяет длину прогресс бара

`value` - принимает значение, которое нужно отрисовать в прогресс баре

`min_value` - минимальная граница значения, которая рисуется в прогресс баре

`max_value` - максимальная граница значения, которая рисуется в прогресс баре

`height` - высота прогресс бара (по дефолту это 5)

`border` - принимает значение `True` или `False`. Если `True` - прогресс бар будет “обернут” в границы. Если `False` - прогресс бар будет иметь линию по середине. (По дефолту это `True`)

`color` - определяет цвет шкалы, которая заполняется (по дефолту он зеленый)

`border_color` - определяет цвет границ (по дефолту он белый)

`background_color` - определяет цвет незаполненной части (по дефолту он черный)

### `.circular_bar(center_x, center_y, r, value, min_value, max_value, [width, color, background_color])`

Рисует круглый индикатор прогресса.

`center_x`, `center_y` - координаты центра прогресс бара

`r` - принимает значение, которое определяет радиус прогресс бара

`value` - принимает значение, которое нужно отрисовать в прогресс баре

`min_value` - минимальная граница значения, которая рисуется в прогресс баре

`max_value` - максимальная граница значения, которая рисуется в прогресс баре

`wigth` - принимает значение, которое определяет ширину прогресс бара (по дефолту это 2)

`color` - определяет цвет шкалы, которая заполняется (по дефолту он зеленый)

`background_color` - определяет цвет незаполненной части (по дефолту он белый)

### `.draw_poligon(*center_x*, *center_y*, *r*, *n*, [*bump*, *angle_offset*, *color*, *fill*])`

Рисует полигон

`center_x`, `center_y` - координаты центра полигона

`r` - принимает значение, которое определяет радиус до вершин

`n` - принимает значение, которое определяет количество вершин

`bump` - принимает значение, которое будет сжимать/разжимать середины ребер (по дефолту это 1.0)

`angle_offset` - принимает значение, на которое полигон будет повернут относительно начальной позиции (по дефолту она зависит от кол-ва вершин)

`color` - определяет цвет полигона (по дефолту он белый)

`fill` - принимает значения `True` или `False`. Если `True`, то полигон будет заполненным. Если `False`, то полигон будет полым (по дефолту это `False`)

### `.draw_logo([*x*, *y*, *r*])`

Рисует логотип Artisan Education

`x`, `y` - координаты центра логотипа (по дефолту это 120 и 100)

`r` - радиус логотипа (по дефолту это 80)

### `.print(text)`

Пишет на дисплее, словно это консоль (как `print()` в Python)