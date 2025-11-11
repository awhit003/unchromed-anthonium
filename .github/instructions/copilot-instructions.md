---

applyTo:
  - "src/**/*.**"
  - "~/Developer/unchromed-anthonium/**"
  - "~/Developer/chromium/**"

---

 # Unchromed Anthonium – Repository Assistant Instructions

These instructions guide GitHub Copilot (and other automated tools) on how to interpret and assist within this repository. Keep automation output aligned with the canonical locations and division of responsibility below.

## Authoritative File Responsibilities

Place guidance in the most appropriate file instead of duplicating it here:

1. `.editorconfig` – coding style (indentation, charset, line endings, etc.)
2. `CONTRIBUTING.md` – contribution workflow, architectural guidelines, code review expectations
3. `README.md` – project overview, quick start, high‑level concepts

This file is only for automation meta‑instructions (paths, environment context) and must stay concise.

## Key Source & Environment Roots

### macOS Development Environment
* Repo root: `~/Developer/unchromed-anthonium`
* depot_tools: `~/depot_tools`
* Chromium source: `~/Developer/chromium/src`

### Windows Development Environment
Details for the Windows workstation (host name FOLLY) are maintained separately to avoid duplication. See: [Folly host reference](./folly-instructions.md)

Quick reference paths (mirror of Folly doc):
* Repo root: `C:\src\unchromed-anthonium`
* depot_tools: `C:\src\depot_tools`
* Chromium source: `C:\src\chromium\src`

## Expansion & Change Policy

When adding environment nuances (e.g., platform-specific build flags, PATH caveats, shell profile snippets):
1. Prefer updating the dedicated host/platform doc (e.g., `folly-instructions.md`).
2. Link to that doc from here only if discoverability would otherwise suffer.
3. Avoid repeating multi-line instructions—centralize and reference.

## Automation Expectations

Automated suggestions SHOULD:
* Respect the directory roots above when generating relative paths.
* Avoid introducing new technology stacks without justification.
* Propose edits to the authoritative file (see list above) rather than inlining policy text into code comments.

Automated suggestions SHOULD NOT:
* Duplicate host hardware specs already in `folly-instructions.md`.
* Re-state coding style that belongs in `.editorconfig`.
* Embed lengthy architectural rationale (belongs in `CONTRIBUTING.md`).

## Changelog

v1.3 – Rewrite for clarity, added explicit link to Folly host reference, structured sections
v1.2 – Removed AI‑generated duplication
v1.1 – Added header and file categorization instructions
Scaffold v1 – Initial draft (to be extended with rebranding file paths and platform‑specific quirks as discovered)
