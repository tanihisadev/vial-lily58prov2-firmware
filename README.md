# Lily58 Vial Firmware.

---

## Hardware

| Component       | Detail                                                                  |
| -----------------| -------------------------------------------------------------------------|
| Keyboard        | [Lily58 PRO V2](https://khor.store/products/lily58pro-2-0) (Khor Store) |
| MCU             | RP2040 (Raspberry Pi Pico)                                              |
| Split transport | Full-duplex serial — TX: GP0, RX: GP1                                   |
| Display         | SSD1306 OLED (128×32, 270° rotation)                                    |
| RGB             | WS2812 on GP11 (PIO1)                                                   |
| Matrix          | 5 rows × 6 cols per side, COL2ROW                                       |

---

## Flashing

1. Hold the **BOOT** button on the RP2040, then plug in USB — a `RPI-RP2` drive will appear.
2. Drag and drop the `.uf2` file onto the drive. The board reboots automatically.
3. Repeat for the **right half**.

---

## Enabled QMK Features

| Feature | State | Notes |
|---------|-------|-------|
| Vial | ✅ | Full runtime remapping via Vial GUI |
| Extra keys | ✅ | Media / system keys |
| WPM | ✅ | |
| LTO | ✅ | Link-time optimisation — smaller firmware |
| OLED | ✅ | |
| Tap Dance | ✅ | |
| Combos | ✅ | |
| Mouse keys | ✅ | |
| Vial RGB | ✅ | |

---

## Vial GUI

Download the [Vial app](https://get.vial.today/) and plug in the keyboard — it will be detected automatically. You can remap any key, create macros, and adjust tap-term settings without reflashing.
Alternatively, you can visit [Vial](https://vial.rocks) to edit your keymap in the browser.

---
