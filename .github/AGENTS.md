---
description: "Project house style and graphics rules for OpenEPaperLink tags"
---

# OpenEPaperLink Tag House Style

This repo renders tag graphics with `open_epaper_link.drawcustom`. Use this file as the single source of truth for visual rules and layout decisions.

## How to Generate Graphics

- Prefer `open_epaper_link.drawcustom` with a `payload` list of primitives.
- Target size: 400x300 (Solum M2). Keep all layouts within 0..399 and 0..299.
- Use a white background, black text, and a red accent bar for headers.
- Set `dither: 2`, `rotate: 0`, and `ttl: 300` unless a layout needs a different value.

### Minimal template (copy/paste)

```yaml
- action: open_epaper_link.drawcustom
  target:
    device_id: !input tag_device
  data:
    background: white
    rotate: 0
    dither: 2
    ttl: 300
    payload:
      - type: rectangle
        x_start: 0
        y_start: 0
        x_end: 399
        y_end: 299
        fill: white
        outline: white

      - type: rectangle
        x_start: 0
        y_start: 0
        x_end: 399
        y_end: 34
        fill: red
        outline: black

      - type: text
        value: "TITLE"
        x: 12
        y: 8
        font: "{{ font_file }}"
        size: 24
        color: white
```

## House Style Tokens

- Font default: use one of the bundled CC fonts below (do not use rbm.ttf).
- Accent color: `red` for headers and emphasis.
- Text color: `black`.
- Black text on red is not allowed; if text must sit on red, use white text or add a white outline.
- Line width: 2 for separators and frames.
- Margins: 12 to 20 px from edges for text blocks.
- Spacing: prefer whitespace over heavy grid lines (warm minimal).

## Layout Guidance (Warm Minimal)

- Use 1 primary header and 1 to 3 content blocks.
- Avoid dense grids unless the content truly needs it.
- Prefer a single accent bar plus light separators.
- Keep numeric values large and labels small.
- Favor left-aligned text with consistent baselines.

## Fonts (CC Licensed, Bundled)

These fonts are stored under `fonts/` with OFL licenses.

- `fonts/atkinson_hyperlegible/AtkinsonHyperlegible-Regular.ttf`
- `fonts/atkinson_hyperlegible/AtkinsonHyperlegible-Bold.ttf`
- `fonts/source_sans_3/SourceSans3-Regular.ttf`
- `fonts/source_sans_3/SourceSans3-Bold.ttf`

Use the file path directly in the `font` field.

## When Adding New Screens

- Add a `font_file` input with a safe default.
- Keep the palette consistent with the house style unless a screen is special purpose.
- Use `target` selectors so users can choose a device, entity, or area.
