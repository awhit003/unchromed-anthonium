# Build chain test on Windows

## Windows build: minimal, reliable checklist

1) Visual Studio 2022 + Windows SDK
- Required:
  - Workload: Desktop development with C++
  - Components:
    - MSVC v143 – VS 2022 C++ x64/x86 build tools
    - Windows 11 SDK 10.0.22621.x (keep this one; newer SDKs can coexist)

2) System and Git settings

- Enable long paths system-wide
- Git long paths (avoid path issues in Chromium)

Reboot may be needed for the OS long paths change.

3) Python, Git, depot_tools
- Install Python 3.10+ and Git (if not already).
- Clone depot_tools and add to PATH:

4) Fetch and sync Chromium (Windows)

5) Generate build files with GN
- is_component_build=true speeds linking for iterative builds.
- You can switch to a Release (is_debug=false) full static link later.

6) Smoke test a small target

7) Build Chrome

If anything fails, grab the tail of the log and the failing step.

## Pull this from GitHub first

If you're setting up a fresh Windows machine, start by cloning this repo:

- Via VS Code: open "Source Control" → "Clone Repository" → paste https://github.com/awhit003/unchromed-anthonium and choose a local folder (e.g., `C:\src\unchromed-anthonium`).
- Or via PowerShell:
  - `git clone https://github.com/awhit003/unchromed-anthonium C:\src\unchromed-anthonium`
  - `cd C:\src\unchromed-anthonium`

Then follow the checklist above on the same host to install VS, SDK, Python, Git, and `depot_tools`.

## Spin up a clean Windows VM in Hyper‑V (optional, recommended for reproducibility)

Prereqs: Windows 11 Pro/Enterprise on the host, Hyper‑V enabled, and sufficient disk/CPU.

High-level steps:
- Create a new virtual switch in Hyper‑V Manager (External or Default depending on your network needs).
- Create a new Generation 2 VM:
  - 4–8 vCPU, 16–32 GB RAM (adjust based on host resources)
  - VHDX size ≥ 200 GB (Chromium checkout + build artifacts are large)
  - Attach a Windows 11 ISO and install the OS.
- After first boot:
  - Enable long paths and install Windows Updates.
  - Install Visual Studio 2022 components listed above (MSVC v143 + Windows 11 SDK 10.0.22621.x).
  - Install Git and Python 3.10+.
  - Clone `depot_tools` and add it to PATH.
  - Clone this repo and proceed with fetch/sync/build steps.

Tips:
- Snapshot (Checkpoint) the VM after you finish installing toolchains so you can revert quickly for clean builds.
- Consider placing the Chromium checkout on a dedicated VHDX to manage storage separately from the OS disk.
