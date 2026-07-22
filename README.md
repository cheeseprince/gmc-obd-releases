# GMC OBD Display — OTA Releases

Firmware release channel for an in-cab OBD-II stat display on a **2025 GMC Sierra 1500
3.0L Duramax** (LZ0, Global B). Binaries only — source is maintained privately.

The display shows live engine, transmission, aftertreatment and economy data pulled over
Bluetooth LE from a generic ELM327 adapter, including enhanced GM Mode-22 parameters
(transmission temperature, EGT, DPF differential pressure, fuel rail pressure, DEF level)
that generic scan tools do not expose.

## Hardware

| Part | Detail |
| :--- | :--- |
| **Display / MCU** | Elecrow **CrowPanel Advance 3.5"** — ESP32-S3-WROOM-1-N16R8 (16 MB flash, 8 MB PSRAM), 480×320 IPS |
| **Input** | Arduino **Modulino** rotary encoder (I²C) — rotate to move, press to zoom, long-press for settings |
| **Clock** | **PCF8563** real-time clock @ 0x51 + coin cell — timestamps the SD logs and drives automatic day/night theming |
| **Storage** | **microSD** card (FAT32) — 1 Hz CSV drive logs |
| **OBD adapter** | **Vgate vLinker MS** in BLE mode (classic-CAN ELM327) |
| **Power** | Truck USB (switched 5 V) → board USB-C |

The capacitive touch panel is present but unused; all navigation is via the encoder.

## Screenshots

Pixel-exact renders of the real firmware UI are in [`screenshots/`](screenshots/) —
all seven gauge pages, the boot splash, and the settings menu.

## How updates work

Devices fetch `manifest.txt` over HTTPS (GitHub Pages), compare the release git hash
against their running build, and self-update via ESP32 dual-slot OTA. The downloaded
image is **SHA-256 verified before the slot is activated**; any failure leaves the running
slot untouched.

Manifest format — one line per release:

```
<env> <git-hash> <sha256> <size-bytes> <filename>
```

Published by `publish_ota.sh` from the build machine. **Do not edit by hand.**
