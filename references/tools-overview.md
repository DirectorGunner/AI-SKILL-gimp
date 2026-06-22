# Tools Overview

GIMP's tools live in the Toolbox and are driven by a companion options panel. This file is a map of the tool system and a quick-reference catalog of tool names and default shortcuts; deep usage lives in the sibling files.

**When this applies:** Read this when you need to identify which tool to invoke, its exact name, its default shortcut, or which category and menu path it sits under, before drilling into a task-specific file.

## The Toolbox and Tool Options

The Toolbox holds the clickable tool icons and also surfaces the foreground/background color area, the active brush, pattern, and gradient. Docked beneath it is the **Tool Options** dialog, which shows the settings for whichever tool is selected. Keep both visible, since a tool's behavior depends on how its options are set. Two color shortcuts live in the Toolbox color area: **D** resets the foreground and background to black and white, and **X** swaps them.

```text
Pick a tool (click icon or press its shortcut) → adjust it in Tool Options → act on the canvas
Example: press  N  for Pencil, set its options, then draw.
```

## Tool categories

The manual groups tools into five categories: **Selection tools**, **Paint tools**, **Transform tools**, **Color tools**, and **Other tools**. Color tools are covered in `colors-and-adjustments.md`; the rest are cataloged below. Shortcuts marked TODO were not confirmed on the fetched pages — assign them via **Edit > Keyboard Shortcuts**.

## Selection tools (Tools > Selection Tools)

- **Rectangle Select** `R` · **Ellipse Select** `E` · **Free Select** (the Lasso) `F`
- **Fuzzy Select** (Magic wand) `U` · **By Color Select** `Shift+O` · **Foreground Select** (no default) · **Scissors Select** (TODO)

See `selections.md` for behavior and modes.

## Paint tools (Tools > Paint Tools)

- **Pencil** `N` · **Paintbrush** `P` · **Airbrush** `A` · **Ink** `K` · **MyPaint Brush** `Y`
- **Bucket Fill** `Shift+B` · **Gradient** `G` · **Eraser** `Shift+E`
- **Clone** `C` · **Heal** `H` · **Smudge** `S` · **Dodge/Burn** `Shift+D`

## Transform tools (Tools > Transform Tools)

- **Align and Distribute** `Q` · **Move** `M` · **Crop** `Shift+C`
- **Rotate** `Shift+R` · **Scale** `Shift+S` · **Shear** `Shift+H` · **Perspective** `Shift+P` · **Flip** `Shift+F`
- **Unified Transform**, **Handle Transform**, **Cage Transform**, **Warp Transform**, **3D Transform** (shortcuts TODO)

## Other tools

- **Paths** `B` (**Tools > Paths**) — see `paths.md`
- **Text** `T` (**Tools > Text**) — adds text in a new layer, editable on canvas
- **Color Picker** `O` · **Measure** (no default) · **Zoom** (no default) · **GEGL Operation** (TODO)

## Do / Don't

- **Do** use the exact tool name and category as written (e.g. "By Color Select", "Dodge/Burn").
- **Do** open **Tool Options** alongside the Toolbox before acting; options change outcomes.
- **Don't** assume a shortcut where one is marked TODO or "no default" — assign it via **Edit > Keyboard Shortcuts**.
- **Don't** document per-tool options here; route to the depth files.

## Related

`interface-and-workflow.md` · `selections.md` · `paths.md` · `colors-and-adjustments.md` · `layers-and-modes.md`
