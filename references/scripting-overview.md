# Scripting and Plug-ins

GIMP can be driven by code as well as by mouse. This file orients an agent to the two scripting languages, where their consoles live, how add-ons are installed, and how to run GIMP non-interactively.

**When this applies:** Read this first whenever a task involves automating GIMP, writing or installing a script or plug-in, choosing between Script-Fu and Python-Fu, or driving GIMP from a server/MCP.

## Plug-ins versus scripts

A plug-in is an external program that runs under the control of the main GIMP application; everything in the **Filters** menu is a plug-in. Scripts are interpreted programs that GIMP runs through a bundled interpreter rather than as separate compiled binaries. Both reach GIMP's functionality through the same Procedural Database (see `pdb-reference.md`).

## Script-Fu versus Python-Fu

Script-Fu is the built-in scripting layer based on the Scheme language, always available. Python-Fu uses Python 3 through GObject Introspection: a plug-in begins with `import gi`, then `gi.require_version('Gimp', '3.0')` and `from gi.repository import Gimp`, and defines a class inheriting from `Gimp.PlugIn`. Choose Script-Fu for portable, dependency-free automation; Python-Fu when you want Python libraries or richer logic.

## The consoles

- Script-Fu: **Filters > Development > Script-Fu > Script-Fu Console** — evaluates Scheme expressions immediately; the fastest way to try a PDB call. A Script-Fu server starts from **Filters > Development > Script-Fu > Start Server**.
- Python-Fu: **Filters > Development > Python-Fu > Python-Fu Console** — an interactive Python shell pre-loaded with the `gimp` and `pdb` objects.

```scheme
(car (gimp-image-new 640 480 RGB))   ; evaluate a PDB call directly in the Script-Fu console
```

## Installing scripts and plug-ins

To add a Script-Fu script, copy or move its file into one of GIMP's Scripts folders, whose location is shown under **Preferences: Folders > Scripts**, then restart GIMP. A plug-in goes under GIMP's user `/plug-ins` directory in a folder whose name matches the plug-in's filename; on Linux/Unix this is `~/gimp-3.2/plug-ins`, and there you can also run `gimptool-3.2 --install borker.c`. TODO: literal Scripts path strings and Windows/macOS plug-in paths are not printed in the manual.

## Headless and batch invocation

Run GIMP non-interactively from the command line:

- `-i`, `--no-interface` — run without a user interface.
- `-b`, `--batch=commands` — execute the commands non-interactively; when the command is `-`, commands are read from standard input.
- `--batch-interpreter=proc` — the procedure used to process batch commands; the default is Script-Fu.
- `-d`, `--no-data` and `-f`, `--no-fonts` — skip loading data/fonts for faster startup.

```bash
# -i = no UI; repeat -b for several commands; default interpreter is Script-Fu
gimp -i -b '(car (gimp-image-new 640 480 RGB))'
```

See `pdb-recipes-io-batch.md` for a load/flatten/save batch and the (deprecated) quit note.

## Do / Don't

- **Do** open **Filters > Development > Script-Fu > Script-Fu Console** (or the Python-Fu Console) to test calls interactively.
- **Do** match a plug-in's folder name to its filename when installing.
- **Don't** assume the older `Filters > Script-Fu > Console` path; 3.2 places both consoles under **Development**.
- **Don't** invent batch procedures the manual does not state — verify them in the Procedure Browser.

## Related

`script-fu.md` · `python-fu.md` · `pdb-reference.md` · `pdb-recipes-io-batch.md` · `filters.md`
