# Fractal Voyager Engine – State

This directory will hold the JSON state files that drive the Fractal Voyager Engine.

Concept:

- The **state file** is the single source of truth.
- Engines (backend + viewer) are projections of this state.
- Changing the file (by hand, via tools, or via the model/BIOS layer)
  changes the visible “universe”.

Planned contents:

- `example_state.json` – minimal example with a few objects.
- Schema notes and validations (link back to `docs/architecture.md`).

Until we lock the schema, this directory stays light and mostly documented.
