# JAKOVA-NET Glossary

Short, practical definitions for the core JAKOVA-NET vocabulary.

---

## Core OS concepts

**JAKOVA-NET**  
Local-first AI operating system pattern. Model runs as BIOS, not as a hosted web app. One JSON state file on disk, many “universes” rendered by different engines.

**Model as BIOS**  
The LLM behaves like firmware:

- boots the system
- helps decide how to mutate the JSON state
- never owns the user’s world or data

**JSON state file (event horizon)**  
Single canonical state on disk that describes the current “universe”:

- metadata (universe id, title, version)
- camera (mode, position, target, FOV)
- objects (id, type, position, scale, labels, data)

Change the JSON, the universe changes. Engines are just lenses.

**Engines as lenses**  
Any runtime that can read the state file and render / act on it:

- Python backend (simulation, rules, routing)
- Unity viewer (3D/4D visualisation)
- Future engines (robot control, printers, factories, dashboards)

None of them are the source of truth; they only project the JSON.

---

## Governance & power routing

**Prime Core**  
The ideological and governance backbone for JAKOVA-NET. Specifies ownership of ideologies, attribution rules, and who is allowed to change what.

**Ideology objects**  
Ideologies treated as first-class objects inside the OS (like files), not free-floating memes. They have owners, versions, and explicit routing rules.

**EXAWATTS**  
Lightweight work-class and power-routing layer for personal multi-AI operating systems. Answers: “Which agent is allowed to do which kind of work, on behalf of whom, and when?”

**Work-class**  
A labelled class of tasks (e.g. “file ops”, “research”, “hardware”, “social ops”) with clear safety and routing constraints.

**Black hole recycle node**  
Design metaphor for recycling entropy: legacy ideas / noise / overspill get compacted and turned into useful exawatt “fuel” instead of being deleted or left to rot.

---

## Cross-scale theory

**EBNT (Evans-Barboza Network Theory)**  
Cross-scale framework that treats many networks (cosmic filaments, neural networks, social graphs, infrastructure) as having shared structural invariants.

**Tiny local cosmos**  
Minimal example universe used in the Fractal Voyager Engine: a very small JSON state that still obeys the same pattern as much larger worlds.

---

## Fractal Voyager Engine (FVE)

**Fractal Voyager Engine (FVE)**  
Demo engine for JAKOVA-NET v1.0:

- Python backend: loads/mutates the JSON
- Unity viewer: renders stars/objects from the same file
- Swappable skins: same pattern could represent robots, printers, factories, etc.

**Universe schema**  
The JSON “shape” that FVE expects. Tracked in `fve/state-schema.v0.json`.

**Example universes**

- `fve/examples/tiny_local_cosmos.json` – minimal demonstrator.
- Future examples: lab, logistics, robotics, printer/factory views.

---

## Meta & process

**Local-first**  
All critical state lives on your machine:

- no hard dependency on a cloud DB
- system can survive network loss
- user keeps ownership of their world

**C137 canonical**  
The “no-bullshit” spec layer: what the OS is *actually* allowed to be. Vibes live elsewhere; C137 is the canonical reference.

**Loop mesh / lattice**  
Routing pattern for work and governance changes: who can propose, who can veto, and how changes ripple through dependent systems.
