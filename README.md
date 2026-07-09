# Scan Troubleshooter

A single-page web app for visualizing measurement scans — the **raw** profile against
the **filtered** one, plus their deviation. No build step, no dependencies: just
`index.html`.

**Live app:** https://jbcbro.github.io/scan_troubleshooter/

## Usage

Open the page and drag & drop (or pick) a scan file. Two formats are supported:

- **CSV** — `;`, `,` or tab separated, with `X-Pos`, `Z-Raw`, `Z-Filtered` columns
  (extra columns, metadata footers, and zero-padding rows are ignored).
  In the instrument export the `X-Pos` column is the *filtered* grid, while
  `Z-Raw` is a positional stream sampled every 0.1 mm from the scan start —
  the "CSV raw X" control sets the step, or switches to row-aligned parsing
  for CSVs where all columns share the `X-Pos` grid.
- **JSON** — either `{ "arRawX": [], "arRawZ": [], "arFiltX": [], "arFiltZ": [] }`
  or an array of row objects with `X-Pos` / `Z-Raw` / `Z-Filtered` fields

You can also load a file by URL parameter: `index.html?file=<url>` (same-origin
or CORS-enabled, e.g. a raw gist).

### Charts

- **Profile** — raw vs filtered Z over X position, with crosshair readout
- **Deviation** — raw − filtered on the raw X grid (filtered is interpolated when
  the two series have different grids)
- Scroll to zoom, drag to pan, double-click to reset; both charts stay in sync
- Legend toggles a series; **Table view** lists every point
- Light and dark theme follow the system setting

## Development

Serve the folder with any static server and open it:

```sh
python3 -m http.server 8000
# http://localhost:8000
```
