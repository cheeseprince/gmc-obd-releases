# GMC OBD Display — OTA Releases

Firmware release channel for the two in-cab OBD display units (2025 GMC Sierra
1500 3.0L Duramax): the CrowPanel 3.5" dash unit and the Waveshare 1.8" round
knob. Binaries only — source is maintained privately.

Devices fetch `manifest.json` over HTTPS (GitHub Pages), compare the release
git hash against their running build, and self-update via ESP32 dual-slot OTA
with SHA-256 verification.

Published by `publish_ota.sh` from the build machine. Do not edit by hand.
