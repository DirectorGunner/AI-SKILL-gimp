# GIMP 3.2 Skill

> _Task-routed, faithful GIMP 3.2 reference for editing and generating raster images and for automating GIMP through Script-Fu, Python-Fu, and the Procedural Database._

Part of **[Agent Kaizen](https://github.com/DirectorGunner/agent-kaizen)** — Agent Kaizen is designed to support reliable AI agent workflows, context engineering, and AI systems engineering in VS Code, Codex, and Claude Code. Build reusable agent skills, reduce unnecessary context loading, add validation loops, and apply Spec → Verifier → Environment scaffolding to new and existing projects.

This repository is the `gimp` skill: a reusable, trigger-rich task handbook that an AI coding agent (OpenAI Codex, Claude Code) loads on demand when a task matches its triggers.

## What this skill covers

This skill gives faithful, task-organized guidance for GIMP 3.2 (the GNU Image Manipulation Program): layers, blend/paint modes, masks, channels, selections (including feathering and saving to channels), and Bézier paths, plus tools, the Filters menu, and color work such as levels, curves, hue-saturation, and ICC profile assign-versus-convert. It covers opening, saving `.xcf`, and exporting PNG/JPEG, and emphasizes driving GIMP programmatically through Script-Fu, Python-Fu, the Script-Fu Console, and the Procedural Database (PDB) — including headless/batch (`gimp -i -b`) runs and a GIMP MCP server. Identifiers like menu paths, option labels, shortcuts, mode names, and `gimp-*` procedure names are preserved exactly as the manual prints them. It also flags the GIMP 3.x break from 2.10 — Python-Fu is now Python 3 plus GObject Introspection and many PDB procedures were renamed.

## What's inside

- `SKILL.md` — frontmatter (`name` + trigger-rich `description`) and a lean body.
- `references/` — right-sized topic files the agent loads only when relevant (plus `INDEX.md` and `topics.json`).
- `GOTCHA.md` — known pitfalls and edge cases.

## Use it

This skill is one git repo inside the Agent Kaizen **skills store**. The store nests two folders on purpose: the outer **`SKILLS\`** is a VS Code project for building and maintaining skills (its own workspace + tooling), and the inner lowercase **`skills\`** holds every skill as its own repo. That split lets a project pull skills two ways — the **whole `skills\` folder at once** (loads everything — **not recommended**) or **one skill at a time** (recommended: load only what a task needs and stay under Claude Code's skill-listing budget).

Paths below use **`%DEVROOT%`** — the `DEVROOT` environment variable pointing at the folder that contains `SKILLS\`. Set it once by running **`SetDevRoot.cmd`** in the SKILLS repo root (no admin); a new shell then resolves `%DEVROOT%` automatically.

Link **just this skill** (recommended) — a Windows directory junction, no admin:

```cmd
mklink /J .agents\skills\gimp  "%DEVROOT%\SKILLS\skills\gimp"
mklink /J .claude\skills\gimp  "%DEVROOT%\SKILLS\skills\gimp"
```

Or link the **whole store** at once (loads every skill — not recommended outside a skills-dev project):

```cmd
mklink /J .agents\skills  "%DEVROOT%\SKILLS\skills"
mklink /J .claude\skills  "%DEVROOT%\SKILLS\skills"
```

Remove a link (the store copy is untouched):

```cmd
rmdir .agents\skills\gimp
rmdir .claude\skills\gimp
```

The agent (OpenAI Codex, Claude Code) then auto-loads this skill whenever a task matches its triggers. Built and validated with **[skill-drafting](https://github.com/DirectorGunner/AI-skill-drafting)** to the Agent Kaizen gold standard.

## License

Licensed under **AGPL-3.0**, matching the [Agent Kaizen](https://github.com/DirectorGunner/agent-kaizen) project.
