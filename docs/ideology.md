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

# Ideology & Ownership (JAKOVA-NET Prime)

This file is a human-readable bridge to the full spec  
**“JAKOVA-NET Prime: Ownership of Ideologies”** (see Zenodo for the citable version).

## 1. Why bother with ideology?

Most systems treat “ideas” as free-floating content:

- memes
- prompts
- config files
- ad-targeting fodder

JAKOVA-NET treats **ideologies as objects** inside the operating system:

- they have IDs
- they have owners
- they have routing rules

You cannot route power through an ideology without knowing where it came from and who is accountable.

---

## 2. Basic model

At a high level:

- An **ideology** is a structured object describing:
  - assumptions about the world
  - goals and constraints
  - safety requirements

- Ideologies can be:
  - attached to universes
  - attached to engines
  - attached to users or roles

---

## 3. Ownership

The Prime spec defines:

- how ideologies are **attributed** (who authored what)
- how credit and responsibility are assigned
- how conflicting ideologies are resolved or isolated

The intent is to avoid:

- “free idea” extraction with no credit
- anonymous governance over human lives
- opaque black-box decision-making

---

## 4. How it touches the code

Any serious JAKOVA-NET deployment should:

- treat ideologies as first-class objects in its state
- log which ideology affected which decision
- make it possible to audit decisions back to ideological inputs

For the demo phase, this repo focuses on the **state and engine pattern**.  
Prime is the guardrail that prevents that pattern being bent into another black-box.

For full detail, read the Zenodo paper and cite that in serious work.
