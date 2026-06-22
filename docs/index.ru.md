# Документация PiBody

Добро пожаловать на сайт документации **PiBody**.

[PiBody](https://artisan.education) — это образовательная микроконтроллерная плата на базе Raspberry Pico W, программируемая на MicroPython. На этом сайте описана документация пакета `pibody` — библиотеки прошивки, предоставляющей высокоуровневый API для всех встроенных и подключаемых периферийных устройств.

## Модули

| Модули | Описание |
|---|---|
| Ввод (Аналоговый) |
| [`pibody.LightSensor`](input/analog/light-sensor.md) | Аналоговый ввод АЦП (чтение датчика освещённости) |
| [`pibody.Potentiometer`](input/analog/potentiometer.md) | Аналоговый ввод АЦП (чтение состояния потенциометра) |
| Ввод (Цифровой) |
| [`pibody.MotionSensor`](input/digital/motion-sensor.md) | Цифровой входной пин (чтение датчика движения) |
| [`pibody.Button`](input/digital/push-button.md) | Цифровой входной пин (чтение кнопки) |
| [`pibody.Switch`](input/digital/switch.md) | Цифровой входной пин (чтение переключателя) |
| [`pibody.TouchSensor`](input/digital/touch-sensor.md) | Цифровой входной пин (чтение сенсорного датчика) |
| Ввод (I2C) |
| [`pibody.ClimateSensor`](input/i2c/climate-sensor.md) | Температура, влажность и давление |
| [`pibody.ColorSensor`](input/i2c/color-sensor.md) | RGBW датчик цвета |
| [`pibody.DistanceSensor`](input/i2c/distance-sensor.md) | Лазерный дальномер |
| [`pibody.GyroAccel`](input/i2c/gyro-accel.md) | IMU (акселерометр + гироскоп) |
| Ввод |
| [`pibody.Joystick`](input/joystick.md) | Двухосевой аналоговый джойстик |
| [`pibody.Encoder`](input/encoder.md) | Вращающийся энкодер |
| [`pibody.SoundSensor`](input/sound-sensor.md) | Датчик звука (аналоговый + цифровой выходы) |
| Вывод |
| [`pibody.LED`](output/led.md) | Цифровой выходной пин (управление светодиодом) |
| [`pibody.Buzzer`](output/buzzer.md) | Пьезоизлучатель / динамик |
| [`pibody.LEDTower`](output/led-tower.md) | Адресуемая RGB светодиодная лента |
| [`pibody.Display`](output/display.md) | 320×240 OLED дисплей |
| [`pibody.Servo`](output/servo.md) | RC сервопривод |
| [`pibody.PWM`](output/pwm.md) | Широтно-импульсная модуляция (диммирование LED, управление серво) |
| IoT |
| [`pibody.WiFi`](iot/wifi.md) | Менеджер Wi-Fi |
| [`pibody.TelegramBot`](iot/telegram-bot.md) | API-клиент Telegram Bot |

## Быстрый старт

```python
from pibody import LED

led = LED("A")    # светодиод на слот A
led.on()          # включить
led.off()         # выключить
```

```python
from pibody import Button

btn = Button("B")      # кнопка на слот B
if btn.value() == 1:   # чтение
    print("нажато!")
```

---

*Исходный код документации: [`pibody_libs`](https://github.com/artisan/pibody_libs) — оригинальная библиотека PiBody.*
