# Installation

## 1. Verify the hardware

The supplied firmware is for the dual-USB ESP32-2432S028 CYD using ESPHome's `ESP32-2432S028-9342` display model. Do not flash it unchanged to a different CYD revision. Photograph the board markings and back up an existing working configuration before changing hardware parameters.

You also need a data-capable USB cable, a 2.4 GHz Wi-Fi network, Home Assistant, ESPHome, and a configured Flightradar24 integration.

## 2. Configure Flightradar24 in Home Assistant

Install/configure the Flightradar24 integration using Home Assistant's current instructions. Confirm this source entity exists:

```text
sensor.flightradar24_current_in_area
```

In Developer Tools > States, verify it has a `flights` attribute. The templates expect fields such as distance, flight number or callsign, registration, aircraft code/model, origin/destination, altitude, and ground speed. Missing fields are displayed as `---` or zero.

## 3. Install the Home Assistant templates

Choose one supported Home Assistant configuration method.

### Packages

If packages are enabled, copy `home-assistant/fr24_cyd_templates.yaml` into your packages directory.

### Included template file

If your `configuration.yaml` contains:

```yaml
template: !include templates.yaml
```

merge the sensor list from the included file into `templates.yaml`. Do not add a second top-level `template:` key.

After saving, check the Home Assistant configuration and restart Home Assistant or reload Template Entities. Confirm at least these entities exist:

```text
sensor.fr24_cyd_aircraft_count
sensor.fr24_cyd_nearest_flight
sensor.fr24_cyd_row_1_flight
sensor.fr24_cyd_row_6_distance_km
```

The file generates 31 normalized sensors: aircraft count; seven nearest-aircraft values; and four fields for each of six rows.

## 4. Configure ESPHome secrets

Copy the values from `secrets.yaml.example` into the `secrets.yaml` used by your ESPHome installation and replace both placeholders:

```yaml
wifi_ssid: "YOUR_2_4_GHZ_WIFI_NAME"
wifi_password: "YOUR_WIFI_PASSWORD"
```

Never commit the real `secrets.yaml`.

## 5. Add and validate the firmware

Copy `esphome/cyd-flight-tracker.yaml` to your ESPHome configuration directory. Keep the two YAML files separate: the ESPHome file begins with `substitutions:` and `esphome:`; the Home Assistant file begins with `template:`.

Open the firmware in ESPHome and run **Validate**. Resolve validation or compilation errors before installation. ESPHome syntax and component behavior can change, so validation against your installed ESPHome release is authoritative.

## 6. First flash and Home Assistant pairing

Compile and install the first build by USB. After it joins Wi-Fi, add the discovered ESPHome device in Home Assistant. The supplied configuration uses the native API without an encryption key. If you add API encryption, update the YAML and Home Assistant pairing consistently; that change requires recompiling and reflashing.

The fallback access point is named `CYD Flight Tracker`. Its sample password is embedded in the firmware and should be changed before use in an untrusted environment; changing it requires recompilation.

## 7. Verify data flow

1. Confirm the FR24 source entity is populated.
2. Confirm `sensor.fr24_cyd_*` template entities update.
3. Confirm the CYD is online in the ESPHome integration.
4. Confirm the list and nearest pages update.
5. Tap anywhere to switch pages and tap during the splash to skip it.

## Updating

Read `CHANGELOG.md`, back up your working YAML, validate the new version, then install over the air. Use USB recovery if an OTA update changes network, API, display, or low-level board configuration incorrectly.

