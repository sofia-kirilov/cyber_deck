# Design Journal

**Total time logged: 11 h**

---

## Entry 1: The idea and first CAD (6 h) · 18 Oct 2026

So this was kind of my idea, I sketched it out before attempting to CAD anything. I like collecting little trinkets and was inspired by the influx of cyberdecks on my Instagram FYP to try making my own. I wanted to create a shell that could open and shut with some space for a display inside, as well as a little part for some of my trinkets. I sketched my ideas out in Sketchbook and settled on a design kinda similar to one of my blush compacts.

![My sketch](images/sketch.png)

My first version of the CAD wasn't too intense, I was just trying to figure out the shape of the shell. I wanted to make it a little thicker than what I originally did though, in order to fit all the electrical components I'm working on choosing.

Very wonky second try:

![Wonky second try](images/v2_rounder_attempt.png)

---

## Entry 2: Where it's at now (5 h) · 18 Oct 2026

I created a seashell trinket compact. Right now it's around 82×90×46 mm, but I have a very bad sense of space so I might adjust that before printing. It has a scallop shell with engraved lines, a ribbon bow, stars, a starfish and pearls, a signature, and a pearl rim. Inside will be a round touchscreen, a battery with USB-C charging, and a little tray for my trinkets.

![Current design](images/render.png)

---

## Posted a reel · 18 Oct 2026

my very tuff trinket idea

---

<details>
<summary><b>Build log: technical notes on every version and what broke</b></summary>

### Oct 17: Idea and first version (rectangular "cyberdeck" jewelry box)

I wanted to make a compact or jewelry box with a working display, something like a tiny cyberdeck, ideally with touch.

**v1 design:**
- Rectangular clamshell, 124 × 84 × 56 mm, built around the ESP32-2432S028R ("Cheap Yellow Display"): a 2.8" resistive touchscreen and ESP32 on one 86 × 50 mm board for about $15.
- Screen set into the top of the lid. A mirror recess on the inside of the lid, like a makeup compact.
- Ring slots and two trays in the base.
- Hinge pin made from 1.75 mm filament, magnet clasp at the front.

**Problems / decisions:**
- I couldn't find a drawing showing exactly where the LCD sits on the board, so the window position was a guess.
- Resistive touch needs a stylus or fingernail.
- It worked, but it looked like an electronics box, not a compact. I wanted something prettier.

![v1: rectangular cyberdeck box](images/v1_cyberdeck_box.png)

---

### Oct 17–18: Seashell v2 with a round display

I switched to a seashell shape with a round screen inside, where a compact's mirror would be.

- First display choice: Waveshare ESP32-S3-Touch-LCD-2.1 (75 mm round board, 480×480, capacitive touch, LiPo header).
- First outline was a pure fan, scallop rays spreading from the hinge. To fit a 75 mm board it had to be **174 mm wide**, way too big. Real scallops are almost round, so I changed the outline to a round body with "ears" at the hinge. That brought it to about 111 × 117 mm.
- Ribs were flat-bottomed grooves cut into a dome, plus a scalloped edge and a pin hinge on the ears.
- Checked collisions with the lid opened to 30°, 60°, 90° and 110°: no collisions.

---

### Oct 18: Trying to make it "rounder"

I wanted puffier, rounder ribs, closer to a real blush compact.

**What I tried:**
1. **Ellipsoid lobes** (one per rib) intersected with the dome. The valleys between ribs came out under 1 mm deep because the dome envelope flattened them. Not visible.
2. **Height-map surface:** a smooth B-spline surface computed from a formula (dome minus rounded valleys). It looked great on paper, but the CAD booleans became unreliable: intersections returned the wrong volume, then hung for 10+ minutes and ran out of memory.

![Rounder attempt: ribs too shallow to see](images/v2_rounder_attempt.png)

**Lesson:** sculpted free-form surfaces and solid booleans don't mix well. I went back to an exact dome with **stacked grooves** (3 widths and depths) to approximate a rounded valley profile. It's robust and fast.

---

### Oct 18: v3, rebuilt from my sketch

I drew the version I actually wanted (`images/sketch.png`): a round ribbed shell, a ruffled bow at the top, sparkles, my signature on the right, and a layered scalloped rim. I also set real requirements:
- About blush-compact width and length (~8 cm), roughly double the thickness
- Pieces that click together; opens and closes with a snap
- Charging
- Deep enough for small trinkets

