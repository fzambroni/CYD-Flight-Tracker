# Changelog

All notable changes to this project will be documented here. The format follows Keep a Changelog, and the project intends to use Semantic Versioning.

## [0.1.2] - 2026-08-28

### Fixed

- Restored the correct ILI9342 controller profile and RGB color behavior.
- Changed the base LVGL orientation from 90° to 0° because ILI9342 is natively 320x240.
- Migrated the orientation preference key so an old saved 90° value cannot reapply the clipped 240x320 viewport after updating.

## [0.1.1] - 2026-08-28

### Fixed

- Changed the dual-USB CYD display preset to `ESP32-2432S028-7789` to correct the clipped upper edge and approximately 32-pixel blank strip at the right side caused by an incompatible controller address window.

## [0.1.0] - 2026-08-28

### Added

- Initial public release package.
- Nearby list for up to six aircraft and a nearest-aircraft detail page.
- Home Assistant templates backed by `sensor.flightradar24_current_in_area`.
- Runtime controls for display, themes, units, columns, navigation, dimming, and night mode.
- Runtime display orientation selector.
- Startup splash screen with configurable visibility and duration.
- Tap-anywhere page navigation and splash skipping.
- Installation, usage, security, contribution, disclaimer, and release documentation.
