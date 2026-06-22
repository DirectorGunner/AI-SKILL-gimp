---
name: gimp
description: >-
  Use when working with GIMP, the GNU Image Manipulation Program (especially GIMP 3.2) - editing or
  generating raster images; working with layers, layer/blend modes, masks, channels, selections, or
  Bézier paths; applying tools or filters; adjusting colors, levels, curves, or ICC color profiles;
  importing or exporting image files (.xcf, PNG, JPEG); or automating GIMP through Script-Fu,
  Python-Fu, the Script-Fu Console, or the Procedural Database (PDB) - including driving GIMP from a
  GIMP MCP server or a headless/batch (gimp -i -b) run. Also fires when you see .xcf files, gimp-*
  procedure calls, script-fu-register, "from gi.repository import Gimp", or GObject-Introspection
  GIMP plug-ins, even when the user never says "GIMP" by name. Gives task-routed, faithful 3.2
  reference with worked examples.
covers:
  - recipe
  - procedure browser
  - selection
  - feather
  - save to channel
  - paths
  - levels
  - curves
  - xcf
  - export
  - script-fu
  - python-fu
---

# GIMP 3.2

Task-organized, faithful guidance for GIMP 3.2 (GNU Image Manipulation Program), with emphasis on
driving GIMP programmatically through Script-Fu, Python-Fu, and the Procedural Database (PDB) — for
example from a GIMP MCP server. Content is original; identifiers (menu paths, option labels,
keyboard shortcuts, mode names, procedure names, numbers) are preserved exactly as the manual prints
them.

## When to use this skill

Reach for this skill whenever a task touches GIMP: editing or generating images; layers, blend modes,
masks, channels, selections, or paths; tools or filters; color adjustments and color management;
opening, saving (`.xcf`), or exporting (PNG/JPEG); or automating GIMP via Script-Fu / Python-Fu / the
PDB — including when the user opens a `.xcf` file, pastes `gimp-*` calls, writes `script-fu-register`
or `from gi.repository import Gimp`, or wires up a GIMP MCP server, without naming "GIMP".

## How to use it (runtime workflow)

1. Read this file, then consult the **task router** below (or `references/topics.json`).
2. Open only the one or two reference files relevant to the task — do not read everything
   (progressive disclosure).
3. Answer strictly from the reference; preserve menu paths, option labels, shortcuts, mode names, and
   procedure names exactly as written.
4. If something is not covered, say so and mark it `TODO` — never invent a menu path, option, or PDB
   procedure name. For scripting, the in-app **Help > Procedure Browser** is the authoritative source
   for exact procedure names, parameters, and return types.
5. Remember the GIMP 3.x API is not 2.10: Python-Fu is Python 3 + GObject Introspection, and many PDB
   procedures were renamed — verify names before relying on them.

## Task router

| If the task is about… | Read |
| --- | --- |
| windows, docks/dialogs, the menu map, zoom/undo, image Mode or Encoding (bit depth) | `references/interface-and-workflow.md` |
| the Toolbox, Tool Options, which tool to use and its shortcut | `references/tools-overview.md` |
| layers, the Layers dialog, groups, alpha, opacity, blend/paint modes | `references/layers-and-modes.md` |
| selections, selection modes, feathering, the Select menu | `references/selections.md` |
| layer masks, the Channels dialog, saving/loading selections, Quick Mask | `references/masks-and-channels.md` |
| Bézier paths, the Paths dialog, stroking, path↔selection, SVG | `references/paths.md` |
| the Colors menu, levels/curves/hue-saturation, ICC profiles (assign vs convert) | `references/colors-and-adjustments.md` |
| the Filters menu taxonomy, Repeat/Re-Show Last | `references/filters.md` |
| opening/importing, saving `.xcf`, exporting/overwriting, PNG/JPEG options | `references/file-formats-and-export.md` |
| Script-Fu vs Python-Fu, the consoles, install dirs, batch/headless flags | `references/scripting-overview.md` |
| the PDB, Procedure Browser, procedure naming and types | `references/pdb-reference.md` |
| Scheme syntax, `script-fu-register` / `script-fu-menu-register` | `references/script-fu.md` |
| Python 3 + GObject Introspection, the `Gimp.PlugIn` model | `references/python-fu.md` |
| scripting image/layer ops (create, fill, resize, flatten) | `references/pdb-recipes-images-layers.md` |
| scripting selections and paths | `references/pdb-recipes-selections-paths.md` |
| scripting color adjustments and filters | `references/pdb-recipes-color-filters.md` |
| scripting file save/export and headless batch runs | `references/pdb-recipes-io-batch.md` |

## Gotchas

Recurring failure modes and what to do instead live in the sibling [GOTCHA.md](GOTCHA.md).

## Verification notes

Validate the package structure (the validator ships with the skill-drafting skill; paths use the `DEVROOT` env var — adjust to your layout):

```powershell
python "$env:DEVROOT\SKILLS\skills\skill-drafting\scripts\validate_skill_package.py" "$env:DEVROOT\SKILLS\skills\gimp"
```

This package is built and checked with the three-layer method (Spec → Verifier → Environment).
Ground-truth checks live in `AI/work/verify_gimp.py` (stdlib only; run `python AI/work/verify_gimp.py
--both`). It verifies: every reference is listed in `references/INDEX.md`, has exactly one
`references/topics.json` entry, and resolves its cross-links; each reference contains a summary, a
"When this applies" line, at least one example, and a Do/Don't or anti-patterns section, with no empty
placeholders; an originality gate rejects source branding/attribution/license leakage in the
references and in the SKILL.md body (outside "Inspired by"); a preserve-glossary of load-bearing
identifiers (menu paths, shortcuts, mode names, PDB procedure names, command-line flags) is grepped
against the references so accidental renames are caught; and `--both` confirms the `.claude` mirror is
byte-identical. Keep those invariants when editing.

## Reference map

Start at `references/INDEX.md`. Metadata: `references/topics.json` (topic → file + keywords).

## Official documentation

Includes original content written for this skill. The official documentation is at https://docs.gimp.org/ — consult it to verify anything uncertain, conflicting, or version-specific.
