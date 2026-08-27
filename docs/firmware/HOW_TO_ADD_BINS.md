# How to add firmware binaries (ESP32-C3 only)

The installer (`manifest.json`) expects:

```text
docs/firmware/esp32c3/
  bootloader.bin
  partitions.bin
  boot_app0.bin
  firmware.bin
```

## From Arduino IDE (ESP32 core 3.x)

1. Board: **ESP32C3 Dev Module**
2. Partition scheme: **Huge APP (3MB No OTA)** (or matching your build)
3. **CDC On Boot: Enabled** if you use native USB
4. Sketch → **Export compiled Binary** (or note paths after Upload)

Typical locations (macOS):

```text
~/Library/Caches/arduino/sketches/<ID>/
  GoProBridgeBle.ino.bin              → firmware.bin
  GoProBridgeBle.ino.bootloader.bin   → bootloader.bin
  GoProBridgeBle.ino.partitions.bin → partitions.bin
```

`boot_app0.bin` from the ESP32 package, e.g.:

```text
…/packages/esp32/hardware/esp32/<version>/tools/partitions/boot_app0.bin
```

Copy into `docs/firmware/esp32c3/` with the names above.

## Offsets (in manifest.json)

| Part            | Offset (dec) | Hex     |
|-----------------|-------------|---------|
| bootloader.bin  | 0           | 0x0     |
| partitions.bin  | 32768       | 0x8000  |
| boot_app0.bin   | 57344       | 0xE000  |
| firmware.bin    | 65536       | 0x10000 |

If your build log shows different addresses, adjust `docs/manifest.json`.

## Alternative: single merged image

```json
{
  "chipFamily": "ESP32-C3",
  "parts": [
    { "path": "firmware/esp32c3/merged.bin", "offset": 0 }
  ]
}
```
