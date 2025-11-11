
# Windows build toolchain issues and resolutions

GitHub Copilot on the windows host `folly` says that the build toolchain test on `folly` cannot continue until these two problems are resolved.

## 🛠 Visual Studio discovery (vswhere missing)

```powershell
# Problem demo: attempt to locate Visual Studio using vswhere
$vswhere = 'C:\Program Files (x86)\Microsoft Visual Studio\Installer\vswhere.exe'
if (Test-Path $vswhere) {
  & $vswhere -products * -requires Microsoft.VisualStudio.Component.VC.Tools.x86.x64 `
    -property installationPath,installationVersion -format value
} else {
  Write-Host "vswhere not found: Visual Studio Installer component is missing or installation path differs."
}

# Typical output in your current environment:
# vswhere not found: Visual Studio Installer component is missing or installation path differs.

# This means depot_tools can't auto-detect the VS toolchain (cl.exe, headers, SDK).
# Confirmation that cl.exe isn't on PATH:
where.exe cl 2>$null || Write-Host "cl.exe not on PATH (need vcvarsall or proper VS install)."

# Fix options:
# 1. Re-run the Visual Studio Installer and ensure the 'Installer' folder exists (vswhere shipped).
# 2. Manually locate VS (fallback scan):
Get-ChildItem 'C:\Program Files (x86)\Microsoft Visual Studio' -Directory -Depth 3 |
  Where-Object { $_.FullName -match 'VC\\Tools\\MSVC' } |
  Select-Object -First 1 -ExpandProperty FullName

# 3. Once found, run vcvarsall to populate build env (replace <VS_ROOT>):
# & "<VS_ROOT>\VC\Auxiliary\Build\vcvarsall.bat" x64
# cl.exe /Bv
```

## 🐍 Python alias / stub issue (Microsoft Store shim on PATH)

```powershell
# Problem demo: GN or scripts invoking 'python' hit the Store alias instead of a real interpreter.
Get-Command python -ErrorAction SilentlyContinue
Get-Command python3 -ErrorAction SilentlyContinue
where.exe python 2>$null || Write-Host "python not on PATH"

# Typical output in your current environment (truncated representation):
# CommandType Name        Version
# ---------- ----        -------
# Application python.exe  0.0.0.0  (WindowsApps stub, not a full install)
# Application python3.bat 0.0.0.0  (Alias)
# C:\Users\Anthony\AppData\Local\Microsoft\WindowsApps\python.exe

# When a build script runs:
python --version
# => Python was not found; run without arguments to install from the Microsoft Store...

# That stub breaks Chromium hooks expecting a real CPython (even though depot_tools often uses vpython internally).

# Fix options:
# 1. Install a real Python (recommended):
#   - Download installer (e.g. python 3.11) from https://www.python.org/downloads/windows/
#   - Check "Add Python to PATH" during install.
# 2. Or disable the Store aliases:
#   Settings > Apps > Advanced app settings > App execution aliases
#   Turn off Python and Python3 aliases.
# 3. Verify after install:
python --version
where.exe python
# 4. Ensure depot_tools still first in PATH for vpython consistency:
$env:PATH = "C:\src\depot_tools;$env:PATH"
vpython3 -c "import sys; print(sys.version)"

# Optional: pin a specific interpreter for GN args if needed:
# setx /M PYTHONIOENCODING utf-8
```

Since I don't speak powershell fluently, please either translate this into simple english, or apply the quick fix using your integrated powershell terminal using `ssh yep@folly` [command]`.
 