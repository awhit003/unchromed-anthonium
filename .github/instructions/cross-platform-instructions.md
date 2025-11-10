# Cross‑Platform Build Instructions (Anthonium)

These device-agnostic instructions outline the common flow for building Anthonium (Chromium-based) on macOS and Windows, with a Windows addendum.

## 1. Repositories & Key Locations

- Meta repo (branding/docs):
  - macOS: `~/Developer/unchromed-anthonium`
  - Windows: `C:\src\unchromed-anthonium`
- Chromium checkout:
  - macOS: `~/Developer/chromium/src`
  - Windows: `C:\src\chromium\src`
- depot_tools:
  - macOS: `~/depot_tools`
  - Windows: `C:\src\depot_tools`

## 2. Tooling Overview

- depot_tools provides `gclient`, `gn`, `autoninja`
- Chromium uses its own clang toolchain; platform SDKs (Xcode/Windows SDK) provide system headers/libs

## 3. Common Steps

1) Clone this meta repo
- macOS: `git clone https://github.com/awhit003/unchromed-anthonium ~/Developer/unchromed-anthonium`
- Windows: `git clone https://github.com/awhit003/unchromed-anthonium C:\src\unchromed-anthonium`

2) Install `depot_tools` and add to PATH
- macOS PATH: prepend `~/depot_tools`
- Windows PATH: append `C:\src\depot_tools`

3) Create Chromium workspace and fetch
- macOS: `mkdir -p ~/Developer/chromium && cd ~/Developer/chromium && fetch chromium`
- Windows: `mkdir C:\src\chromium && cd C:\src\chromium && fetch chromium`

4) Sync dependencies
- `cd src && gclient sync`

5) Generate build files
- `gn gen out/Default --args="is_debug=false is_component_build=true target_cpu=\"x64\""`

6) Build a small target, then the browser
- `autoninja -C out/Default base_unittests`
- `autoninja -C out/Default chrome`

## 4. macOS Notes

- Full Xcode required; if Metal errors occur, run: `xcodebuild -downloadComponent MetalToolchain`
- Consider `use_siso=true` for faster local builds

## 5. Windows Addendum

- Install Visual Studio 2022 (Community or Build Tools) with:
  - "Desktop development with C++" workload
  - MSVC v143 (x64/x86) build tools
  - Windows 11 SDK 10.0.22621.x
- Enable long paths:
  ```powershell
  reg add HKLM\SYSTEM\CurrentControlSet\Control\FileSystem /v LongPathsEnabled /t REG_DWORD /d 1 /f
  git config --global core.longpaths true
  ```
- Optional: Use Hyper‑V to create a clean VM for reproducible builds; allocate ≥ 200 GB VHDX, 16–32 GB RAM, 4–8 vCPU.

## 6. Where things live (quick reference)

- macOS
  - Repo: `~/Developer/unchromed-anthonium`
  - depot_tools: `~/depot_tools`
  - Chromium src: `~/Developer/chromium/src`
- Windows
  - Repo: `C:\src\unchromed-anthonium`
  - depot_tools: `C:\src\depot_tools`
  - Chromium src: `C:\src\chromium\src`

## 7. Troubleshooting

- Check `out/Default/siso_output` or Ninja logs for failing actions
- Verify PATH resolves `gclient`, `gn`, `autoninja`
- Ensure disk space: ≥ 150 GB free before first full build

---
(Scaffold v1 — extend with rebranding file paths and platform‑specific quirks as discovered.)
