
# Anthonium (Custom Chromium)

A customized version of the Chromium browser with feature parity to the official release while ensuring compliance with all relevant licenses.

## Project Objective

To create a personalized fork of the open-source Chromium web browser. The project will be named "unchromed-anthonium".

- The browser is rebranded to be refered to as simply "anthonium" inside and outside of the application.
- will maintain feature parity with Chromium while not referencing `chromium` or `chrome` or `google` outside of documentation.
- The custom branding assets are the terminal alias `ua` primarily, standing for the "unchromed-antonium" name, and a solid black square for an icon.

## Current Status & Base

Base Code: The main Chromium repository source code has been checked out (src/ directory is locally available).

Development Platforms:

- macOS (using depot_tools)
- Win11 (using Visual Studio 2022)

Target Platforms:

- macOS,
- Windows 11.

Build State:
- Build environment is configured and ready for the initial gn gen and autoninja process on macOS.
- Build environment is awaiting verification that it is configured and ready for the initial gn gen and autoninja process on Windows 11.

### Key Locations (Host Paths)

- Meta repo (this repository): macOS `~/Developer/unchromed-anthonium`, Windows `C:\src\unchromed-anthonium`
- Chromium checkout root: macOS `~/Developer/chromium`, Windows `C:\src\chromium`
- Chromium source tree: `.../chromium/src`
- depot_tools: macOS `~/depot_tools`, Windows `C:\src\depot_tools`


## Immediate Technical Task

The immediate goal is to successfully execute the first build of a rebranded application, "anthonium," from the Chromium source. This involves google checkout in a way I don't understand, yet.

Once the basic fork is stable and rebranded, the features will be integrated in subsequent phases.

## Endstate Vision

The final product will be a fully functional web browser that makes no reference to chrome, chromium, or google, outisde of the licensing documentation, that is customized.

## Contributing & Sync Workflow (High-Level)

1. Pull latest: `git pull origin main`
2. Make changes in this meta repo (branding docs) separately from Chromium source edits.
3. Rebrand changes occur under the Chromium checkout (`chromium/src/...`). Keep those patches small & well-commented with upstream license headers retained.
4. Build & test on macOS, then replicate on Windows. Or, the other way around.
5. Commit & push: `git add -p && git commit -m "<message>" && git push origin main`.
