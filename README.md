# Architecture Playground — how to manage your buildings

The site reads your buildings from **plans.csv** automatically. You never edit code.
To add a building you only ever do two things:

1. Put a floor-plan **SVG** in the `plans/` folder.
2. Add one **row** to your spreadsheet, save it as `plans.csv`.

Refresh the site and the new building is swimming.

---

## Folder layout

```
your-site/
├── index.html              ← the program (you don't open this)
├── plans.csv               ← your list of buildings (edit in Excel / Google Sheets)
└── plans/                  ← your floor-plan SVGs
    ├── villa-savoye.svg
    ├── glass-pavilion.svg
    └── national-stadium.svg
```

If `plans.csv` is missing, the site quietly shows a set of demo plans instead, so it
never looks broken.

---

## The spreadsheet (plans.csv)

Open `plans.csv` in Excel or Google Sheets. One row = one building.

| Column   | What to put                                              | Example          |
|----------|----------------------------------------------------------|------------------|
| name     | Building name (this is what "Call out" searches)         | Villa Savoye     |
| file     | The SVG file name, exactly as saved in `plans/`          | villa-savoye.svg |
| width_m  | How many real metres the drawing spans LEFT→RIGHT        | 19.6             |
| height_m | How many real metres the drawing spans TOP→BOTTOM        | 21.5             |
| function | What it is                                               | House            |
| architect| Credit                                                   | Le Corbusier     |
| year     | Completed                                                | 1931             |
| url      | Link for "Read more" (leave blank for none)              | https://...      |
| area_m2  | Optional. Gross floor area. Leave blank to use footprint | (blank)          |

**`width_m` and `height_m` are the important ones** — they're what make every plan
share one true scale. They are real-world **metres**, not pixels.

> If your drawing, from its left edge to its right edge, covers a building that's
> 40 m wide in real life, then `width_m = 40`. Same idea top-to-bottom for `height_m`.

Finding the metres if you don't know them: read them off the drawing's scale bar or
dimensions, or use Google Maps → right-click → "Measure distance" across the footprint.

The size class (S / M / L / XL) is worked out automatically from `width_m × height_m`.

If a value contains a comma, wrap that one value in "quotes", e.g. `"Smith, Jones & Co"`.

---

## Preparing a floor-plan SVG (this matters more than anything)

SVG is the chosen format because it stays perfectly sharp at every zoom level and in
the focus view, and the files are tiny. To make one work in the aquarium:

- **Lines must be white (or light).** Floor plans exported from CAD are usually black
  on white — black lines are invisible on the black background. Recolour the strokes
  to white in a vector editor (Illustrator / Inkscape / Figma).
- **No background.** Delete any white sheet/rectangle behind the drawing so the
  background is transparent — only the lines should remain.
- **Keep a `viewBox`.** Most exports include one; it lets the drawing scale cleanly.
- **Crop tight** so the drawing's edges line up with a clean real-world rectangle.
  That's what makes `width_m` / `height_m` honest, and don't distort the proportions.
- **Orient it the way you want to read it.** That same orientation is what appears
  upright when you double-click a plan to focus it.
- **Name files simply**, lowercase, no spaces: `villa-savoye.svg`.

Keep your original drawings (CAD / PDF) as your private archive; the `plans/` folder
holds the cleaned-up web copies.

---

## Adding more buildings after the site is live

1. Save the new SVG into the `plans/` folder.
2. Add a row in your spreadsheet and save / export it as `plans.csv`.
3. Upload both to GitHub (drag-and-drop into the repo on the GitHub website — no
   command line needed).
4. Refresh the site. Done.

The spreadsheet is your master copy; the repo is the published copy.

---

## Testing it

The "read plans.csv automatically" part works on a real web address (GitHub Pages).
If you double-click `index.html` to open it straight from your computer, the browser
blocks it from reading `plans.csv`, so you'll just see the demo plans — that's normal,
not a bug. To see your real plans, view the site through GitHub Pages.

---

## Handing the data to Claude

If you'd rather hand it off: keep the spreadsheet, then share the `plans.csv` and the
SVG files. The columns above are all that's needed.
