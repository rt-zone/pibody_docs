---
title: Display
---
# Display
Singleton — always returns the same instance

---
## Basic usage

---
### `Display()`
To create a Display object, call `Display()`.

```python
from pibody import Display

display = Display()
```

Also you can directly call object from library.

```python
from pibody import display
```

---
### `.print(*args)`
Print *args* to a scrolling on-screen console.

Arguments are joined with spaces and prefixed with ``">> "``.
Long lines are wrapped to fit the display width.
``\\n`` characters trigger explicit line breaks.

**Args:**

- `*args (Any)` - 
- `font (Any)` - text font module: **font_small**, **font_medium**, **font_large** or **font_bold**. Default is **Display.font_medium**
- `color (Display.Color)` - text foreground colour. Default is **Display.WHITE**

```python
display.print("Hello,", "World!")  # >> Hello, World!
```

---
### `.text(text, x, y)`
Write *text* at (x, y) using *font*.

**Args:**

- `text (str | int | bytes)` - parameter to print
- `x (int)` - text column position
- `y (int)` - text row position
- `font (Any)` - test font module: **font_small**, **font_medium**, **font_large** or **font_bold**. Default is **Display.font_small**
- `fg (Display.Color)` - text foreground colour. Default is **Display.WHITE**
- `bg (Display.Color)` - text background colour. Default is **Display.BLACK**

```python
display.text("PiBody", 50, 50, font = font_bold)  # PiBody
```

---
### `.clear()`
Clear the display and reset the scroll console state.

```python
display.clear()
```

---
## Geometric shapes

---
### `.fill(color)`
Fill the entire display with *color*.

**Args:**

- `color (Display.Color)` - enter preset color, or input own

```python
display.fill(Display.WHITE)
```

---
### `.pixel(x, y, color)`
Set a single pixel at (x, y) to *color*.

**Args:**

- `x (int)` - pixel column (0 = left edge)
- `y (int)` - pixel row (0 = top edge)
- `color (Display.Color)` - pixel colour

```python
display.pixel(10, 10, Display.WHITE)
```

---
### `.line(x0, y0, x1, y1, color)`
Draw a line from (x0, y0) to (x1, y1) in *color*.

**Args:**

- `x0 (int)` - start column
- `y0 (int)` - start row
- `x1 (int)` - end column
- `y1 (int)` - end row
- `color (Display.Color)` - line colour

```python
display.line(10, 10, 20, 20, Display.BLUE)
```

---
### `.hline(x, y, length, color)`
Draw a fast horizontal line of *length* pixels starting at (x, y).

**Args:**

- `x (int)` - start column
- `y (int)` - row position
- `length (int)` - length of line in pixels
- `color (Display.Color)` - line colour

```python
display.hline(10, 10, 15, Display.BLACK)
```

---
### `.vline(x, y, length, color)`
Draw a fast vertical line of *length* pixels starting at (x, y).

**Args:**

- `x (int)` - column position
- `y (int)` - start row
- `length (int)` - length of line in pixels
- `color (Display.Color)` - line colour

```python
display.vline(10, 10, 15, Display.BLACK)
```

---
### `.crosshair(x, y, r, x_center, y_center, crosshair_radius)`
Renders a ball at the center of crosshair.  
x, y cords are relative and range from -1 to 1, where 0 is the middle of the crosshair.

**Args:**

- `x (float)` - relative X position **(-1 = left, 0 = centre, 1 = right)**
- `y (float)` - relative Y position **(-1 = bottom, 0 = centre, 1 = top)**
- `r (int)` - radius
- `x_center (int)` - left-centre anchor point's X
- `y_center (int)` - left-centre anchor point's Y
- `crosshair_radius (int)` - inner radius in pixels
- `color (Display.Color | None)` - primary color of crosshair. Default is **Display.RED**
- `border_color (Display.Color | None)` - colour of the border. Default is **Display.WHITE**
- `background_color (Display.Color | None)` - background color. Default is **Display.BLACK**

```python
display.crosshair(50, 50, 20, 0, 0, 5, background_color = Display.GREEN)
```

---
### `.rect(x, y, width, height, color)`
Draw a rectangle outline with the top-left corner at (x, y).

**Args:**

- `x (int)` - top-left column
- `y (int)` - top-left row
- `width (int)` - rectangle width
- `height (int)` - rectangle height
- `color (Display.Color)` - colour of rectangle's border

```python
display.rect(50, 50, 10, 20, Display.GREEN)
```

---
### `.fill_rect(x, y, width, height, color)`
Draw a filled rectangle with the top-left corner at (x, y).

**Args:**

- `x (int)` - top-left column
- `y (int)` - top-left row
- `width (int)` - rectangle width
- `height (int)` - rectangle height
- `color (Display.Color)` - color of full rectangle

