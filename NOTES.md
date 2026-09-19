# How these cards are built

Every sheet is a standalone SVG in `assets/`. Nothing is fetched at render
time: Bebas Neue, Courier Prime and Kalam are subset to only the glyphs each
card uses and embedded as base64 WOFF2, so the type is identical to
hoodgail.me even though GitHub loads these through its image proxy.

## Design tokens

| token   | value     | role                          |
|---------|-----------|-------------------------------|
| paper   | `#E7E1D1` | manila stock                  |
| paperHi | `#F4F0E6` | fold highlight                |
| ink     | `#15120D` | press black                   |
| ink2    | `#4A443A` | second pass                   |
| soft    | `#8A8272` | faded impression              |
| stamp   | `#C1362B` | rubber-stamp red              |
| pen     | `#2A4B9B` | ballpoint blue, marginalia    |

Bebas Neue sets display and figures, Courier Prime carries every piece of
data, and Kalam appears only in blue as handwriting in the margin.

## Motion

Each sheet gets one orchestrated moment and at most one thing that loops:

- masthead: rules draw, name drops in, the stamp lands, then a tech ticker runs
- work history: the receipt prints top to bottom
- arsenal: checkboxes tick down the list
- tickets: a red LIVE dot breathes
- engine: the wireframe mark turns on its axis
- get in touch: scissors travel the tear line

Every card answers `prefers-reduced-motion: reduce`, and the resting state is
the finished state, so a renderer that ignores CSS still shows a complete card.

## Regenerating

```
pip install fonttools brotli
python build.py
```

Sizes are computed from real font metrics rather than guessed, so changing a
string re-fits the layout instead of overflowing it.
