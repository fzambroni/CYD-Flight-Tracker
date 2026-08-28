# Security Policy

## Supported versions

Until the project reaches a stable release, security fixes apply to the latest version on the default branch only.

## Reporting a vulnerability

Do not disclose a vulnerability publicly before a fix is available. Use GitHub's private vulnerability-reporting feature if enabled. Otherwise, contact the repository owner privately through the contact method listed on their GitHub profile. Include reproduction steps and impact, but never include real credentials or unrelated personal data.

## Deployment guidance

- Keep Home Assistant, ESPHome, and device firmware updated.
- Use a trusted Wi-Fi network and isolate IoT devices where practical.
- Replace the sample fallback access-point password before deployment.
- Consider enabling ESPHome native API encryption and appropriate OTA authentication; keep keys only in `secrets.yaml`.
- Do not expose the ESPHome native API, fallback access point, or Home Assistant directly to the public internet.
- Sanitize logs before sharing them.

The default firmware uses an unencrypted ESPHome native API on the local network for ease of initial setup. Users with an untrusted LAN should enable API encryption before deployment; doing so requires recompilation and consistent Home Assistant pairing.

