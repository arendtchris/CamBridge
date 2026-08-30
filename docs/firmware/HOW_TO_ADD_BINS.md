# How to add firmware binaries (ESP32-C3 only)

The installer (`manifest.json`) expects the **Arduino export names** (no renaming):

```text
docs/firmware/esp32c3/
  GoProBridgeBle.ino.bootloader.bin
  GoProBridgeBle.ino.partitions.bin
  boot_app0.bin
  GoProBridgeBle.ino.bin
```

## From Arduino IDE (ESP32 core 3.x)

1. Board: **ESP32C3 Dev Module**
2. Partition scheme: **Huge APP (3MB No OTA)** (or matching your build)
3. **CDC On Boot: Enabled** if you use native USB
4. Sketch → **Export compiled Binary**

Copy the exported files **as-is** into `docs/firmware/esp32c3/`:

```text
GoProBridgeBle.ino.bin
GoProBridgeBle.ino.bootloader.bin
GoProBridgeBle.ino.partitions.bin
```

`boot_app0.bin` is not part of the sketch export. Take it once from the ESP32 package, e.g.:

```text
…/packages/esp32/hardware/esp32/<version>/tools/partitions/boot_app0.bin
```

## Offsets (in manifest.json)

| Part                                   | Offset (dec) | Hex     |
|----------------------------------------|-------------|---------|
| GoProBridgeBle.ino.bootloader.bin      | 0           | 0x0     |
| GoProBridgeBle.ino.partitions.bin      | 32768       | 0x8000  |
| boot_app0.bin                          | 57344       | 0xE000  |
| GoProBridgeBle.ino.bin                 | 65536       | 0x10000 |

If your build log shows different addresses, adjust `docs/manifest.json`.

## Alternative: single merged image

If you prefer one file only, export/use the merged image and set:

```json
{
  "chipFamily": "ESP32-C3",
  "parts": [
    { "path": "firmware/esp32c3/GoProBridgeBle.ino.merged.bin", "offset": 0 }
  ]
}
```
