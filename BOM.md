# Bill of Materials

Prices are approximate (USD, October 2026) and don't include shipping or tax.

## Electronics

| # | Part | Qty | Unit price | Link | Notes |
|---|---|---|---|---|---|
| 1 | Waveshare ESP32-S3-Touch-LCD-1.28 | 1 | $21.99 | [Waveshare](https://www.waveshare.com/product/esp32-s3-touch-lcd-1.28.htm) · [Amazon](https://www.amazon.com/Waveshare-ESP32-S3-Development-Accelerometer-Gyroscope/dp/B0CM68M8LR) | Get the **Touch** version. 1.28" round 240×240 IPS, CST816S capacitive touch, ESP32-S3, IMU, LiPo charging, USB-C, MX1.25 2-pin battery header. |
| 2 | 3.7 V LiPo, 402030 (200 mAh, 30 × 20 × 4 mm) | 1 | ~$6 + shipping | [eBay](https://www.ebay.com/itm/184958200210) | Pick the **1.25 mm** connector option. Anything up to 30 × 25 × 4 mm fits. **Check polarity** against the board's +/− marks before plugging in; many 1.25 mm plugs come wired reversed. |
| 3 | USB-C male-to-female extension, 10–20 cm | 1 | $5–8 | Search: *"USB-C male to female extension short slim"* | Female end must be **≤ 12.4 × 6.9 mm** to fit the holder. Panel-mount versions with screw ears are too big. |

## Hardware

| # | Part | Qty | Unit price | Link | Notes |
|---|---|---|---|---|---|
| 4 | M2 × 6 mm socket head screw | 4 | ~$6 for a kit | Search: *"M2 socket head screw assortment"* | Holds the bezel plate to the lid. A kit leaves spares. |

No magnets, hinge pin or glue needed. The hinge and latch are printed snap-fits.

## Printed parts

| # | File | Qty | Material | Approx. filament |
|---|---|---|---|---|
| 5 | `print/lid.3mf` / `.stl` | 1 | PETG | ≤ 26 g |
| 6 | `print/base.3mf` / `.stl` | 1 | PETG | ≤ 29 g |
| 7 | `print/bezel_plate.3mf` / `.stl` | 1 | PETG | ≤ 9 g |

Upper bounds are for a solid part; your slicer's estimate with 15% infill will be lower. PETG costs about $20/kg, so the whole thing is under $1.50 of filament. Silk or pearl colors suit the shell look.

## Cost summary

| Item | Cost |
|---|---|
| Display board | $22 |
| LiPo battery | $6–9 |
| USB-C extension | $5–8 |
| Screws | $6 |
| Filament | ~$2 |
| **Total** | **≈ $41–47** |

## Tools

- 3D printer (build plate at least 90 × 90 mm)
- 1.5 mm hex key for M2 screws
- Tweezers, if the battery plug needs re-pinning for polarity
- Calipers, to measure the board before printing the lid
