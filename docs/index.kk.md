# PiBody Анықтамалығы

**PiBody** анықтамалық сайтына қош келдіңіз.

[PiBody](https://artisan.education) — Raspberry Pico W негізіндегі, MicroPython тілінде бағдарламаланатын білім беру микроконтроллерлік платасы. Бұл сайт `pibody` пакетінің — барлық кірістірілген және қосылатын перифериялық құрылғыларға арналған жоғары деңгейлі API беретін firmware кітапханасының анықтамалығын сипаттайды.

## Модульдер

| Модульдер | Сипаттамасы |
|---|---|
| Кіріс (Аналогты) |
| [`pibody.LightSensor`](input/analog/light-sensor.md) | Аналогты кіріс АЦП (жарық сенсорын оқу) |
| [`pibody.Potentiometer`](input/analog/potentiometer.md) | Аналогты кіріс АЦП (потенциометр күйін оқу) |
| Кіріс (Сандық) |
| [`pibody.MotionSensor`](input/digital/motion-sensor.md) | Сандық кіріс пины (қозғалыс сенсорын оқу) |
| [`pibody.Button`](input/digital/push-button.md) | Сандық кіріс пины (түймені оқу) |
| [`pibody.Switch`](input/digital/switch.md) | Сандық кіріс пины (ауыстырғышты оқу) |
| [`pibody.TouchSensor`](input/digital/touch-sensor.md) | Сандық кіріс пины (жанасу сенсорын оқу) |
| Кіріс (I2C) |
| [`pibody.ClimateSensor`](input/i2c/climate-sensor.md) | Температура, ылғалдылық және қысым |
| [`pibody.ColorSensor`](input/i2c/color-sensor.md) | RGBW түс сенсоры |
| [`pibody.DistanceSensor`](input/i2c/distance-sensor.md) | Лазерлік қашықтық өлшегіш |
| [`pibody.GyroAccel`](input/i2c/gyro-accel.md) | IMU (акселерометр + гироскоп) |
| Кіріс |
| [`pibody.Joystick`](input/joystick.md) | Екі осьті аналогты джойстик |
| [`pibody.Encoder`](input/encoder.md) | Айналмалы энкодер |
| [`pibody.SoundSensor`](input/sound-sensor.md) | Дыбыс детекторы (аналогты + сандық шығыстар) |
| Шығыс |
| [`pibody.LED`](output/led.md) | Сандық шығыс пины (жарықдиодты басқару) |
| [`pibody.Buzzer`](output/buzzer.md) | Пьезо дыбыстағыш / динамик |
| [`pibody.LEDTower`](output/led-tower.md) | Мекенжайланатын RGB жарықдиодты лента |
| [`pibody.Display`](output/display.md) | 320×240 OLED дисплей |
| [`pibody.Servo`](output/servo.md) | RC сервоқозғалтқыш |
| [`pibody.PWM`](output/pwm.md) | Импульстік ендік модуляциясы (LED күңгірттеу, серво басқару) |
| IoT |
| [`pibody.WiFi`](iot/wifi.md) | Wi-Fi менеджері |
| [`pibody.TelegramBot`](iot/telegram-bot.md) | Telegram Bot API клиенті |

## Жылдам бастау

```python
from pibody import LED

led = LED("A")    # LED A слотында
led.on()          # қосу
led.off()         # өшіру
```

```python
from pibody import Button

btn = Button("B")      # B слотындағы түйме
if btn.value() == 1:   # оқу
    print("басылды!")
```

---

*Анықтамалықтың бастапқы коды: [`pibody_libs`](https://github.com/artisan/pibody_libs) — PiBody түпкі кітапханасы.*
