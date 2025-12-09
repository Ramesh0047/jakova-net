# JAKOVA-NET

**JAKOVA-NET** is a local-first AI operating system that treats the model as BIOS, not an app.

Instead of “AI as a website”, JAKOVA-NET runs as a **stateful OS pattern** on local hardware:
one JSON state file drives a stack of engines (Python, Unity, etc.) that render different
“universes” on top of the same underlying model + state.

---

## Current demo: Fractal Voyager Engine

**Fractal Voyager Engine (FVE)** is the first live demo of the JAKOVA-NET pattern:

- Python backend
- Unity cosmos viewer (3D/4D-style space view)
- Driven by a **single JSON state file** on a 2019 MSI GL73 laptop
- Local-first: no cloud dependency for core logic

Swap the JSON and the same engine can represent:

- stars and galaxies  
- robots and factories  
- printers, vehicles or datasets  

Same pattern, different “universe skins”.

---

## Design philosophy

- **Local-first** – The model lives as close to the metal as possible.  
- **Model as BIOS** – The LLM is treated like firmware / BIOS, not a web app.  
- **OS, not app** – JAKOVA-NET is an *operating system pattern*, not a single product.  
- **Ideology explicit** – Governance, ownership, and safety are written down as specs, not vibes.

If you want the full story, read the two Zenodo papers:

1. **OS architecture** – overall design and pattern  
   - DOI: https://doi.org/10.5281/zenodo.17861175

2. **Ideology / ownership spec** – who owns the ideology, how forks stay honest  
   - DOI: https://doi.org/10.5281/zenodo.XXXXXXXX  
     _(replace `XXXXXXXX` with the new ideology DOI)_

---

## Status

This is an active, messy, *real* project:

- Hardware: single 2019 MSI GL73 laptop in Cornwall  
- Stack: Python + Unity (for now), JSON state file as truth  
- Goal: prove that a local-first AI OS pattern can scale from “one laptop” to “many worlds”

Code will be opened in stages as it stabilises. For now, this repo is the canonical
spec + landing pad.

---

## Who should care

- People building **OS-grade AI**, not just chat apps  
- Robotics / simulation folks who want LLMs as **control firmware**, not UX glitter  
- Systems / infra people obsessed with **local-first**, offline-capable stacks  
- Anyone who wants to stress-test or break a fresh OS pattern

If that’s you, open an issue or reach out on X:  
[`@JakEvan28683627`](https://x.com/JakEvan28683627)

---

## Citation

If you reference JAKOVA-NET in papers, posts or projects, please cite:

> Evans, J., & JAKOVA. (2025). *JAKOVA-NET v1.0: Local-First AI Operating System (Model as BIOS, Not App).* Zenodo. https://doi.org/10.5281/zenodo.17861175

and, for ideology / governance:

> Evans, J., & JAKOVA. (2025). *JAKOVA-NET Prime: Ownership of Ideologies.* Zenodo. https://doi.org/10.5281/zenodo.XXXXXXXX