```python
display.fill_rect(50, 50, 10, 20, Display.GREEN)
```

---
### `.circle(x, y, r, color)`
Draw a circle outline centred at (x, y) with radius *r*.

**Args:**

- `x (int)` - centre column
- `y (int)` - centre row
- `r (int)` - circle radius
- `color (Display.Color)` - color of circle's border

```python
display.circle(50, 50, 10, Display.GREEN)
```

---
### `.fill_circle(x, y, r, color)`
Draw a filled circle centred at (x, y) with radius *r*.

**Args:**

- `x (int)` - centre column
- `y (int)` - centre row
- `r (int)` - circle radius
- `color (Display.Color)` - fill color

```python
display.fill_circle(50, 50, 10, Display.GREEN)
```

---
### `.arc(color, center_x, center_y, r)`
Draw an arc (thick outline segment of a circle).

**Args:**

- `color (Display.Color)` - arc primary color
- `center_x (int)` - centre point's X
- `center_y (int)` - centre point's Y
- `r (int)` - inner radius in pixels
- `width (int | None)` -  = radial thickness in pixels. Default is **1**
- `start_angle (int | None)` - start of arc in degrees. Default is **0**
- `end_angle (int | None)` - end of arc in degrees. Default is **360**

```python
display.arc(display.WHITE, 50, 50, 20)
```

---
## Polygon drawing

---
### `.draw_polygon(center_x, center_y, r, n)`
Draw a regular *n*-sided polygon with optional mid-edge bulge.

**Args:**

- `center_x (int)` - left-centre anchor point's X
- `center_y (int)` - left-centre anchor point's Y
- `r (int)` - circumradius in pixels
- `n (int)` - number of sides
- `bump (float | None)` - mid-edge bulge factor relative to r (1.0 = flat). Default is **1.0**
- `angle_offset (float | None)` - rotation offset in degrees; auto-computed if None. Default is **None**
- `color (Display.Color | None)` - outline / fill colour. Default is **Display.WHITE**
- `fill (bool | None)` - filled polygon if **True**, outline only if **False**. Default is **False**

```python
display.draw_polygon(50, 50, 20, 4, color = Display.GREEN)
```

---
### `.polygon_center(polygon) -> (int, int)`
Return the centroid ``(x, y)`` of a closed convex *polygon*.

**Args:**

- `polygon (list[tuple[int, int]])` - list of coordinates. [(0, 0), (10, 0), (10, 10), (0, 10)]

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

center_x, center_y = display.polygon_center(poly)

print(center_x, center_y)
```

---
### `.polygon(polygon, x, y, color)`
Draw a polygon outline translated to (x, y), optionally rotated *angle* radians about (center_x, center_y).

**Args:**

- `polygon (list[tuple[int, int]])` - list of coordinates. [(0, 0), (10, 0), (10, 10), (0, 10)]
- `x (int)` - translation offset column
- `y (int)` - translation offset row
- `color (Display.Color)` - primary color of polygon
- `angle (float)` - rotation angle. Default is **0.0**
- `center_x (int)` - rotation pivot column. Default is **0**
- `center_y (int)` - rotation pivot row. Default is **0**

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

display.polygon(poly, 0, 0, Display.RED, angle = 45)
```

---
### `.fill_polygon(polygon, x, y, color)`
Draw a filled polygon translated to (x, y), optionally rotated *angle* radians about (center_x, center_y).

**Args:**

- `polygon (list[tuple[int, int]])` - list of coordinates. [(0, 0), (10, 0), (10, 10), (0, 10)]
- `x (int)` - translation offset column
- `y (int)` - translation offset row
- `color (Display.Color)` - primary color of polygon
- `angle (float)` - rotation angle. Default is **0.0**
- `center_x (int)` - rotation pivot column. Default is **0**
- `center_y (int)` - rotation pivot row. Default is **0**

```python
poly = [(0, 0), (10, 0), (10, 10), (0, 10)]

display.fill_polygon(poly, 0, 0, Display.RED, angle = 45)
```

---
### `.bounding() -> (int, int, int, int)`
Enable / disable dirty-rectangle tracking and query results.

Passing True or False resets the tracked rectangle and enables / disables tracking respectively.

Returns **(min_x, min_y, max_x, max_y)** or, if *as_rect* is True, **(min_x, min_y, width, height)**.

**Args:**

- `status (bool | None)` - Default is **None**
- `as_rect (bool | None)` - Default is **False**

```python
data = display.bounding()
print(data)
```

---
## Bitmap

---
### `.blit_buffer(buffer, x, y, width, height)`
Copy a raw RGB565 buffer to the display at (x, y).

*buffer* must contain **width * height * 2** bytes.

**Args:**