**Changes:**
- **Smaller display:** the 75 mm board doesn't fit an 8 cm compact, so I switched to the Waveshare ESP32-S3-Touch-LCD-1.28 (32.4 mm round screen). It has the same features: capacitive touch, ESP32-S3, LiPo charging.
- **Size:** 82 × 90 × ~46 mm.
- **Snap latch:** a flexible tab on the base with a bump that clicks into a groove in the lid. It replaced the magnets.
- **Snap hinge:** pins on the lid's middle knuckle press into slotted sockets in the base. No filament pin needed.
- **Charging:** LiPo behind the screen, and a USB-C extension seated in a holder so the port shows on the right edge.
- **Tray:** 22 mm deep in the base.
- **Signature:** engraved "Sofia Kirilov" in Great Vibes script.

**Problems:**
- Engraving the script text into the curved shell used **over 6 GB of RAM** and crashed. Fix: split the text into 3–6 chunks and cut each one with a flat floor set just below the local shell height. That took about 40 s and under 1 GB.
- The collision check found two fit issues. The lid ceiling hit the battery corners, so I raised the dome 2 mm. The latch tab grazed the thumb lip by 0.2 mm, so I shortened it.

---

### Oct 18: Flowy ribbon bow

The first bow was made of stretched ellipsoid blobs and looked lumpy. I rebuilt it as an actual ribbon: an elliptical cross-section swept along 3D spline paths.
- Two teardrop loops, a wrapped knot, and two wavy tails ending in V-notches.
- The tails follow the shell's surface normal, so they lie flat on the curve.

**Bug:** at first the loop ribbons lay flat in their own plane, so the tight tip of each loop folded into itself and the union failed. Standing the ribbon on edge, with its face around the inside of the loop like real ribbon, fixed it.

---

### Oct 18: More detail

- Two fine engraved lines along each rib, skipped on the lobe that carries the signature so it stays readable
- Pearl beading: about 80 pearls on the lid rim and a row around the base band
- Four-loop bow (two big, two small)
- Embossed starfish and a raised pearl among the stars and moons

**Bug:** the pearl union on the base band failed (invalid solid). A fuzzy boolean with 0.01 mm tolerance fixed it.

---

### Oct 18 (evening): Making it open in Onshape

The STEP file uploaded to Onshape but never translated. It just showed a grey "STEP file" card. Debugging, step by step:

1. **48 MB assembly:** I split it into one STEP per part.
2. **Re-imported my own files and found the real bug:** the dome, built as a stretched sphere, came back from STEP with **zero volume**. I replaced it with exact spherical caps sized to the same height and edge drop. Those round-trip perfectly.
3. **Inside-out solid:** after the reorder, the lid body had negative volume. I added an orientation fix (`OrientClosedSolid`) to the cleanup step.
4. **Posts and bosses exporting as separate bodies:** they only touched the inner wall. I extended them 0.6 mm into the wall so they fuse.
5. **Decoration columns:** after reordering the build, the stars ran as solid columns through the inside of the lid. I limited them to a thin skin layer.
6. **Bisecting in Onshape:** I uploaded three test lids (body → + stars and pearls → + bow). The base, plate and first two tests loaded. **The bow broke it.**
7. Rebuilt the ribbons as **lofts** through cross-sections instead of sweeps. Onshape still failed.
8. **Final fix:** the bow is now **layered raised relief** that follows the shell, built the same way as the stars, which already worked. Layers: tails 1.0 mm, big loops 1.6 mm, small loops 2.1 mm, knot 2.7 mm with wrap creases. It's no longer free-standing, but it still has depth and now prints with **no supports**.

**Lesson:** verify every export by re-importing it, and when an external tool fails, bisect with test files instead of guessing.

---

### Nov 1: Repo cleanup

- Wrote README, BOM and this journal
- Added `print/` with STL and 3MF files
- Repaired the lid and plate meshes, which had tiny gaps from tessellation. All three are now watertight, and the repaired volumes match the CAD within 0.1%.

### Next

- [ ] Confirm `lid.step` loads in Onshape
- [ ] Buy parts, measure the real board (`BOARD_D`, `BOARD_T` are estimates)
- [ ] Test print the latch and hinge first, since they're the riskiest parts
- [ ] Firmware: clock, trinket list, shell animation

</details>
