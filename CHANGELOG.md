# Changelog

All notable changes to this project will be documented here. The format follows Keep a Changelog, and the project intends to use Semantic Versioning.

## [0.2.9] - 2026-08-28

### Fixed

- Removed lambda actions adjacent to `binary_sensor.is_on` conditions in the connectivity scripts, preventing the target validator from merging them into one condition item.
- Internet status text is now assigned explicitly in the available/unavailable branches.

## [0.2.8] - 2026-08-28

### Fixed

- Removed the conditional recovery script that caused the target ESPHome validator to combine `condition` and `script.execute` into one action.
- Connectivity state transitions now use template binary-sensor `on_press` triggers for showing and dismissing the unavailable page.

## [0.2.7] - 2026-08-28

### Fixed

- Removed unsupported `update_interval` options from template binary sensors for compatibility with the target ESPHome version.

## [0.2.6] - 2026-08-28

### Fixed

- Moved the connectivity recovery condition into a separate script so `update_connectivity_page` contains only one top-level `if`, avoiding another duplicate-key validation error in the target ESPHome editor.

## [0.2.5] - 2026-08-28

### Fixed

- Replaced repeated `binary_sensor.is_on` entries inside `and` conditions with single composite internal status sensors, avoiding duplicate-key errors from the target ESPHome YAML validator.

## [0.2.4] - 2026-08-28

### Fixed

- Replaced all lambda conditions in the connectivity-page decision block with internal template binary sensors and `binary_sensor.is_on/is_off` conditions for compatibility with stricter ESPHome YAML validation.

## [0.2.3] - 2026-08-28

### Fixed

- Flattened the connectivity-page conditions to avoid a duplicate-key validation error in ESPHome versions that reject nested lambda conditions in this automation block.

## [0.2.2] - 2026-08-28

### Fixed

- Replaced the generic API connection count with explicit Home Assistant client connect/disconnect tracking.
- ESPHome log, dashboard, and OTA connections no longer prevent the Service Unavailable page from appearing when Home Assistant is offline.

## [0.2.1] - 2026-08-28

### Fixed

- Updated the Home Assistant API connection check to use the zero-argument `APIServer::is_connected()` method supported by the target ESPHome build.
- Changed the dynamic internet-status label lambda to return `std::string`, as required by the LVGL label update action.

## [0.2.0] - 2026-08-28

### Added

- Added an automatic Service Unavailable page with separate Wi-Fi, internet, and Home Assistant connection indicators.
- Added a configurable compile-time internet connectivity endpoint, checked at boot and every 30 seconds.
- Added automatic return to the configured flight page when Home Assistant reconnects.

## [0.1.4] - 2026-08-28

### Added

- Added a `Large` 14 px table-font preset alongside Tiny, Small, and Medium.

### Changed

- Restored persistent display orientation. The last selected 0° or 180° landscape orientation now survives a restart.

## [0.1.3] - 2026-08-28

### Fixed

- Explicitly forced the ILI9342 address window to 320x240 with zero offsets and padding.
- Disabled restoration of the obsolete 90-degree orientation preference so boot consistently uses the native landscape viewport.
- Added a one-pixel-inset 318x238 frame to the Nearby and Nearest pages so all four border lines remain inside the drawable area.

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
