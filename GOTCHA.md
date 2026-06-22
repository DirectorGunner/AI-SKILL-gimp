# GIMP — Gotchas

Recurring failure modes when relying on the GIMP reference, and what to do instead. Read alongside `SKILL.md`.

- This reference targets GIMP 3.2; PDB procedure names (`gimp-*`), Script-Fu/Python-Fu calls, menu paths, and parameters differ from 2.10 — verify against the installed GIMP version.
- Script-Fu (Scheme) and Python-Fu (GObject-Introspection) APIs differ in naming and argument style; confirm which runtime you are in before calling a procedure.
- Headless/batch (`gimp -i -b`) behavior and available procedures can differ from the interactive GUI; verify a procedure exists in your build's PDB.
- If a procedure, menu path, or option is not in the references, say so and mark it `TODO` — never invent one.