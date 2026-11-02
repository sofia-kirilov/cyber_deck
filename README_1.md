# Shell Trinket Compact

A 3D-printable seashell compact for tiny trinkets, with a round touchscreen built into the lid. It snaps shut, charges over USB-C, and has a 22 mm deep tray for rings and small things.

![Renders: closed, lid top, open, base](images/render.png)

## Why I made this

I wanted something between a makeup compact, a jewelry box and a tiny cyberdeck. It should look like a decorative object first, but open up to a working screen. I started from my own sketch of a ribbed shell with a ruffled bow, sparkles and my signature, then modeled it parametrically so I could keep changing proportions and details.

<img src="images/sketch.png" width="360" alt="Original sketch">

## Features

- **Shell:** round scallop shell with 9 ribs, fine engraved lines, scalloped edges, and pearl beading on both rims
- **Details:** layered relief ribbon bow (4 loops, knot, wavy notched tails), raised stars, crescent moons, a starfish and a pearl, plus my signature engraved in script
- **Screen:** 1.28" round capacitive touchscreen (240×240, ESP32-S3 with Wi-Fi/BLE) behind a bezel plate with a ring of pearl dimples
- **Power:** LiPo battery behind the screen, charged through a USB-C port on the right edge of the lid
- **Closing:** snap latch at the front (no magnets), snap-in hinge (no pin or screws)
- **Storage:** open trinket tray in the base, about 22 mm deep
- **Size:** about 82 × 90 × 46 mm closed

<img src="images/bow.png" width="600" alt="Relief bow detail">

## Repository layout

```
shell-compact/
├── README.md
├── BOM.md                  parts list with prices and links
├── JOURNAL.md              design journal
├── cad/
│   ├── shell_trinket_compact.py     parametric CadQuery source (generates everything)
│   ├── lid.step  base.step  bezel_plate.step
│   ├── lid_no_signature.step        backup lid without the engraved signature
│   ├── shell_compact_assembly.step  all parts in place, with dummy screen and battery
│   └── fonts/GreatVibes-Regular.ttf (SIL Open Font License)
├── print/
│   ├── lid.stl   lid.3mf
│   ├── base.stl  base.3mf
│   └── bezel_plate.stl  bezel_plate.3mf
└── images/
```

## Bill of materials

Full list with links and prices: **[BOM.md](BOM.md)**. Summary:

| Part | Qty | Approx. cost |
|---|---|---|
| Waveshare ESP32-S3-Touch-LCD-1.28 | 1 | $22 |
| 3.7 V LiPo, ≤ 30 × 25 × 4 mm, 1.25 mm plug | 1 | $6–9 |
| Short USB-C male-to-female extension | 1 | $5–8 |
| M2 × 6 screws | 4 | $6 (kit) |
| PETG filament | ~60 g | $2 |
| **Total** | | **≈ $41–47** |

## Printing

All files in `print/` are already oriented and repaired (watertight). Use the `.3mf` files for Bambu Studio, PrusaSlicer or Orca, or the `.stl` files for anything else.

| Part | Orientation | Supports | Approx. time* |
|---|---|---|---|
| `base` | flat on its bottom | none | ~3 h |
| `lid` | seam side down, dome up | none | ~3 h |
| `bezel_plate` | flat, screen side down | none | ~40 min |

*Rough estimates at 0.12 mm layers. Check your slicer's numbers.

**Settings:** PETG (the latch and hinge need to flex; PLA works but cracks more easily), 0.4 mm nozzle, 0.12 mm layers so the 2 mm pearls come out round, 3 walls, 15% infill.

## Assembly

1. **Hinge:** hold the lid upright behind the base and press its hinge pins into the slotted base knuckles until they click.
2. **Screen:** put the display face-down into the ring on the bezel plate.
3. **Battery:** plug the LiPo into the board's battery connector (check polarity first, see [BOM.md](BOM.md)) and lay it behind the display.
4. **USB-C:** plug the extension into the board and seat its female end in the holder on the right side of the lid, so the port lines up with the opening.
5. **Close up:** screw the bezel plate into the lid with the four M2 screws.

## Software

The board runs Arduino or ESP-IDF. Waveshare's [wiki](https://www.waveshare.com/wiki/ESP32-S3-Touch-LCD-1.28) has the pinout, touch driver (CST816S) and LVGL examples. Planned UI: clock, a small "what's inside" trinket list, and an animated shell screensaver.

## Modifying the design

```bash
pip install cadquery
cd cad
python3 shell_trinket_compact.py     # writes STEP + STL to cad/out/ (about 10 min)
```

The main parameters are at the top of the script, including board size (`BOARD_D`, `BOARD_T`), USB-C holder size (`USB_BODY`), number of ribs, dome heights, pearl spacing, and signature text and position.
