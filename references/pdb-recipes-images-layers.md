# PDB Recipes: Images and Layers

Worked Script-Fu calls for building images and managing layers, using only procedure names the GIMP 3.2 manual prints. Run snippets in the console at **Filters > Development > Script-Fu > Script-Fu Console**.

**When this applies:** Read this when you are driving GIMP through the PDB and need to create an image, add or stack layers, fill, resize, or flatten.

## Create an image with a layer and show it

Make a blank RGB image, add a full-size layer, fill its background, then display.

```scheme
(let* ((img (car (gimp-image-new 640 480 RGB)))
       (lyr (car (gimp-layer-new img "layer 1" 640 480 RGB-IMAGE 100 LAYER-MODE-NORMAL))))
  (gimp-image-insert-layer img lyr 0 0)        ; args: image layer parent position
  (gimp-context-set-background '(255 255 255))
  (gimp-drawable-fill lyr FILL-BACKGROUND)
  (gimp-display-new img)
  (gimp-image-clean-all img))
```

## Resize the canvas and a layer together

```scheme
(let* ((w (car (gimp-drawable-get-width  lyr)))
       (h (car (gimp-drawable-get-height lyr))))
  (gimp-image-resize img w h 0 0)              ; new-width new-height offx offy
  (gimp-layer-resize lyr w h 0 0))
```

## Flatten an image inside an undo group

`gimp-image-flatten` returns the single resulting layer; wrap multi-step edits so one undo reverses them.

```scheme
(gimp-image-undo-group-start img)
(gimp-image-flatten img)
(gimp-image-undo-group-end img)
```

## Move a layer by an offset

```scheme
(gimp-layer-set-offsets lyr 35 35)             ; offset-x offset-y
```

## Layer ops the web manual leaves to the browser

TODO: the 3.2 web manual documents duplicate, merge-down, reorder, and the opacity/mode setters only as **Layer** menu commands (e.g. **Layer > Duplicate Layers**, **Layer > Merge Down**), not as PDB names. Look up the exact procedures in **Help > Procedure Browser**.

## Do / Don't

- **Do** take `(car …)` of a procedure result: GIMP returns lists, even for one value.
- **Do** pass colors as `'(r g b)` lists and use the constants `RGB`, `RGB-IMAGE`, `LAYER-MODE-NORMAL`, `FILL-BACKGROUND` verbatim.
- **Don't** invent layer procedure names; verify any not shown here in the Procedure Browser.
- **Don't** reorder arguments — `gimp-image-insert-layer` is image, layer, parent, position.

## Related

`pdb-recipes-selections-paths.md` · `pdb-recipes-io-batch.md` · `script-fu.md` · `pdb-reference.md` · `layers-and-modes.md`
