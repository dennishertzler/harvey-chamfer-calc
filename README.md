# Harvey Adjustable Chamfer Cutter Calculator

A single-page web tool for **Harvey Tool** adjustable chamfer cutters **#81250** and **#81260**. Pick a chamfer angle (10°–80°) and get **min/max cutter diameter**, **radial depth of cut (DOC)**, and **axial DOC** in inches, plus a reference diagram and a curve chart across the full angle range.

This repository is a **machining reference calculator**, not an official Harvey Tool product. Always confirm critical dimensions against Harvey Tool catalogs, drawings, and your CAM simulation before cutting.

## Quick start

There is no build step or server required.

1. Clone or download this folder.
2. Open `harvey-chamfer-calc.html` in a modern desktop or mobile browser (double-click the file, or use *File → Open*).

The page loads fonts from Google Fonts; an internet connection is needed for typography on first load.

## What you can do

- **Set chamfer angle** with the slider (0.5° steps) or the number field (0.1° steps), from **10° to 80°**.
- **See four results** (all in **inches**):
  - **Min diameter** and **max diameter** — effective cutter diameter limits at that angle (from tabulated data, smoothed).
  - **Radial DOC** and **axial DOC** — depth components resolved from the chamfer angle.
- **Reference SVG** — illustrates max/min diameter, radial DOC, axial DOC, and angle θ relative to the tool and workpiece.
- **Curve preview** — canvas chart of all four quantities from 10° to 80°, with the current angle highlighted and table points marked.

## How the numbers are computed

The implementation in `harvey-chamfer-calc.html` uses two ideas:

1. **Min / max diameter** — Values come from an internal table (one row per 5° from 10° to 80°). Between those angles, **natural cubic splines** interpolate smoothly so the UI can use any angle in range.

2. **Radial and axial DOC** — These follow a **sine/cosine relationship** with chamfer angle θ (in degrees): radial DOC is *K*·cos(θ) and axial DOC is *K*·sin(θ), with scale *K* fitted to the reference table. At 45°, radial and axial DOC are equal.

If the angle is outside 10°–80°, the calculator shows an error message instead of extrapolating.

## Files

| File | Purpose |
|------|---------|
| `harvey-chamfer-calc.html` | Full UI, styles, diagram, chart, and logic in one file |

## Browser support

Any recent browser with HTML5 canvas and ES2015+ JavaScript (Chrome, Firefox, Safari, Edge) should work.

## License / attribution

Harvey Tool is a trademark of its owner. This project is an independent calculator for shop use; it is not affiliated with or endorsed by Harvey Tool unless stated otherwise by the repository owner.
