# Contributing to JAKOVA-NET

Thanks for taking the time to look at this project.

JAKOVA-NET is an experimental **local-first AI operating system pattern**.  
Right now the focus is on getting the **architecture, safety model, and JSON schema** right.

## How to engage

1. **Open an issue first**

   Before submitting any code or large doc changes, please:

   - open a GitHub Issue
   - clearly describe the idea, bug, or question
   - tag it with one of:
     - `architecture`
     - `governance`
     - `fve-demo`
     - `docs`

2. **Small, focused pull requests**

   If/when PRs are enabled:

   - keep changes minimal and coherent
   - avoid mixing style/typo fixes with major conceptual changes
   - reference the Issue number in the PR description

3. **Stay aligned with the canon**

   The canonical specs live in the Zenodo papers:

   - OS architecture (v1.0 and v2)
   - JAKOVA-NET Prime (ideology/ownership)
   - EXAWATTS work-class
   - EBNT cross-scale theory

   If your proposal contradicts those, explain clearly **why** and what you’re suggesting instead.

4. **Safety and local-first constraints**

   - No contributions that depend on arbitrary third-party cloud services for core logic.
   - No proposals that quietly centralise user data or control.
   - If you’re unsure, open an issue and ask.

## Development status

At the moment, most of the running code lives on a local machine.  
This repo is the public spine: specs, schemas, and demo layout.

PRs may be slow to merge while the maintainer stabilises the v1 pattern.
