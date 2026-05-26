# Lily58 Pro (V2) Vial Firmware

> This Firmware is based off the base firmware provided by [Khor](https://github.com/moltenkhor) for his revision of the Lily58 Pro V2.

## Hardware

| Component       | Detail                                                                  |
| --------------- | ----------------------------------------------------------------------- |
| Keyboard        | [Lily58 PRO V2](https://khor.store/products/lily58pro-2-0) (Khor Store) |
| MCU             | RP2040                                             |
| Split transport | Full-duplex serial — TX: GP0, RX: GP1                                   |
| Display         | SSD1306 OLED (128×32) — master 0°, slave 270°                           |
| RGB             | WS2812 on GP11 (PIO1)                                                   |
| Matrix          | 5 rows × 6 cols per side, COL2ROW                                       |

---
 
## Building
 
### Prerequisites
 
**Arch / CachyOS:**
```bash
sudo pacman -S arm-none-eabi-gcc arm-none-eabi-newlib python python-pip git
pip install qmk --break-system-packages
```
 
### Setup
 
Clone the vial-qmk fork — **do not use mainline QMK**, it does not include Vial support:
 
```bash
git clone https://github.com/vial-kb/vial-qmk.git --recurse-submodules ~/vial-qmk
cd ~/vial-qmk
pip install -r requirements.txt --break-system-packages
```
 
Copy the keyboard definition into the vial-qmk keyboards directory:
 
```bash
cp -r /path/to/lily58prov2 ~/vial-qmk/keyboards/lily58prov2
```
 
### Compile
 
```bash
cd ~/vial-qmk
qmk compile -kb lily58prov2 -km vial
```
 
The output file will be at `~/vial-qmk/lily58prov2_vial.uf2`.
 
---

## Flashing

1. Hold the **BOOT** button on the RP2040, then plug in USB — a `RPI-RP2` drive will appear.
2. Drag and drop the `.uf2` file onto the drive. The board reboots automatically.
3. Repeat for the **right half**.

---

## Known Hardware Issue

The Lily58 PRO V2 PCB has an issue with VBUS sense detection, which prevents reliable cold-boot handedness detection in firmware. A `SPLIT_WATCHDOG_ENABLE` workaround is in place — on cold boot the keyboard takes a few seconds to reset and establish the split link correctly. However, newer versions of this PCB will not have the same issue and thus this workaround will not be necessary.

---

## Enabled QMK Features

| Feature           | State | Notes                                          |
| ----------------- | ----- | ---------------------------------------------- |
| Vial              | ✅    | Full runtime remapping via Vial GUI             |
| Extra keys        | ✅    | Media / system keys                            |
| WPM               | ✅    | Synced to slave half for OLED display           |
| LTO               | ✅    | Link-time optimisation — smaller firmware       |
| OLED              | ✅    | Glitch logo (master), status display (slave)   |
| Tap Dance         | ✅    |                                                |
| Combos            | ✅    |                                                |
| Mouse keys        | ✅    |                                                |
| Vial RGB          | ✅    |                                                |
| Split watchdog    | ✅    | Cold boot handedness workaround                |

---

## Layer Naming Structure

| Layer | Name  | Access           | Purpose                          |
| ----- | ----- | ---------------- | -------------------------------- |
| 0     | BASE  | —                | QWERTY                           |
| 1     | NUM   | LT (Space hold)  | Numbers (right) + F-keys (left)  |
| 2     | NAV   | LT (Enter hold)  | Navigation + one-hand modifiers  |
| 3     | SYM   | MO (pinky)       | Symbols                          |
| 4     | MAUS  | TG from NUMFN    | Mouse movement                   |
| 5     | SYS   | —                | Reserved                         |

---

## Vial GUI

Download the [Vial app](https://get.vial.today/) or visit [vial.rocks](https://vial.rocks) to remap keys, configure tap dance, combos, and macros without reflashing.
