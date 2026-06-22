---
title: Sound Sensor
---
# Sound Sensor
Sound Sensor converts sound into an electrical signal.

---
### `SoundSensor(slot)`
To create a SoundSensor object, call `SoundSensor(slot)`.

Also you can use short alias `Sound(slot)`.

Since the sound sensor can work as digital and analog, as analog it can only be inserted into slots with an ADC (analog-to-digital converter), and there are only 2 such slots on the PiBody: `"C"` and `"F"`. For digital signal can be used in any slot.

**Args:**

- `slot (string | int | tuple)` - slot label ("A", "B", "C", "D", "E", "F", "G", "H"), pin port (0, 2 and etc.), tuple (0, Pin.OUT)

**Returns:**
    Return a ``SoundSensor`` object for *slot*.
```python
from pibody import SoundSensor

sound = SoundSensor("A")
```

---
### `.read() -> (int, float)`
Return (digital, analog) as a tuple.  
Digital signal **1** if sound was loud.  
Analog signal returns sound level in range **[0, 1.0]**. **0.5** is default, and it will be sinusoid wave info.

- `digital` - digital sound level **0 or 1**
- `analog` - analog sound level normalized in range from **0** to **1.0**

```python
sound.read()
```

```python
from pibody import Sound  # short alias
from time import sleep
 
sound = Sound("A")
 
while True:
	digital, analog = sound.read()
	if digital == 1:
		print("Sound is significant")
	else:
		print("Sound is not significant")
	
	print("Sound level:", analog)
	sleep(1)
```

---
### `.read_digital() -> int`
Return the digital sound level: **0 or 1**.

```python
data = sound.read_digital()
print(data)
```

---
### `.read_analog(normalized | None) -> float`
Return the analog sound level.

**Args**:
- `normalized` - if **True** returns a float in range **[0, 1.0]**.
If **False** returns the raw 16-bit ADC value in range **[0, 65535]**. Default is **True**

```python
data = sound.read_analog()
print(data)
```
