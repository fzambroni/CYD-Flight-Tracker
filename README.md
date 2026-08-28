# CYD Flight Tracker

CYD Flight Tracker turns a 2.8-inch ESP32 Cheap Yellow Display (CYD) into a compact nearby-aircraft display powered by Home Assistant and its Flightradar24 integration.

It provides two touch pages:

- **Nearby** — up to six aircraft with flight/callsign, aircraft type, route, and distance.
- **Nearest** — the closest aircraft with distance, altitude, and ground speed.

Tap anywhere on either page to switch pages. At startup, an optional splash screen displays **CYD Flight Tracker** and **Dev. By Fabricio Zambroni**; tapping it skips the delay.

## Architecture

```text
Flightradar24 integration
          |
          v
Home Assistant template sensors
          |
          v  ESPHome native API (local network)
ESP32-2432S028-9342 CYD
```

The display does not contact Flightradar24 directly. Home Assistant obtains the integration data, the included templates normalize it, and ESPHome subscribes to those template entities.

## Supported hardware

The included firmware targets the **ESP32-2432S028 dual-USB CYD with an ILI9342 display**, selected in ESPHome as `ESP32-2432S028-9342`. The ILI9342 profile is natively 320x240, so the landscape interface uses a base LVGL rotation of 0°. Other CYD revisions—including ILI9341 and ST7789V variants—require a different display model and may also require different GPIO assignments, color order, or touch calibration.

## Requirements

- A supported dual-USB ESP32-2432S028-9342 CYD and a data-capable USB cable
- Home Assistant with the ESPHome integration
- ESPHome capable of the `mipi_spi`, LVGL, and runtime display-rotation features used by the YAML
- Home Assistant's Flightradar24 integration configured so `sensor.flightradar24_current_in_area` exists and exposes a `flights` attribute
- A 2.4 GHz Wi-Fi network reachable by both Home Assistant and the CYD

## Repository layout

```text
.
|-- esphome/cyd-flight-tracker.yaml
|-- home-assistant/fr24_cyd_templates.yaml
|-- docs/INSTALLATION.md
|-- docs/USER_GUIDE.md
|-- docs/RELEASE_CHECKLIST.md
|-- secrets.yaml.example
|-- CHANGELOG.md
|-- CONTRIBUTING.md
|-- DISCLAIMER.md
|-- SECURITY.md
`-- LICENSE
```

## Quick start

1. Install and configure Home Assistant's Flightradar24 integration.
2. Add `home-assistant/fr24_cyd_templates.yaml` to Home Assistant and restart or reload Template Entities.
3. Confirm `sensor.fr24_cyd_row_1_flight` exists.
4. Copy `esphome/cyd-flight-tracker.yaml` into ESPHome.
5. Add Wi-Fi values from `secrets.yaml.example` to ESPHome's `secrets.yaml`.
6. Validate, compile, and install by USB for the first flash.
7. Add the ESPHome device to Home Assistant.

See [Installation](docs/INSTALLATION.md) for complete instructions and [User Guide](docs/USER_GUIDE.md) for controls and troubleshooting.

## Runtime settings versus recompilation

Most daily settings are Home Assistant entities and do **not** require recompilation: brightness, splash visibility and duration, orientation, auto-dim, night brightness and hours, page selection, automatic cycling, row count, column visibility, themes, font-size preset, and unit choices.

Recompile when changing hardware-dependent or structural configuration: board/display model, GPIOs, bus wiring, touch calibration/transform, Wi-Fi credentials, fallback access-point credentials, API/OTA security, or the LVGL page/widget layout. See the full matrix in the [User Guide](docs/USER_GUIDE.md#runtime-controls-and-recompilation).

## Privacy and network behavior

The CYD connects to the configured Wi-Fi network and communicates with Home Assistant over the ESPHome native API. The firmware contains no direct third-party HTTP client. Home Assistant's Flightradar24 integration may communicate with third-party services according to that integration's implementation and configuration. Logs and entity states can expose nearby aircraft data and local network details; share diagnostics carefully.

## Status and limitations

This is hobby software. Flight data may be delayed, incomplete, unavailable, or inaccurate. Coverage and fields depend on the upstream integration and service. Third-party APIs, integrations, entity names, and schemas may change without notice. Do not use this project for navigation, flight operations, safety, surveillance, or emergency decisions.

## Attribution and non-affiliation

Developed by Fabricio Zambroni. Built with the open-source [ESPHome](https://esphome.io/), [LVGL](https://lvgl.io/), and [Home Assistant](https://www.home-assistant.io/) ecosystems and designed for commonly sold CYD hardware. Flight data is supplied through Home Assistant's Flightradar24 integration.

This project is unofficial and is not affiliated with, endorsed by, or sponsored by Flightradar24, Home Assistant, ESPHome, LVGL, Espressif, or any hardware manufacturer or vendor. Names and trademarks belong to their respective owners.

## License

Project-authored code and documentation are released under the [MIT License](LICENSE). Third-party projects and services remain subject to their own licenses and terms.
