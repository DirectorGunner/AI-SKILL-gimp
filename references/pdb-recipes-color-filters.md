# PDB Recipes: Colors and Filters

Worked PDB calls for color/tone adjustments in GIMP 3.x, confirmed against the GIMP 3.0 API
(`Gimp.Drawable` methods). Script-Fu uses the hyphenated form; confirm parameter ranges and enum
values in **Help > Procedure Browser**.

**When this applies:** Read this when scripting brightness/contrast, levels, curves, desaturate,
threshold, or other tonal adjustments, or running a filter, via the PDB.

## Tone and color adjustments on a drawable

In 3.0 these operate on a drawable and are named `gimp-drawable-*` (the 2.10 short names like
`gimp-brightness-contrast` are gone):

```scheme
(gimp-drawable-brightness-contrast drawable brightness contrast)
(gimp-drawable-levels    drawable channel low-in high-in clamp-in gamma low-out high-out clamp-out)
(gimp-drawable-curves-explicit drawable channel num-values values)
(gimp-drawable-desaturate drawable desaturate-mode)   ; desaturate-mode is a DESATURATE-* constant
(gimp-drawable-threshold  drawable channel low high)
(gimp-drawable-invert     drawable linear)
```

Other confirmed methods: `gimp-drawable-curves-spline`, `gimp-drawable-equalize`,
`gimp-drawable-hue-saturation`, `gimp-drawable-color-balance`, `gimp-drawable-posterize`.

There is **no** `gimp-drawable-hue-chroma`: the **Colors > Hue Chroma** UI operation has no
same-named drawable procedure — locate its operation in the Procedure Browser.

TODO: exact parameter ranges and enum constants (channels, desaturate mode, the boolean for
`gimp-drawable-invert`) are not asserted here — read them from the Procedure Browser.

## Running a filter

Most filters are GEGL operations, exposed as `plug-in-*` procedures or run through GEGL; the manual
does not enumerate them. Find the specific filter procedure in **Help > Procedure Browser** (see
`filters.md` for the menu taxonomy).

## Python (GObject Introspection) equivalents

Typed methods on the drawable: `drawable.brightness_contrast(...)`, `drawable.levels(...)`,
`drawable.desaturate(...)`, `drawable.threshold(...)`.

## Do / Don't

- **Do** operate on the drawable from your image setup (see `pdb-recipes-images-layers.md`).
- **Do** confirm parameter ranges and enum constants in the Procedure Browser.
- **Don't** assume `gimp-drawable-hue-chroma` exists; it does not.
- **Don't** reuse the 2.10 name `gimp-brightness-contrast`; 3.0 uses `gimp-drawable-brightness-contrast`.

## Related

`pdb-recipes-images-layers.md` · `pdb-recipes-selections-paths.md` · `colors-and-adjustments.md` · `filters.md` · `pdb-reference.md`
