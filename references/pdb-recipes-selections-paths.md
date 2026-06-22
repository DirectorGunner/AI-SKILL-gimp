# PDB Recipes: Selections and Paths

Worked PDB calls for selections and paths in GIMP 3.x, using procedure names confirmed against the GIMP 3.0 API. Script-Fu uses the hyphenated form of each procedure; confirm exact parameter order and types in **Help > Procedure Browser**.

**When this applies:** Read this when scripting selections (make, modify, save) or converting a path to a selection while driving GIMP.

## Geometric selections

Selection-by-shape procedures live on the image; the argument after the image is the channel operation (a `GimpChannelOps` value such as `CHANNEL-OP-REPLACE`).

```scheme
(gimp-image-select-rectangle image CHANNEL-OP-REPLACE x y width height)
(gimp-image-select-ellipse   image CHANNEL-OP-REPLACE x y width height)
```

Other shape procedures: `gimp-image-select-round-rectangle`, `gimp-image-select-polygon`,
`gimp-image-select-color`, `gimp-image-select-contiguous-color`, `gimp-image-select-item`.

## Modify the current selection

```scheme
(gimp-selection-feather image radius)   ; soften the edge
(gimp-selection-grow    image steps)
(gimp-selection-shrink  image steps)
(gimp-selection-border  image radius)
```

Also `gimp-selection-sharpen`, `gimp-selection-invert`, `gimp-selection-all`, `gimp-selection-none`,
`gimp-selection-float`, `gimp-selection-bounds`, `gimp-selection-is-empty`.

## Save a selection to a channel

`gimp-selection-save` returns a new channel holding the current selection.

```scheme
(let* ((chan (car (gimp-selection-save image))))
  chan)   ; reuse or reload this channel later
```

## Selection from a path or item

In 3.0 paths are the `Gimp.Path` class (ScriptFu's argument-type keyword is `SF-VECTORS`). Convert a
path, layer, or channel to a selection with `gimp-image-select-item`:

```scheme
(gimp-image-select-item image CHANNEL-OP-REPLACE item)
```

TODO: path creation, stroking, and SVG import/export procedure names are not all confirmed here —
look them up in **Help > Procedure Browser**.

## Python (GObject Introspection) equivalents

The same operations are typed methods: `image.select_rectangle(...)`, `Gimp.Selection.feather(image,
radius)`, `Gimp.Selection.invert(image)`, `Gimp.Selection.none(image)`.

## Do / Don't

- **Do** confirm each procedure's parameter order/types in **Help > Procedure Browser** before relying on it.
- **Do** take `(car …)` of a returning call (for example `gimp-selection-save`).
- **Don't** carry over 2.10 names blindly; these are the GIMP 3.0 names.
- **Don't** assume a channel-op constant; pass the documented `GimpChannelOps` value (e.g. `CHANNEL-OP-REPLACE`).

## Related

`pdb-recipes-images-layers.md` · `pdb-recipes-color-filters.md` · `selections.md` · `paths.md` · `pdb-reference.md`

## See also

- [Selections](selections.md)
