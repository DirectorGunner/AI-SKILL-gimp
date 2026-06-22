# GIMP 3.2 References — Index

Start here. Each file is a self-contained, original guide to one concern. Load only what the task
needs (progressive disclosure). Metadata: `topics.json` (topic → file + keywords). All content is
original prose; names, menu paths, shortcuts, procedure names, and numbers are preserved verbatim
from the GIMP 3.2 User Manual.

## Editing and image structure

| Component | One-line summary | Read this when… |
| --- | --- | --- |
| [interface-and-workflow.md](interface-and-workflow.md) | Windows, docks/dialogs, the menu map, zoom/undo, image Mode and Encoding | orienting in the UI or setting color mode/bit depth |
| [tools-overview.md](tools-overview.md) | The Toolbox, Tool Options, and a catalog of tools with default shortcuts | identifying which tool to use and its shortcut |
| [layers-and-modes.md](layers-and-modes.md) | The layer stack, Layers dialog, groups, alpha, and the blend-mode names | working with layers or picking a blend mode |
| [selections.md](selections.md) | Partial selections, tool modes, feathering, and the Select menu | constraining edits to part of an image |
| [masks-and-channels.md](masks-and-channels.md) | Layer masks (white/black direction), the Channels dialog, Quick Mask | masking a layer or saving/loading selections |
| [paths.md](paths.md) | Bézier paths, the Paths dialog, stroking, path↔selection, SVG | drawing vectors or converting paths and selections |
| [colors-and-adjustments.md](colors-and-adjustments.md) | The Colors menu operations and color management (assign vs convert) | naming a color op or handling ICC profiles |
| [filters.md](filters.md) | The Filters menu taxonomy and Repeat/Re-Show Last | locating a filter category or reapplying one |
| [file-formats-and-export.md](file-formats-and-export.md) | Open/import vs Save (.xcf) vs Export; PNG/JPEG options | opening, saving, or exporting images |

## Scripting, PDB, and automation

| Component | One-line summary | Read this when… |
| --- | --- | --- |
| [scripting-overview.md](scripting-overview.md) | Script-Fu vs Python-Fu, the consoles, install dirs, batch flags | automating GIMP or choosing a language |
| [pdb-reference.md](pdb-reference.md) | The Procedural Database, Procedure Browser, naming, types | finding or calling a PDB procedure |
| [script-fu.md](script-fu.md) | Scheme syntax essentials and `script-fu-register` argument order | writing or reading a Script-Fu script |
| [python-fu.md](python-fu.md) | Python 3 + GObject Introspection; the `Gimp.PlugIn` model | writing or reading a Python plug-in |
| [pdb-recipes-images-layers.md](pdb-recipes-images-layers.md) | Real Script-Fu recipes: create image, layers, fill, resize, flatten | scripting image and layer operations |
| [pdb-recipes-selections-paths.md](pdb-recipes-selections-paths.md) | Selection/path automation map + Procedure Browser routing | scripting selections or paths |
| [pdb-recipes-color-filters.md](pdb-recipes-color-filters.md) | Colors/filters automation map + Procedure Browser routing | scripting color adjustments or filters |
| [pdb-recipes-io-batch.md](pdb-recipes-io-batch.md) | Save/export patterns and verbatim headless/batch command-line flags | exporting or running GIMP headless |

## Reading paths

- **Driving GIMP via PDB/MCP:** scripting-overview → pdb-reference → pdb-recipes-images-layers →
  pdb-recipes-io-batch, then the other recipe files as needed.
- **Writing a script/plug-in:** scripting-overview → script-fu or python-fu → pdb-reference.
- **Editing an image by hand:** interface-and-workflow → tools-overview → layers-and-modes →
  selections → masks-and-channels.
- **Color/output work:** colors-and-adjustments → filters → file-formats-and-export.

## Note on PDB coverage

The GIMP 3.2 *web* manual prints exact procedure names only where its Script-Fu tutorial shows them
(image/layer creation, fill, resize, flatten). For selections, paths, color adjustments, filters, and
file load/save it documents the **menu commands**, not the procedure signatures. Those references
therefore route to the in-app **Help > Procedure Browser**, which is the authoritative source for
exact names, parameters, and return types — they do not guess.
