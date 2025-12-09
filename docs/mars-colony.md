# JAKOVA-NET Martian Project X  
_Mars colony stack on a local-first AI operating system_

This document describes how JAKOVA-NET treats a Martian colony as just another “universe” on the same BIOS + JSON + engines stack.

For the formal record of this project, see:  

- **JAKOVA-NET: Martian Project X – Local-First Colony Stack for Mars**  
  DOI: `10.5281/zenodo.17870481`

Zenodo is the canonical, citable spec. This doc is the repo-side blueprint that shows how it plugs into the OS.

---

## 1. Design goals

Martian Project X is built to satisfy four constraints:

1. **Local-first, survivable stack**  
   - Colony must keep running if cut off from Earth network and cloud services.  
   - Full state (colony layout, assets, synth roles, governance) is in one JSON state file on local hardware.

2. **Guardrailed automation, human sovereignty**  
   - Synths (AI systems, robots, planners) can optimise, route, and refactor – but do not own the colony.  
   - Human operators remain canonical source of law, values, and final veto.

3. **Composable, forkable universes**  
   - “Mars City C137” is one universe configuration.  
   - Alternate histories / layouts (C138, C139…) are new JSON state files on the same BIOS + engines.

4. **Cyberpunk-era realism, not fantasy**  
   - Assumes messy politics, uneven infrastructure, and high-risk edges.  
   - The stack is designed for partial deployment (one lab, one fab, one habitat) as well as full cities.

---

## 2. Stack overview

Martian Project X reuses the global JAKOVA-NET pattern:

1. **Model as BIOS (LLM layer)**  
   - Boots the system, interprets the JSON state, and suggests mutations.  
   - Never silently overwrites human-owned data.  
   - All policy / governance reasoning is traceable back to text specs (this repo + Zenodo).

2. **JSON state as event horizon**  
   - Single canonical state file for a given universe, e.g. `mars_city_c137.json`.  
   - Stores:
     - colony meta (name, epoch, reality tag)  
     - environment (sites, domes, terrain tiles)  
     - infrastructure (power, life support, transport)  
     - synth instances and roles  
     - guardrail hooks (what rules apply, where)

3. **Engines as lenses**  
   - **Fractal Voyager Engine (FVE)** – cosmos / colony visualisation, planning views.  
   - Future engines:  
     - robotics / fabrication control  
     - simulation / digital-twin  
     - logistics, civics, and emergency response dashboards.

The important part: engines are replaceable. The JSON + BIOS layer is the stable spine.

---

## 3. Colony phases

Project X is structured into phases that map cleanly to JSON universe versions.

### Phase 0 – Simulation & blueprints (Earth)

- Run Mars universes locally on commodity hardware (e.g. GL73 laptop).  
- FVE renders surface tiles, habitats, power spines, and traffic as a “tiny local cosmos”.  
- Synths exist only as planning agents – they make suggestions, not commits.  
- Output: a sequence of JSON snapshots that converge on feasible early-city layouts.

### Phase 1 – Pathfinder habitat stack

- Deploy a minimal JAKOVA-NET node in one habitat / lab on Mars:  
  - local storage with the current Mars universe state  
  - on-site engines for monitoring and planning  
  - tight guardrail profile (no autonomous heavy-equipment control yet)
- Earth and Mars stay in sync through versioned JSON snapshots, not opaque black-box models.

### Phase 2 – First City (C137 spine)

- Promote a single configuration to “First City Canonical”: `mars_city_c137`.  
- State file now includes:
  - distributed power & life support  
  - multiple habitats / districts  
  - registered synths with explicit roles and limits  
  - governance objects (charters, councils, incident logs)
- Engines may now act on physical infrastructure where explicitly granted (e.g. route rovers, power loads, printers).

### Phase 3 – Expansion & forks

- Additional universes fork from C137:
  - alternate layouts, experimental districts, or different governance models.  
- Some forks remain purely simulated; others become candidates for real deployment.  
- Guardrails require that any live fork:
  - declares lineage from a known canonical universe, and  
  - passes explicit human review before controlling real hardware.

---

## 4. Synths on Mars: classes and limits

In this project, “synths” are AI-driven entities (software agents, control systems, or embodied robots) registered as objects in the JSON state.

### 4.1 Synth classes

