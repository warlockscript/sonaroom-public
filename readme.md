# 🎵 Sonaroom

**3D Acoustic Simulator**

A professional, cross-platform 3D acoustic simulation and room modeling tool built with Python and PySide6. Designed for acoustic engineers, architects, and audio professionals to visualize, simulate, and optimize room acoustics in real-time.

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![PySide6](https://img.shields.io/badge/UI-PySide6-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## ✨ Key Features

- **🎨 Sleek, Modern UI**: Ultra-compact, borderless 11px Material Design theme with seamless Light/Dark mode toggling.
- **🔄 Auto-Simulate Propagation**: Changing a surface material instantly recalculates and redraws acoustic ray paths in the 3D viewport without manual intervention.
- **🎯 3D-to-Panel Synchronization**: Click any surface (Floor, Walls, Ceiling) in the 3D viewport, and the Side Panel will automatically scroll to and highlight the corresponding material dropdown.
- **💾 Persistent Preferences**: User settings (theme, default materials, calculation speed) are automatically saved to disk and restored on startup using `QSettings`.
- **📊 Comprehensive Acoustic Tools**: 
  - Room Configuration & Custom Room Builder
  - 9-Band Material Absorption Database
  - Ray-Tracing Propagation & Heatmap Visualization
  - AI Optimizer & Measurement Panels
  - Phase 5: Integrated Auralization Engine & Client-Ready PDF Report Generation.

---

## 🛠️ Tech Stack

- **Language**: Python 3.10+
- **GUI Framework**: PySide6 (Qt for Python)
- **3D Rendering**: PyVista / VTK
- **Math & Data**: NumPy, SciPy
- **State Management**: Custom `ProjectState` with JSON serialization

---

## 🚀 Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/warlockscript/3d-Room-Acoustic-Designer.git
cd 3d-Room-Acoustic-Designer
```

### 2. Create the environment and install
```bash
python -m venv venv
venv\Scripts\python.exe -m pip install -r requirements.txt
```

### 3. Run
```bash
venv\Scripts\python.exe -m app.main
```

---

## 🧪 Tests

All tests, each file in its own process (no pytest needed):
```bash
venv\Scripts\python.exe tests\run_all.py
```

Only files whose name contains a word, e.g. `heatmap`:
```bash
venv\Scripts\python.exe tests\run_all.py heatmap
```

The window tests open the real main window off-screen; they never touch your
saved preferences or your material database. What the tests cover, and what
is still open, is in [docs/audit-2026-10.md](docs/audit-2026-10.md).

---

## 📦 Building a release

**Windows** — the program folder, a zip, and an installer (if
[Inno Setup 6](https://jrsoftware.org/isinfo.php) is installed):
```bash
build_release.bat
```
`build_release.bat quick` skips the tests. It builds in its own venv,
`.venv-build` (your `venv` is not touched), with Python 3.12.1 or newer —
found with `py -3.12` or uv (`uv python install 3.12`), or named in
`BUILD_PYTHON`. Python 3.12.0 cannot be used: a bug in it breaks scipy in the
packaged program. The built program checks itself (`--self-test`) before it
is zipped. Output in `dist\`:
`Sonaroom-<ver>-windows-x64.zip` and `…-windows-x64-setup.exe`.

**Linux** — `.deb`, `.rpm` and `.tar.gz`, on Linux or in WSL (PyInstaller
cannot build for another OS):
```bash
bash packaging/build_linux.sh
```
Needs `python3-venv` and `binutils`; `rpm` (Debian/Ubuntu) or `rpm-build`
(Fedora) for the `.rpm`; `xvfb` is best for the tests (else the desktop
display is used). All install to `/opt/sonaroom` with a
`sonaroom` command and a menu entry.