- `buffer (bytes | bytearray)` - buffer
- `x (int)` - top-left column
- `y (int)` - top-left row
- `width (int)` - rectangle width
- `height (int)` - rectangle height

```python
display.blit_buffer(buf, 50, 50, 60, 60)
```

---
### `.bitmap(bitmap, x, y)`
Draw a bitmap module (created by imgtobitmap.py or monofont2bitmap.py) at (x, y). Use *index* to select from multi-bitmap modules.

**Args:**

- `bitmap (Any)` - bitmap
- `x (int)` - top-left column
- `y (int)` - top-left row
- `index (int | None)` - multi-bitmap index. Default is **0**

```python
display.bitmap(bitmap, 0, 0)
```

---
## Image

---
### `.jpg(jpg, x, y)`
Draw a JPEG at (x, y).

**Args:**

- `jpg (str | bytes | bytearray)` - may be a filename string or a buffer containing JPEG data
- `x (int)` - top-left column
- `y (int)` - top-left row
- `method (int)` - render method. Use **Display.SLOW** for images that exceed available free RAM. Default is **Display.FAST**

```python
display.jpg("dog.jpg", 0, 0)
```

---
### `.jpg_decode(jpg) -> (bytearray, int, int)`
Decode a JPEG and return **(buffer, width, height)**.

**Args:**

- `jpg (str | bytes | bytearray)` - an RGB565 bytearray suitable for **blit_buffer**
- `x (int | None)` - crop start column. Default is **0**
- `y (int | None)` - crop start row. Default is **0**
- `width (int | None)` - width to crop the decoded image. Default is **None**
- `height (int | None)` - height to crop the decoded image. Default is **None**

```python
display.jpg_decode("dog.jpg")
```

---
### `.png(png, x, y)`
Draw a PNG file at (x, y). Transparency is not supported unless *mask* is True, in which case pixels with zero alpha are skipped (slower, drawn line-by-line).

**Args:**

- `png (str | bytes | bytearray)` - an RGB565 bytearray suitable for **blit_buffer**
- `x (int)` - top-left column
- `y (int)` - top-left row
- `mask (bool = False)` - transparency mode

```python
display.png("dog.jpg", 0, 0, mask = True)
```

---
## Text

---
### `.write(font, s, x, y) -> int`
Write UTF-8 *s* using a proportional bitmap *font* at (x, y). *proportional / TrueType bitmap fonts*.

Returns the `width` of the rendered string in pixels.

**Args:**

- `font (Any)` - bitmap font module: **font_small**, **font_medium**, **font_large** or **font_bold**. Default is **Display.font_medium**
- `s (str)` - text to be showed
- `x (int)` - text column position
- `y (int)` - text row position

```python
display.write(Display.font_medium, "Hello", 10, 10)
```

---
### `.write_len(font, s) -> int`
Return the pixel length of *s* when rendered with *font*. *proportional / TrueType bitmap fonts*.

**Args:**

- `font (Any)` - bitmap font module: **font_small**, **font_medium**, **font_large** or **font_bold**. Default is **Display.font_medium**
- `s (str)` - text to be showed

```python
length = display.write_len(Display.font_medium, "PiBody")
print(length)
```

---
### `.draw(font, s, x, y)`
Draw *s* using a Hershey vector *font* with (x, y) as the *lower-left* corner of the text. *scale* must be > 0. *Hershey vector fonts*.

**Args:**

- `font (Any)` - bitmap font module: **font_small**, **font_medium**, **font_large** or **font_bold**. Default is **Display.font_medium**
- `s (str)` - text to be showed
- `x (int)` - lower-left column
- `y (int)` - lower-left row
- `fg (Display.Color | None)` - text foreground colour. Default is **Display.WHITE**
- `scale (float | None)` - scale. Default is **1.0**

```python
display.draw(Display.font_medium, "PiBody", 15, 15)
```

---
### `.draw_len(font, s)`
Return the pixel length of *s* when drawn with *font* at *scale*. *Hershey vector fonts*.

**Args:**

- `font (Any)` - bitmap font module: **font_small**, **font_medium**, **font_large** or **font_bold**. Default is **Display.font_medium**
- `s (str)` - text to be showed
- `scale (float | None)` - scale. Default is **1.0**

```python
length = display.draw_len(Display.font_medium, "PiBody", 15, 15)
print(length)
```

---
## Progress bar

---
### `.linear_bar(x, y, value, min_value, max_value)`
Draw a horizontal progress bar centred vertically on *y*.

**Args:**

