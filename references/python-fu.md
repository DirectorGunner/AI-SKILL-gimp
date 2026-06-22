# Python-Fu Plug-ins

Python-Fu in GIMP 3.2 is Python 3 driven through GObject Introspection: you import the `Gimp` namespace and subclass `Gimp.PlugIn`. This file covers the import preamble, the registration model, calling the PDB, and the console.

**When this applies:** Read this when writing or reading a GIMP 3.2 Python plug-in, setting up the `gi` imports, wiring registration, or calling the PDB from Python.

## The import preamble

Pin each typelib version with `gi.require_version` before importing it.

```python
import sys
import gi
gi.require_version('Gimp', '3.0')
from gi.repository import Gimp
gi.require_version('GimpUi', '3.0')
from gi.repository import GimpUi
from gi.repository import GObject
from gi.repository import GLib
```

## Declaring and building a procedure

Subclass `Gimp.PlugIn`; return procedure names from `do_query_procedures`; construct each in `do_create_procedure` with `Gimp.ImageProcedure.new`. The `run` callback receives `(procedure, run_mode, image, drawables, config, run_data)` — note `drawables` is plural.

```python
class MyPlugin(Gimp.PlugIn):
    def do_query_procedures(self):
        return ["my-plug-in"]
    def do_create_procedure(self, name):
        proc = Gimp.ImageProcedure.new(self, name, Gimp.PDBProcType.PLUGIN, self.run, None)
        proc.set_menu_label("My plug-in")
        proc.add_menu_path('<Image>/Filters/Tutorial/')
        return proc
    def run(self, procedure, run_mode, image, drawables, config, run_data):
        Gimp.message("Hello")
        return procedure.new_return_values(Gimp.PDBStatusType.SUCCESS, GLib.Error())

Gimp.main(MyPlugin.__gtype__, sys.argv)
```

## Calling a PDB procedure by name

Look it up, build a config, set properties, run; check the status from `result.index(0)`:

```python
procedure = Gimp.get_pdb().lookup_procedure('gimp-image-flatten')
config = procedure.create_config()
config.set_property('image', image)
result = procedure.run(config)
if result.index(0) is Gimp.PDBStatusType.SUCCESS:
    pass
```

Typed GObject-Introspection methods are the alternative: `Gimp.Image.new(...)`, `drawable.brightness_contrast(...)`.

## The Python-Fu Console

Open **Filters > Development > Python-Fu > Python-Fu Console** — an interactive Python shell pre-loaded with the `gimp` and `pdb` objects.

## Do / Don't

- **Do** call `gi.require_version(...)` for each namespace before importing it.
- **Do** treat `run`'s `drawables` argument as plural (multiple selected drawables).
- **Don't** carry over GIMP 2.10 Python-Fu idioms; the 3.x model is `Gimp.PlugIn` + GObject Introspection.
- **Don't** pass run-mode positionally to a looked-up procedure; set it via `config.set_property('run-mode', Gimp.RunMode.NONINTERACTIVE)`.

## Related

`scripting-overview.md` · `script-fu.md` · `pdb-reference.md` · `pdb-recipes-images-layers.md` · `pdb-recipes-io-batch.md`
