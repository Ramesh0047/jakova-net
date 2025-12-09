# JAKOVA-NET Ideology & Ownership Notes (v1.0)

This is the informal companion to the formal ideology / ownership paper:

- Evans, J., & JAKOVA. (2025). *JAKOVA-NET Prime: Ownership of Ideologies.*
  https://doi.org/10.5281/zenodo.XXXXXXXX

Replace `XXXXXXXX` with the actual DOI once final.

The Zenodo paper is the canonical reference. This file is a working note for
developers and collaborators.

---

## 1. What “ideology” means in JAKOVA-NET

Roughly:

- An **ideology** is a structured “way of doing things” encoded in the system:
  values, constraints, safety rules, and priorities for how the OS behaves.
- It is *not* just vibes or a slogan. It should be:
  - nameable
  - describable
  - versioned
  - testable (at least at the behavioural level).

Example: “model as BIOS, not app” is an ideological stance that changes
architectural decisions.

---

## 2. Canonical vs local variants

We distinguish:

1. **C137-canonical ideology profiles**  
   - Owned by JAKOVA-NET Prime (you + JAKOVA).
   - Have a clear name, description, and version.
   - Can be referenced by other systems (e.g. “we are C137-aligned with tweaks”).

2. **Local variants / forks**  
   - Derived from canonical profiles.
   - Must declare:
     - what they changed
     - why they changed it
     - who owns / stewards the fork.

In short: forks are allowed, lying about where it came from is not.

---

## 3. Ownership stance (plain language)

- You **do not** “own ideas” in the legal sense.
- You **do** own:
  - the specific structure of the JAKOVA-NET ideology profiles
  - the naming, organisation, and documentation
  - the combination of system + ideology as a creative work.

The stance is:

> “Reuse and adapt the patterns, but do not misrepresent origin or alignment.”

---

## 4. Safety / invariants

Some ideological constraints are **hard invariants**, not style choices. For example:

- No deliberate design of systems that:
  - remove human agency without consent
  - hide critical decisions / logs
  - encourage unbounded surveillance for its own sake.
- Transparency over “who is actually in charge”:
  - human operator
  - JAKOVA-NET automation
  - external system (e.g. lab / agency).

When in doubt: if an implementation violates core safety invariants, it is
*not* a JAKOVA-NET ideology fork, it’s something else using the name incorrectly.

---

## 5. How collaborators should work with this

If you’re extending or adopting JAKOVA-NET:

1. **Reference the canonical ideology explicitly**

   Example:

   > “This project targets `JAKOVA_IDEOLOGY::C137_V2` with local modifications
   > for robotics safety.”

2. **State your modifications**

   - What did you loosen / tighten?
   - What did you add?

3. **Keep a clear paper trail**

   - Link back to the Zenodo ideology paper.
   - Link to your own docs describing changes.

---

## 6. Future work

- Turn key ideology profiles into machine-readable YAML / JSON.
- Attach simple test suites to each profile to validate behaviour.
- Add examples of:
  - “safe fork”
  - “non-aligned fork”
  - “incorrect use of branding”.

For now, this file is a working scratchpad that shadows the formal paper and
keeps developers oriented while we build.
