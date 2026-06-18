# PiBody Documentation

Welcome to the **PiBody** documentation site.

[PiBody](https://artisan.education) is an educational microcontroller board based on Raspberry Pico W, programmed in MicroPython. This site documents the `pibody` package — the
firmware library that provides a high-level API for all onboard and pluggable peripherals.

## Modules

| Modules | Description |
|---|---|
| Input (Analog) |
| [`pibody.LightSensor`](input/analog/light-sensor.md) | Analog input ADC (read a light sensor) |
| [`pibody.Potentiometer`](input/analog/potentiometer.md) | Analog input ADC (read a potentiometer state) |
| Input (Digital) |
| [`pibody.MotionSensor`](input/digital/motion-sensor.md) | Digital input pin (read a motion sensor) |
| [`pibody.Button`](input/digital/push-button.md) | Digital input pin (read a button) |
| [`pibody.Switch`](input/digital/switch.md) | Digital input pin (read a switch) |
| [`pibody.TouchSensor`](input/digital/touch-sensor.md) | Digital input pin (read a touch sensor) |
| Input (I2C) |
| [`pibody.ClimateSensor`](input/i2c/climate-sensor.md) | Temperature, humidity and pressure |
| [`pibody.ColorSensor`](input/i2c/color-sensor.md) | RGBW colour sensor |
| [`pibody.DistanceSensor`](input/i2c/distance-sensor.md) | Time-of-flight distance sensor |
| [`pibody.GyroAccel`](input/i2c/gyro-accel.md) | IMU (accelerometer + gyroscope) |
| Input |
| [`pibody.Joystick`](input/joystick.md) | 2-axis analogue joystick |
| [`pibody.Encoder`](input/encoder.md) | Rotary encoder |
| [`pibody.SoundSensor`](input/sound-sensor.md) | Sound detector (analogue + digital outputs) |
| Output |
| [`pibody.LED`](output/led.md) | Digital output pin (drives an LED) |
| [`pibody.Buzzer`](output/buzzer.md) | Piezo buzzer / speaker |
| [`pibody.LEDTower`](output/led-tower.md) | Addressable RGB LED strip |
| [`pibody.Display`](output/display.md) | 320×240 OLED display |
| [`pibody.Servo`](output/servo.md) | RC servo motor |
| [`pibody.PWM`](output/pwm.md) | Pulse-width modulation output (LED dimming, servo control) |
| IOT |
| [`pibody.WiFi`](iot/wifi.md) | WiFi manager |
| [`pibody.TelegramBot`](iot/telegram-bot.md) | Telegram bot API client |

## Quick start

```python
from pibody import LED

led = LED("A")    # LED on slot A
led.on()          # turn on
led.off()         # turn off
```

```python
from pibody import Button

btn = Button("B")      # Button on slot B
if btn.value() == 1:   # read
    print("pressed!")
```

---

*Documentation source: [`pibody_stubs`](https://github.com/artisan/pibody_stubs) — type stubs with Google-style docstrings used by this site and for IDE support.*
