# Async MQTT client compatibility fork for ESP8266 and ESP32

[![Build Status](https://github.com/labodj/async-mqtt-client/actions/workflows/push.yml/badge.svg)](https://github.com/labodj/async-mqtt-client/actions/workflows/push.yml)

This repository is the LSH compatibility fork of
[AsyncMqttClient](https://github.com/marvinroger/async-mqtt-client). Its
lineage is `marvinroger` -> `OttoWinter` -> `HeMan` -> `labodj`; the
`-esphome` package name is inherited from the OttoWinter fork. This project is
not maintained by or for the ESPHome project.

## Why this fork exists

The HeMan release used by Homie pins the discontinued `esphome` async TCP
packages and does not compile with current ESP32 Arduino 3 toolchains. This
fork keeps that MQTT implementation and public API while switching its network
dependencies to the maintained
[ESP32Async](https://github.com/ESP32Async) packages:

- `ESP32Async/ESPAsyncTCP ^2.0.0` on ESP8266
- `ESP32Async/AsyncTCP ^3.5.0` on ESP32 and LibreTiny

It also handles the current ESP32 `AsyncClient::close()` API without changing
the immediate-close behavior required by the ESP8266 backend. There are no
other intentional changes to MQTT behavior relative to HeMan 2.1.0.

## Features

- MQTT 3.1.1
- Fully asynchronous operation
- Subscribe and publish at QoS 0, 1 and 2
- ESP8266, ESP32 Arduino 2, and ESP32 Arduino 3 CI builds

The current ESP32Async transports do not provide the historical asynchronous
SSL/TLS path. See [limitations and known issues](docs/4.-Limitations-and-known-issues.md).

## Installation

The package is available in the
[PlatformIO Registry](https://registry.platformio.org/libraries/labodj/AsyncMqttClient-esphome):

```ini
lib_deps =
  labodj/AsyncMqttClient-esphome@^2.1.4
```

Firmware projects that require fully reproducible dependency resolution should
pin a release archive or exact commit instead of a version range.

API and usage documentation is in the [docs folder](docs).
