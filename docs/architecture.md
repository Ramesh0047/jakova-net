# JAKOVA-NET Architecture (v1.0)

This document is a high-level architecture sketch for **JAKOVA-NET** as a
local-first AI operating system.

The detailed, citable spec is in the Zenodo OS paper:

- Evans, J., & JAKOVA. (2025). *JAKOVA-NET v1.0: Local-First AI Operating System
  (Model as BIOS, Not App).* https://doi.org/10.5281/zenodo.17861175

This file stays informal and implementation-oriented.

---

## 1. Layer model

Conceptually, JAKOVA-NET is split into a few layers:

1. **Hardware layer**

   - Whatever box you have: 2019 MSI GL73 laptop, tower, cluster, etc.
   - OS is currently “normal” (Windows / Linux), JAKOVA-NET sits on top.

2. **Host OS + runtime layer**

   - Python runtime
   - Unity runtime (for Fractal Voyager Engine demo)
   - Future: other engines (C#, Rust, etc.) can join as long as they speak JSON.

3. **Model / BIOS layer**

   - The LLM (and any helpers) are treated like **firmware**.
   - They don’t live as a “chat app” – they are the decision / reasoning core the
     rest of the system calls into.
   - This layer should be swappable as long as interface contracts are respected.

4. **State layer (JSON state file)**

   - Single JSON (or small set of files) is the **source of truth**.
   - Engines read from / write to this state; views are projections.
   - In the current demo, this state file drives the Fractal Voyager Engine.

5. **Engine layer**

   - Python processes that:
     - interpret state
     - talk to the model
     - manage IO and coordination between tools
   - Unity processes that:
     - render the cosmos / other “universes”
     - receive camera / interaction commands

6. **View / interaction layer**

   - Anything that faces a human:
     - Unity viewer window
     - CLI tools
     - Future: web UI, dashboards, etc.
   - Views are deliberately dumb: all “intelligence” is pushed downwards into
     model + state + engines.

---

## 2. Fractal Voyager Engine (FVE) in this model

For the current demo:

- **Hardware:** 2019 MSI GL73 laptop
- **Host OS:** Windows
- **Model layer:** external LLM (JAKOVA) acting as BIOS
- **State:** `voyager_state.json` (name TBD)
- **Engines:**
  - Python backend that:
    - loads the JSON
    - computes positions / metadata for objects (stars, systems, etc.)
    - serves data to Unity over a local interface
  - Unity client that:
    - renders objects as a navigable “cosmos”
    - sends camera / selection events back to Python

Everything interesting flows through the JSON state and the model/BIOS layer.

If we swap the schema (e.g. robots instead of stars) but keep the pattern,
we still have JAKOVA-NET. That’s the point.

---

## 3. Local-first properties (what “local-first AI OS” means here)

- **No hard dependency on remote servers** for core functionality.
- The **authoritative state** is on disk, not in a cloud database.
- Model calls can be:
  - to a local model, or
  - to a remote API *treated as a pluggable BIOS module*, not as the whole system.
- The system should be able to:
  - degrade gracefully when offline
  - keep logs / state locally
  - resync or extend when connectivity returns.

---

## 4. Future directions (v1.x+)

Roadmap-style, not promises:

- Clean interface spec for the **BIOS layer** (so different models can plug in).
- Formal schema for the JSON state file(s).
- Multiple engines:
  - cosmos viewer
  - robotics / factory sim
  - printer / vehicle / logistics views
- Local-only mode with an on-box model stack.

---

## 5. Implementation notes

This file is intentionally free-form. When the implementation stabilises,
we can either:

- promote parts of this into the Zenodo spec, or
- link out to more detailed docs for each engine.
