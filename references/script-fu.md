# Script-Fu Language Essentials

Script-Fu is GIMP's built-in Scheme scripting language whose forms call the PDB. This file covers the syntax, the registration functions, and the GIMP 3 (ScriptFu v3) changes.

**When this applies:** Read this when writing, fixing, or explaining a `.scm` Script-Fu script, or when you need the registration functions or the `SF-` argument types.

## Scheme syntax

Everything is a parenthesized list whose first element is the operator; calls nest freely. Bind locals with `let*`, reassign with `set!`, define procedures with `define`; take a list's head with `car` and tail with `cdr`; quote a literal list with `'(…)`.

```scheme
(let* ((sum (+ 5 6))) (car '("a" "b")))   ; → "a"
```

## Calling a PDB procedure

Procedures are dashed names that return a list, so wrap the call in `car` to grab the result:

```scheme
(let* ((image (car (gimp-image-new 640 480 RGB))))
  (gimp-display-new image)
  (gimp-image-clean-all image))
```

## Registering a script (classic form)

`script-fu-register` takes, in this exact order: procedure name, label, description, author, copyright, date, an image-types string (empty for none), then one `SF-TYPE  "label"  default` triplet per parameter; `script-fu-menu-register` places it in a menu.

```scheme
(script-fu-register
  "script-fu-my-box" "My Box" "Builds a box." "Author"
  "copyright 2026, Author" "June 15, 2026" ""
  SF-STRING     "Text"      "Hi"
  SF-ADJUSTMENT "Font size" '(50 1 1000 1 10 0 1)
  SF-COLOR      "Color"     '(0 0 0))
(script-fu-menu-register "script-fu-my-box" "<Image>/Filters/Tutorial")
```

## GIMP 3 (ScriptFu v3) changes

- `script-fu-register` is now **deprecated**: scripts using it still run but get an old look-and-feel, no automated dialog, and no persistent settings. Prefer **`script-fu-register-filter`** or **`script-fu-register-procedure`** for new scripts.
- `SF-VALUE` is **obsolete** (it let users enter arbitrary strings that errored); use `SF-ADJUSTMENT` or `SF-STRING` instead.

## SF- argument types

- Object types: `SF-IMAGE`, `SF-LAYER`, `SF-CHANNEL`, `SF-DRAWABLE`, `SF-VECTORS`.
- Resource types: `SF-BRUSH`, `SF-FONT`, `SF-GRADIENT`, `SF-PALETTE`, `SF-PATTERN`.
- Inputs: `SF-STRING`, `SF-ADJUSTMENT`, `SF-SPINNER`, `SF-TOGGLE`, `SF-COLOR`, `SF-OPTION`, `SF-ENUM`.
- v3 multi-drawable: `SF-ONE-DRAWABLE`, `SF-ONE-OR-MORE-DRAWABLE`, `SF-TWO-OR-MORE-DRAWABLE`.

## Do / Don't

- **Do** wrap PDB calls in `car` to extract the returned value.
- **Do** prefer `script-fu-register-filter` / `script-fu-register-procedure` for new GIMP 3 scripts.
- **Don't** use `SF-VALUE` in new scripts; it is obsolete.
- **Don't** drop or misorder the seven leading `script-fu-register` arguments.

## Related

`scripting-overview.md` · `python-fu.md` · `pdb-reference.md` · `pdb-recipes-images-layers.md` · `pdb-recipes-selections-paths.md`
