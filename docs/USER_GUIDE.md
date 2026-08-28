# User Guide

## Display pages

**Splash:** optionally shown at boot with the project title and developer credit. Tap anywhere to skip it.

**Nearby:** shows up to six aircraft sorted by the distance supplied by the Home Assistant templates. Columns can show flight/callsign, aircraft type, route, and distance.

**Nearest:** shows the closest aircraft and its flight/callsign, type, route, distance, altitude, and speed.

There are no visible navigation buttons. Tap anywhere on Nearby to open Nearest; tap anywhere on Nearest to return to Nearby. A touch also wakes a dimmed display.

## Runtime controls and recompilation

These ESPHome entities are exposed to Home Assistant. Entity IDs normally use the `cyd_flight_tracker` prefix, but Home Assistant may adjust them if a name already exists.

| Control | Type | Runtime behavior |
|---|---|---|
| Display Brightness | Number | Normal backlight level |
| Splash Duration | Number | Splash delay, 1–10 seconds |
| Auto Dim Timeout | Number | Idle delay before dimming |
| Dim Brightness | Number | Dimmed backlight level |
| Night Brightness | Number | Night-mode backlight level |
| Night Start/End Hour | Number | Night-mode schedule |
| Auto Cycle Interval | Number | Delay between automatic page changes |
| Nearby Rows | Number | Visible list rows, 1–6 |
| Display Orientation | Select | 0°, 90°, 180°, or 270° |
| Default Page / Current Page | Select | Startup target and immediate navigation |
| Accent Theme / Surface Theme | Select | Prepared color presets |
| Table Font Size | Select | Tiny, Small, or Medium preset |
| Distance / Altitude / Speed Unit | Select | Display conversion units |
| Show Splash Screen | Switch | Enables the startup splash |
| Display Enabled | Switch | Enables/disables the display |
| Auto Dim / Night Mode / Auto Cycle | Switch | Power and navigation behaviors |
| Show Column Header / Aircraft Count | Switch | Header visibility |
| Show Type / Route / Distance Column | Switch | Table column visibility |
| Next Page / Return to Default Page | Button | Navigation actions |
| Wake Display | Button | Restores active brightness |
| Restart Device | Button | Restarts the ESP32 |

All controls above are runtime-configurable in Home Assistant and do not require recompilation. Values configured with persistence are restored after reboot.

The following changes require validation, compilation, and installation:

- ESP32 board or CYD/display-controller variant
- GPIO and SPI assignments
- display driver, color order/depth, and inversion settings
- touch calibration and coordinate transforms
- Wi-Fi credentials and fallback access-point configuration
- native API or OTA security settings
- adding fonts, themes, pages, widgets, sensors, or new behavior
- changing the hard-coded splash text or developer credit

Although orientation is a runtime select in this firmware, the display/rotation capability itself must remain enabled and supported by the installed ESPHome version.

## Suggested Home Assistant dashboard

Add the device's configuration entities to an Entities card. Keep frequently used controls—brightness, current page, row count, units, and theme—visible, and place maintenance buttons in a separate card to prevent accidental restarts.

## Troubleshooting

### ESPHome says the `esphome` section is missing

The Home Assistant template file was opened in ESPHome. Use `esphome/cyd-flight-tracker.yaml` in ESPHome and `home-assistant/fr24_cyd_templates.yaml` in Home Assistant.

### The display has wrong colors, corruption, or no image

Confirm the board is the ST7789V dual-USB variant. A black strip of roughly 30–32 pixels combined with clipping on the opposite edge usually indicates the wrong controller preset, not an LVGL margin problem. ILI9341 and ILI9342 variants need their corresponding display model. Do not randomly change GPIOs while powered. Restore a known-good board configuration and validate again.

### The image or touch is rotated/mirrored

Try the Display Orientation entity first. If visual and touch coordinates still disagree, the hardware-specific touch `calibration` or `transform` values require editing and recompilation.

### No aircraft appear

Check the chain in order: `sensor.flightradar24_current_in_area`, its `flights` attribute, `sensor.fr24_cyd_aircraft_count`, row sensors, then the ESPHome device connection. No aircraft in the configured area is a valid state.

### Values show `---` or `0`

The upstream flight record did not include that field, or an integration schema changed. Inspect the source `flights` attribute and update the templates if field names have changed.

### The device is offline

Confirm 2.4 GHz Wi-Fi availability, credentials, DHCP, and Home Assistant reachability. Use the fallback access point or USB logs for recovery. Avoid posting logs without removing SSIDs, IP addresses, and identifiers.

### Controls do not retain values

Wait briefly after changing a control before power loss. If the problem continues, inspect ESPHome logs for preference/storage warnings.

## Limitations

- The list is limited to six aircraft.
- Sorting and data freshness depend on Home Assistant and the integration.
- Aircraft type, route, altitude, and speed may be absent.
- This is not a certified aviation instrument.
- Upstream integrations, APIs, attributes, service terms, and ESPHome components may change.
