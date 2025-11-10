# Local macOS Development Instructions (Anthonium)

See also: `.github/instructions/cross-platform-instructions.md` for shared steps.

- Meta repo: `~/Developer/unchromed-anthonium`
- Chromium src: `~/Developer/chromium/src`
- depot_tools: `~/depot_tools`

1) Install Xcode (full) and run once. If Metal errors:
```bash
xcodebuild -downloadComponent MetalToolchain
```

2) Add depot_tools to PATH (zsh):
```bash
if [[ ":$PATH:" != *":$HOME/depot_tools:"* ]]; then export PATH="$HOME/depot_tools:$PATH"; fi
```

3) Fetch & sync Chromium:
```bash
mkdir -p ~/Developer/chromium && cd ~/Developer/chromium
fetch chromium
cd src && gclient sync
```

4) GN + build:
```bash
gn gen out/Default --args='is_debug=true is_component_build=true use_siso=true'
autoninja -C out/Default base_unittests
# then
autoninja -C out/Default chrome
```
