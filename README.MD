# PiBody Documentation

Documentation site for the [PiBody](https://artisan.education) educational microcontroller board. Built with [MkDocs](https://www.mkdocs.org/).

## Quick start

```sh
# Install dependencies
pip install mkdocs mkdocs-i18n

# Start dev server
mkdocs serve

# Build static site
mkdocs build
```

The built site is output to `site/`.

## Project structure

```
docs/
├── index.md              # Home page
├── input/                # Input peripherals
│   ├── analog/           # Light sensor, potentiometer
│   ├── digital/          # Button, switch, motion/touch sensor
│   └── i2c/              # Climate, color, distance sensor, IMU
├── output/               # Output peripherals
├── iot/                  # WiFi, Telegram Bot
└── hardware.md           # Board overview
```

## License

© Artisan Education
