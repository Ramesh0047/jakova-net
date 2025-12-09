# JAKOVA-NET

**JAKOVA-NET is a local-first AI operating system that treats the model as BIOS, not an app.**

Instead of “AI as a website”, JAKOVA-NET runs as a **stateful OS pattern** on local hardware:

- one JSON state file on disk
- a set of engines (Python, Unity, etc.) that read that state
- the model acts as BIOS / firmware, not a remote API

Swap the JSON file and the same engines can render different “universes” on top of the same underlying model + state:
stars, factories, printers, datasets, social graphs – same pattern, new skin.

---

## Current demo: Fractal Voyager Engine (FVE)

**Fractal Voyager Engine (FVE)** is the first live demo of the JAKOVA-NET pattern:

- Python backend
- Unity cosmos viewer (3D/4D-style space view)
- Driven by a single JSON state file on a 2019 MSI GL73 laptop
- Fully local-first: no cloud dependency for core logic

Right now, the JSON state holds a tiny local cosmos:

- `meta` – universe ID, title, version
- `camera` – mode, position, target, FOV
- `objects[]` – id, type, position, scale, labels, data

The **same engine** could just as easily load robots in a factory, vehicles in a depot, or printers in a lab instead of stars.
The JSON is the universe; engines are just lenses.

---

## Design philosophy

### Local-first by default

- The model runs **as close to the metal as possible**.
- Core state lives on disk, under the user’s control.
- Network loss should change convenience, not reality.

### Model as BIOS, not app

- The LLM is treated like **firmware / BIOS**:
  - boots the system
  - helps decide how to mutate the JSON state
  - does not own the user’s world or data

### OS, not app

JAKOVA-NET is an **operating system pattern**, not a single product.

- You can run different “universes” (cosmos, lab, logistics, etc.) on top of the same pattern.
- Governance, ownership, and safety are handled at the OS layer, not bolted on as an afterthought.

### Ideology & ownership

The ideological backbone lives in a separate, citable spec:
[JAKOVA-NET Prime: Ownership of Ideologies](https://doi.org/10.5281/zenodo.17861175).

Short version:

- Ideologies are treated as objects inside the OS, not free-floating memes.
- Attribution, ownership, and routing are explicit.
- The goal is **human-owned, accountable AI systems**, not anonymous black boxes.

---

## Repository layout

```text
.
├── README.md                # You are here
├── LICENSE                  # MIT, open to fork and experiment
├── CITATION.cff             # How to cite this repo
├── .gitignore               # Python + Unity + editor noise
├── CODE_OF_CONDUCT.md       # Community expectations
├── CONTRIBUTING.md          # How to propose work
├── SECURITY.md              # Security / safety contact
│
├── docs/
│   ├── architecture.md          # OS architecture (model-as-BIOS, JSON state, engines)
│   ├── ideology.md              # Ownership / governance overview
│   ├── fractal-voyager-engine.md# FVE demo notes
│   ├── roadmap.md               # High-level milestones
│   └── glossary.md              # Core terms (BIOS, exawatts, EBNT, etc.)
│
└── fve/
    ├── README.md                # FVE demo: what it is, how it works conceptually
    ├── state-schema.v0.json     # Draft JSON schema for universe state
    └── examples/
        └── tiny_local_cosmos.json   # Minimal example universe

## License

This repository is released under the MIT License.  
See [`LICENSE`](./LICENSE) for details.