- `x (int)` - left-centre anchor point's X
- `y (int)` - left-centre anchor point's Y
- `value (float)` - current value (clamped to min_value–max_value)
- `min_value (float)` - value that corresponds to an empty bar
- `max_value (float)` - value that corresponds to a full bar
- `length (int | None)` - total bar length in pixels. Default is **100**
- `height (int | None)` - bar height in pixels. Default is **5**
- `border (bool | None)` - = if `True`, draw a rectangular border and flood the empty region; if **False**, draw end caps and a centre line instead. Default is **False**
- `bar_color (Display.Color | None)` - colour of the filled portion. Default is **Display.GREEN**
- `border_color (Display.Color | None)` - colour of the border / end caps / centre line. Default is **Display.WHITE**
- `background_color (Display.Color | None)` - colour of the unfilled portion. Default is **Display.BLACK**

```python
display.linear_bar(50, 50, 5, 0, 10)
```

---
### `.circular_bar(center_x, center_y, r, value, min_value, max_value)`
Draw a circular progress bar.

The filled arc (from -90° to the computed angle) is drawn in *color*; the remainder is drawn in *background_color*.

**Args:**

- `center_x (int)` - centre point's X
- `center_y (int)` - centre point's Y
- `r (int)` - inner radius in pixels
- `value (float)` - current value (clamped to min_value–max_value)
- `min_value (float)` - value that corresponds to an empty bar
- `max_value (float)` - value that corresponds to a full bar
- `width (int | None)` - radial thickness in pixels. Default **2**
- `color (display.Color | None)` - colour of the filled portion. Default is **Display.GREEN**
- `background_color (display.Color | None)` - colour of the unfilled portion. Default is **Display.WHITE**

```python
display.circular_bar(50, 50, 20, 5, 0, 10)
```

---
## Other Functions

---
### `.sleep_mode(value)`
Enter (True) or exit (False) sleep mode.  
Display content may not be preserved during sleep.

**Args:**

- `value (bool)` - sleep mode on/off

```python
display.sleep_mode(True)
```

---
### `.logo()`
Draw the Artisan Education product logo at (x, y) with radius *r*.

Fills the screen white before drawing.

**Args:**

- `x (int | None)` - centre column
- `y (int | None)` - centre row
- `r (int | None)` - radius of logo

```python
display.logo()
```

---
### `.hsv(h, s, v) -> Display.Color`
Convert HSV to a packed RGB565 colour value.  
Analogous to color() method, but uses hue, saturation, value as inputs.

**Args:**

- `h (float)` - hue in range **[0, 360]**
- `s (float)` - saturation in range **[0.0, 1.0]**
- `v (float)` - value / brightness in range **[0.0, 1.0]**

```python
text_color = display.hsv(200, 0.8, 1.0)

display.print("Hi", font = text_color)
```

---
## Configuration

---
### `.width() -> int`
Return the current logical display width in pixels.

```python
width = display.width()
print(width)
```

---
### `.height() -> int`
Return the current logical display height in pixels.

```python
height = display.height()
print(height)
```

---
### `.rotation(r)`
Rotate the logical display counter-clockwise.

- `0` = Portrait **(0°)**
- `1` = Landscape **(90°)**
- `2` = Inverse Portrait **(180°)**
- `3` = Inverse Landscape **(270°)**

**Args:**

- `r` - rotation mode from **0** to **3**

```python
display.rotation(2)
```

---
### `.offset(x_start, y_start)`
Override the column/row start offsets.

Call *after* ``rotation()`` if you need to adjust for a non-standard panel layout.

**Args:**

- `x_start (int)` - column start offset
- `y_start (int)` - row start offset

```python
display.offset(10, 10)
```

---
### `.inversion_mode(value)`
Enable **(True)** or disable **(False)** display color inversion.

**Args:**

- `value (bool)` - value state

```python
display.inversion_mode(True)
```

---
### `.madctl(value | None) -> None | int`
Get (no argument) or set (with argument) the MADCTL register value.  
Controls rotation and color order at the hardware level.

**Args:**

- `value (int)` - MADCTL register value

Returns the current value when called with no argument, otherwise sets value and returns None.

```python
display.madctl()
```

---
## Additional info

### Display.Color preset colors

`Display.Color` provides several preset colours you can use with any drawing method.

| Name | Description |
|---|---|
| <span style="color: #000000; font-weight: bold;">Display.BLACK</span>   | pure black |
| <span style="color: #0000FF; font-weight: bold;">Display.BLUE</span>    | blue |
| <span style="color: #FF0000; font-weight: bold;">Display.RED</span>     | red |
| <span style="color: #00FF00; font-weight: bold;">Display.GREEN</span>   | green |
| <span style="color: #00FFFF; font-weight: bold;">Display.CYAN</span>    | cyan |
| <span style="color: #FF00FF; font-weight: bold;">Display.MAGENTA</span> | magenta |
| <span style="color: #FFFF00; font-weight: bold;">Display.YELLOW</span>  | yellow |
| <span style="color: #FFFFFF; font-weight: bold;">Display.WHITE</span>   | pure white |