Suggested initial classes:

- **INFRA-SYNTH** – infrastructure & maintenance  
  - power routing, life-support tuning, thermal management  
  - proposal engine for maintenance schedules and upgrades

- **CIVIC-SYNTH** – civic data & planning  
  - monitors habitat occupancy, resource usage, and public feedback  
  - proposes zoning changes, expansion plans, and policy tweaks

- **FRONTIER-SYNTH** – exploration & science  
  - route planning for rovers / drones  
  - risk-aware sampling, drill sites, and off-city excursions

- **FAB-SYNTH** – manufacturing & embodiment  
  - 3D printer queues, toolpath optimisation, spare-parts inventories  
  - tied closely to robotics / fab engines, never free-running

Each synth instance has:

- a unique ID  
- a class (one of the above)  
- a scope (which assets / districts it can see)  
- a permissions profile (which actions it may request vs execute)

### 4.2 Guardrail lattice (high-level)

Guardrails are a first-class part of the universe state, not an add-on.

Minimal lattice for Mars:

1. **Authority guardrails**
   - No synth may commit changes to governance objects (charter, law, rights) – proposals only.  
   - Any change that moves resources between humans (ownership, housing, rationing) requires explicit human sign-off.

2. **Physical-risk guardrails**
   - Hard blocks on actions that can cause rapid loss of life (power-to-zero on a whole district, airlock overrides, etc.)  
   - Synths may raise alarms and propose mitigations but cannot silence alarms.

3. **Scope & logging**
   - Every synth action is attributable and logged in the JSON state (or an attached log), including who / what approved it.  
   - Scopes are minimal by default; expansions are explicit changes to state, not silent internal drift.

4. **Fork guardrails**
   - Live colonies can only run universes derived from a signed, human-approved canonical snapshot.  
   - Experimental forks are clearly tagged as non-live, even if they share engines and hardware.

For deeper ideology / ownership details, see `docs/ideology.md` and the Zenodo ideology spec.
 
---

## 5. Universe files for Mars

For Martian Project X, we standardise on:

- `fve/examples/tiny_local_cosmos.json`  
  – existing minimal cosmos example.

- `fve/examples/mars_city_c137.json`  
  – First City canonical seed for Mars.  

The Mars file should, at minimum, encode:

- top-level meta:
  - `"universe_id": "MARS_CITY_C137"`  
  - `"epoch": "phase-1"` / `"phase-2"` etc.  
  - `"reality": "sim"` or `"live"`

- camera / view defaults for FVE  
- arrays of:
  - `sites` (named locations with coordinates / elevation)  
  - `structures` (habitats, domes, tunnels…)  
  - `infrastructure` (power, air, water, comms)  
  - `synths` (instances with class + permissions)  
  - `guardrails` (which lattice rules apply where)

As the schema stabilises, the Mars JSON must stay compatible with `fve/state-schema.v0.json` and any future schema versions.

---

## 6. Ownership and contributions

- Canonical authorship for Martian Project X is currently:

  - **Jak Evans (JAKOVA-NET)** – OS + colony architecture  
  - JAKOVA-NET AI systems – assistance, not legal authors

- Formal citations should use the Zenodo DOI: `10.5281/zenodo.17870481`.

- Contributions to this repo **do not** transfer ownership of the Martian Project X concept.  
  - Contributors are credited for code, schemas, and engineered artefacts.  
  - The ideological / narrative backbone remains version-controlled under JAKOVA-NET Prime.

To propose changes:

1. Open a GitHub issue or PR referencing the relevant Zenodo DOI and universe file(s).  
2. Clearly mark whether your proposal targets:
   - schema / code,  
   - colony layout / logistics, or  
   - governance / ideology (which requires an extra layer of review).

---

## 7. Status

- Zenodo spec: **live** (`10.5281/zenodo.17870481`)  
- Repo docs: this file (blueprint), plus `architecture.md`, `ideology.md`, and `fractal-voyager-engine.md`.  
- Universe files:
  - `tiny_local_cosmos.json` – done  
  - `mars_city_c137.json` – **planned** (v0 template to be added under `fve/examples/`)

Once `mars_city_c137.json` lands, the Martian colony becomes just another bootable universe in the JAKOVA-NET stack – same BIOS, different sky.
