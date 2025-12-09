# Fractal Voyager Engine (FVE) – Notes

This doc tracks the first live implementation of the JAKOVA-NET pattern:
the **Fractal Voyager Engine**.

Goal: demo a local-first AI OS where a single JSON state file drives a
Python + Unity cosmos viewer stack on a 2019 MSI GL73 laptop.

---

## 1. High-level flow

1. Load JSON state file (e.g. `state/voyager_state.json`).
2. Python backend:
   - parses objects (stars, systems, etc.)
   - builds a data model for the scene
   - exposes data over a local interface (file, socket, HTTP – TBD)
3. Unity viewer:
   - requests scene data from Python
   - renders objects as a navigable 3D/4D “cosmos”
   - sends camera / selection events back to Python
4. Python updates state (and optionally calls the model/BIOS layer).
5. Updated state gets reflected back into the viewer on next tick.

The **JSON state file is the truth**. Everything else is projection.

---

## 2. Intended repo layout for FVE

Planned structure (names may change):


Right now this is just a scaffold so the code has somewhere to land.

---

## 3. Open questions / TODOs

- Decide final transport between Python ↔ Unity (HTTP, gRPC, named pipes, etc.).
- Lock in a minimal JSON schema for:
  - objects (id, position, type, metadata)
  - camera / view state
- Define where model/BIOS calls sit in the loop:
  - e.g. text commands → state mutations → visual changes.

---

## 4. Relation to the OS pattern

FVE is **one** engine sitting on the JAKOVA-NET stack:

- It proves: “one JSON state file, many universes” is real, not just a metaphor.
- It should be replaceable by other engines (robotics, logistics, etc.) without
  changing the core OS ideas.

When we stabilise FVE, this doc will be updated with more concrete implementation
details and links to actual code.
