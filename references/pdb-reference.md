# The Procedural Database (PDB)

The Procedural Database is GIMP's registry of callable procedures — the single API that Script-Fu and Python-Fu use to do real work. This file explains the system; concrete task recipes live in the `pdb-recipes-*.md` files.

**When this applies:** Read this when you need to find a procedure, understand procedure names and types, or call PDB procedures from either scripting language.

## What the PDB is

The Procedural Database holds the procedures that scripts and plug-ins call to operate on GIMP. Because the database is the shared surface for both languages, learning a procedure once lets you call it from either Script-Fu or Python-Fu.

## The Procedure Browser

Open it from **Help > Procedure Browser**. It displays the procedures in the PDB and lets you search by name, description, help, authors, copyright, date, and type; selecting an entry shows its details on the right. The manual identifies four procedure types: **Internal GIMP procedure**, **GIMP Plug-In**, **GIMP Extension**, and **Temporary Procedure**. Treat this browser as the authoritative source for exact procedure names and signatures.

## Naming conventions

The same operation has two spellings: the C/Python function uses underscores (`gimp_image_new`, `Gimp.Image.new`), while Script-Fu uses hyphens (`gimp-image-new`). Names follow a category-object-action shape (`gimp-layer-new`, `gimp-drawable-get-width`).

## Calling from Script-Fu

Prefix notation; procedures return a list, so take `car` for a single value:

```scheme
(car (gimp-image-new 640 480 RGB))   ; the new image is the first list element
```

## Calling from Python — two ways

Typed GObject-Introspection methods (`Gimp.Image.new(...)`, `drawable.brightness_contrast(...)`), or generic lookup by name through the PDB:

```python
procedure = Gimp.get_pdb().lookup_procedure('gimp-image-flatten')
config = procedure.create_config()
config.set_property('image', image)
result = procedure.run(config)
if result.index(0) is Gimp.PDBStatusType.SUCCESS:
    pass
```

## 3.x deprecations and renames

GIMP 3.0 reworked the API relative to 2.10 — for example `gimp-brightness-contrast` became `gimp-drawable-brightness-contrast`, `gimp-file-save` dropped its per-drawable argument, and `gimp-quit` is now deprecated and takes no argument. Do not assume 2.10 names persist; confirm current names and signatures in the Procedure Browser. TODO: the full set of PDB type names is not on one manual page — read types per procedure in the browser.

## Do / Don't

- **Do** use **Help > Procedure Browser** as ground truth for names, parameters, and return types.
- **Do** remember PDB calls return a list; take `car` for a single value in Script-Fu.
- **Don't** carry over remembered 2.10 procedure names without verifying them in 3.2.
- **Don't** fabricate type names or signatures the manual doesn't print — mark TODO and point to the browser.

## Related

`scripting-overview.md` · `script-fu.md` · `python-fu.md` · `pdb-recipes-images-layers.md` · `pdb-recipes-io-batch.md`
