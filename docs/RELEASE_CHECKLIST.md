# Release Checklist

- [ ] Confirm no credentials, private IP addresses, precise private locations, or logs are committed.
- [ ] Verify filenames and links in README and docs.
- [ ] Validate Home Assistant configuration with `fr24_cyd_templates.yaml` installed.
- [ ] Confirm all 31 `sensor.fr24_cyd_*` entities are created.
- [ ] Validate and compile `esphome/cyd-flight-tracker.yaml` with the supported ESPHome release.
- [ ] Test a clean USB installation on the supported ESP32-2432S028-7789 CYD.
- [ ] Test Wi-Fi provisioning, Home Assistant discovery, API connection, and OTA update.
- [ ] Test splash display/skip, tap-anywhere navigation, all runtime controls, dim/night modes, and restart recovery.
- [ ] Test populated, empty, and partially populated flight data.
- [ ] Update version references and `CHANGELOG.md`.
- [ ] Review `DISCLAIMER.md`, `SECURITY.md`, license, attribution, and non-affiliation text.
- [ ] Create the GitHub release/tag and attach the tested ZIP if desired.
