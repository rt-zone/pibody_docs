---
title: Buzzer Control
---
# Buzzer
The `pibody.Buzzer()` is a device that produces sound when it receives a signal. Buzzers are commonly used in security systems, timers, and various electronic devices where an audible alert is needed.

---
## Basic usage

---
### `Buzzer(slot) -> PWM`
To create Buzzer object call `Buzzer(slot)`.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**  
Return a output [`pibody.PWM`](pwm.md) for *slot*.
```python
from pibody import Buzzer

buzzer = Buzzer("A")
```

---
### `.make_sound(freq, volume, duration)`
Play a tone at *freq* Hz with *volume* for *duration* seconds.

**Args:**

- `freq (int)` - sets the frequency of PWM. By default `frequency` is `1000`
- `volume (float)` - sets the volume and changes duty cycle of buzzer. It can contains value in range `[0, 1.0]`
- `duration (float)` - will make sound on this time in milliseconds

```python
# Plays a sound at 660 Hz for 0.5 seconds at full volume
buzzer.make_sound(660, 1, 0.5)
```

---
### `.freq(value | None) -> None | int`

**Args:**

- `value (int)` - parameter `value` is optional which sets the frequency of PWM. By default `value` is `1000`

If `value` is empty, method returns frequency thats used before.

```python
buzzer.freq(440)

print(buzzer.freq())  # 440
```

---
### `.duty(value | None) -> None | float`
A duty cycle of 0 or 1 creates a “flat” [`pibody.PWM`](pwm.md) signal. Such a signal will not produce sound on the buzzer. A duty cycle of 0.5 makes the buzzer’s volume the loudest.

For more convenient volume control, there is the `.volume()` function. It accepts values from 0 to 1, where 0 is silent and 1 is maximum volume.

**Args:**

- `value (float)` - parameter `value` is optional which sets the duty cycle of PWM and changes volume of buzzer. It can contains value in range [0, 1.0]. By default `value` is `0.5`

If `value` is empty, method returns duty cycle thats used before.

```python
buzzer.duty(0.5)

print(buzzer.duty())  # 0.5
```

---
## Other Functions

---
### `.volume(volume | None) -> None | float`
Get or set volume.

**Args:**

- `volume (float)` - parameter `volume` is optional which sets the volume and changes duty cycle of buzzer. It can contains value in range [0, 1.0]. By default `volume` is `1.0`

Returns the current volume when called with no argument, otherwise sets volume and returns None.

```python
buzzer.volume(0.1)

print(buzzer.volume())  # 0.1
```

---
### `.beep()`
Short high beep (1000 Hz, 0.1 s).  
If you want to play a short beep sound without specifying frequency, volume, or duration, you can use the `.beep()` function.

```python
buzzer.beep()
```

---
### `.boop()`
Short low boop (500 Hz, 0.1 s).  
If you want to play a short beep sound without specifying frequency, volume, or duration, you can use the `.boop()` function.

```python
buzzer.boop()
```

---
### `.on()`
Unmute and resume sound at the current volume.

```python
buzzer.on()
```

---
### `.off()`
Mute the buzzer (keeps frequency set).

```python
buzzer.off()
```

---
### `.duty_u16(value | None) -> None | int`
It same as `.duty()`, but uses not normalized values in range `[0, 65535]`.

**Args:**

- `value (int)` - parameter `value` is optional which sets the duty cycle of PWM and changes volume of buzzer. It can contains value in range [0, 65535]. By default `value` is `32768`

If `value` is empty, method returns duty cycle thats used before.

```python
buzzer.duty(32768)

print(buzzer.duty())  # 32768
```
