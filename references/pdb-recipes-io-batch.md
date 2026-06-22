# PDB Recipes: File I/O and Batch

Worked PDB calls for loading, exporting, and running GIMP headless in 3.x, with procedure names and
signatures confirmed against the GIMP 3.0 API. Script-Fu uses the hyphenated form; confirm parameter
details in **Help > Procedure Browser**.

**When this applies:** Read this when scripting file load/save/export, flatten-before-export, or
headless/batch runs.

## Load and save

`gimp-file-load` takes a run mode and a file and returns the image. `gimp-file-save` takes a run mode,
image, file, and export options — **note 3.0 dropped the per-drawable argument** that 2.10 had; it now
saves the whole image, and `options` may be NULL. Both pick the format from the file.

```scheme
(let* ((image (car (gimp-file-load RUN-NONINTERACTIVE file))))
  (gimp-image-flatten image)
  (gimp-file-save RUN-NONINTERACTIVE image file options)   ; options may be NULL
  (gimp-displays-flush))
```

In the C/GI API the file is a `GFile`: `gimp_file_load(run_mode, file)` returns a `GimpImage`, and
`gimp_file_save(run_mode, image, file, options)` returns a boolean. TODO: confirm how Script-Fu passes
the file (string vs `GFile`) and the `options` value in the Procedure Browser. `RUN-NONINTERACTIVE`
(Script-Fu) corresponds to `Gimp.RunMode.NONINTERACTIVE` (Python).

## Headless / batch invocation

The manual documents these command-line flags verbatim (Chapter 2, "Starting GIMP"):

- `-i`, `--no-interface` — run without a user interface.
- `-b`, `--batch=commands` — execute commands non-interactively; when the command is `-`, read from standard input.
- `--batch-interpreter=proc` — procedure used to process batch commands; the default is Script-Fu.
- `-d`, `--no-data` and `-f`, `--no-fonts` — skip loading data/fonts for faster startup.

```bash
# Convert a PNG to JPEG headless; default interpreter is Script-Fu
gimp -i -d -f -b '(let* ((img (car (gimp-file-load RUN-NONINTERACTIVE (gimp-file-load-...)))))...)'
```

## Quitting

`gimp-quit` exists but is **deprecated** in 3.0 and now takes **no arguments** (`gimp_quit(void)`); the
docs advise plug-ins to quit cleanly by returning gracefully rather than forcing it. This corrects the
old 2.10 idiom `(gimp-quit 0)` — do not pass an argument.

## Do / Don't

- **Do** pair `--batch` with `-i`, and combine `-d -f` for fast, dependency-light headless runs.
- **Do** flatten before exporting to flat formats; `gimp-file-save` selects the format from the file.
- **Don't** pass a drawable to `gimp-file-save` — 3.0 removed that argument.
- **Don't** call `(gimp-quit 0)`; 3.0's `gimp-quit` takes no argument and is deprecated.

## Related

`pdb-recipes-images-layers.md` · `file-formats-and-export.md` · `scripting-overview.md` · `script-fu.md` · `pdb-reference.md`
