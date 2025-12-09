# Fractal Voyager Engine – Backend (Python)

This directory will contain the Python side of the Fractal Voyager Engine (FVE).

Responsibilities:

- Load and validate the JSON state file (see `../state/`).
- Build an in-memory model of the current “universe” (stars, systems, etc.).
- Expose data to the viewer (Unity) over a local interface.
- Receive input / selection events from the viewer and update state.
- Optionally call into the model/BIOS layer (JAKOVA) to:
  - interpret user commands
  - generate or modify structures
  - perform higher-level planning.

For now this is just a placeholder. Code will be added once the interfaces and
schema are locked in.
