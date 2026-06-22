---
title: Buzzer Control
---
# Buzzer
The `pibody.Buzzer()` is a device that produces sound when it receives a signal. Buzzers are commonly used in security systems, timers, and various electronic devices where an audible alert is needed.

---
## Basic usage

---
### `Buzzer(slot) -> PWM`
To create a Buzzer object, call `Buzzer(slot)`.

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
Play a tone at **freq** Hz with **volume** for *duration* seconds.

**Args:**

- `freq (int)` - parameter `value` is optional which sets the pitch of the sound (how many times per second the element vibrates). Useful range is **[20, 5000]**. By default `value` is **1000**
- `volume (float)` - sets the volume and changes duty cycle of buzzer. It can contains value in range **[0, 1.0]**
- `duration (int)` - will make sound on this time in milliseconds

```python
# Plays a sound at 660 Hz for 0.5 seconds at full volume
buzzer.make_sound(660, 1, 500)
```

---
### `.volume(volume | None) -> None | float`
Get or set volume.

**Args:**

- `volume (float)` - parameter `volume` is optional which sets the volume and changes duty cycle of buzzer. It can contains value in range **[0, 1.0]**. By default `volume` is **1.0**

Returns the current volume when called with no argument, otherwise sets volume and returns None.

```python
buzzer.volume(0.1)

print(buzzer.volume())  # 0.1
```

---
### `.beep()`
Short high beep **(1000 Hz, 0.1 s)**.  
If you want to play a short beep sound without specifying frequency, volume, or duration, you can use the `.beep()` function.

```python
buzzer.beep()
```

---
### `.boop()`
Short low boop **(500 Hz, 0.1 s)**.  
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
## PWM

The buzzer generates sound through a piezo element that vibrates when the signal changes. For a piezo buzzer, `freq` controls pitch and `duty` controls volume.

### Recommended starting point

```python
buzzer.freq(440)   # A4 note — clear mid-range tone
buzzer.duty(0.5)   # maximum volume
```

---
### `.freq(value | None) -> None | int`

**Args:**

- `value (int)` - parameter `value` is optional which sets the pitch of the sound (how many times per second the element vibrates). By default `value` is **1000**

    - **20–200 Hz** — low, bass-like tones (rumbles, deep hums)
    - **200–2000 Hz** — mid-range; most musical notes and alarm beeps live here
    - **2000–5000 Hz** — high-pitched (squeaks, notification beeps)
    - Above **5000 Hz** — very shrill; may be quiet on small buzzers
    - Below **~20 Hz** — inaudible as a tone; produces separate clicks per cycle

If `value` is empty, method returns frequency thats used before.

```python
buzzer.freq(440)

print(buzzer.freq())  # 440
```

---
### `.duty(value | None) -> None | float`
A duty cycle of **0 or 1** creates a “flat” [`pibody.PWM`](pwm.md) signal. Such a signal will not produce sound on the buzzer. A duty cycle of **0.5** makes the buzzer’s volume the loudest.

For more convenient volume control, there is the `.volume()` function. It accepts values from **0 to 1**, where **0** is silent and **1** is maximum volume.

**Args:**

- `value (float)` - parameter `value` is optional which sets the duty cycle of PWM and changes volume of buzzer. It can contains value in range **[0, 1.0]**. By default `value` is **0.5** = maximum volume (square wave — equal on/off time)

If `value` is empty, method returns duty cycle thats used before.

```python
buzzer.duty(0.5)

print(buzzer.duty())  # 0.5
```

---
### `.duty_u16(value | None) -> None | int`
It same as `.duty()`, but uses raw values in range **[0, 65535]**.

**Args:**

- `value (int)` - parameter `value` is optional which sets the duty cycle of PWM and changes volume of buzzer. It can contains value in range **[0, 65535]**. By default `value` is **32768**  = maximum volume (square wave — equal on/off time)

If `value` is empty, method returns duty cycle thats used before.

```python
buzzer.duty_u16(32768)

print(buzzer.duty_u16())  # 32768
```

### Simple melody example

```python
from pibody import Buzzer
from time import sleep

buzzer = Buzzer("A")
buzzer.duty(0.5)   # max volume

# Notes (frequency, duration_s)
melody = [
    (262, 0.3),  # C4
    (294, 0.3),  # D4
    (330, 0.3),  # E4
    (349, 0.3),  # F4
    (392, 0.3),  # G4
    (440, 0.3),  # A4
    (494, 0.3),  # B4
    (523, 0.5),  # C5
]

for freq, dur in melody:
    buzzer.freq(freq)
    sleep(dur)

buzzer.off()
```
