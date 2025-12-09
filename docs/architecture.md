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

# JAKOVA-NET Architecture

## 1. Overview

JAKOVA-NET is a **local-first AI operating system pattern** built around three core pieces:

1. **Model as BIOS** – the LLM behaves like firmware:
   - boots the system
   - helps decide how to mutate state
   - does not own the user’s world

2. **JSON state file as event horizon** – a single canonical state file on disk:
   - describes the current “universe” (cosmos, lab, factory, etc.)
   - is the only thing engines are allowed to mutate

3. **Engines as lenses** – Python, Unity, and other runtimes:
   - read the JSON
   - render or act on it
   - never assume they are the source of truth

Everything else is details.

---

## 2. Core components

### 2.1 BIOS layer (model)

Roles:

- interpret human intent
- map high-level goals into changes to the JSON state
- enforce safety and ownership rules described in JAKOVA-NET Prime

Properties:

- runs locally where possible
- has no hidden network calls for core decisions
- treats user data and ideologies as first-class objects, not fuel

### 2.2 State layer (JSON)

Single file (per universe) with three main blocks:

- `meta` – universe ID, title, version, timestamps
- `camera` – viewer mode, position, target, FOV
- `objects[]` – list of entities in the universe:
  - `id` – stable identifier
  - `type` – e.g. `star`, `station`, `robot`, `vehicle`, `printer`
  - `position` – `[x, y, z]`
  - `scale` – scalar or vector
  - `labels[]` – tags for grouping, UI, or governance
  - `data{}` – type-specific payload

The schema is documented in `fve/state-schema.v0.json`.

### 2.3 Engines

Engines are replaceable.

- **Python backend**
  - handles loading/saving the JSON
  - coordinates physics, simulation logic, or routing
  - talks to the model (BIOS) when decisions are needed

- **Unity viewer**
  - visualises the universe in 3D/4D
  - never edits the JSON directly; it sends intents back to the backend

In future, engines might be:

- robotics controllers
- printers / fabrication pipelines
- data-viz dashboards
- lab-automation stacks

Same state pattern, new engines.

---

## 3. Execution loop (simplified)

1. **Boot**
   - BIOS loads the JSON state file from disk.
   - If missing, BIOS can generate a seed universe.

2. **Render**
   - Engines read the state and render a view or simulation.

3. **Interact**
   - Human input (or sensors) generates intents.
   - Engines send intents to the BIOS/backend, not directly to the JSON.

4. **Mutate**
   - BIOS validates the intent against:
     - safety rules
     - ownership/ideology rules (see `docs/ideology.md`)
   - If allowed, backend mutates the JSON.

5. **Persist**
   - New state is written back to disk as the new event horizon.

Loop repeats.

---

## 4. Local-first constraints

To call something “JAKOVA-NET-compatible”, the following should hold:

- Core state is stored **locally first**, not in a remote database.
- The system can **boot and function in degraded mode offline**.
- Cloud services, if used, are accelerators – not owners of the core state.
- User can export, archive, or delete their universes without asking a third party.

---

## 5. Relationship to the Zenodo specs

This document is the practical twin of the following citable specs:

- v1.0 OS architecture  
- v2 life/lab/cosmos bridge  
- EXAWATTS work-class  
- EBNT cross-scale theory

If there is a conflict between this file and the Zenodo papers, the papers win; this file will be updated as the canon moves.

