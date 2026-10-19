# 🎵 Sonaroom

**3D Acoustic Simulator**

A professional, cross-platform 3D acoustic simulation and room modeling tool built with Python and PySide6. Designed for acoustic engineers, architects, and audio professionals to visualize, simulate, and optimize room acoustics in real-time.

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![PySide6](https://img.shields.io/badge/UI-PySide6-green.svg)
![License](https://img.shields.io/badge/License-Proprietary-lightgrey.svg)

---

## 🆕 New in 0.3.3

0.3.2 was never published; 0.3.3 includes everything listed here.

- **Facing**: the source and listener show which way they face, on a map-like compass (front wall
  south, back wall north, left west, right east; N/S/E/W round the room). Click either in the 3D view,
  drag the blue ring to turn it and the yellow arrow tip to tilt it (Shift snaps 15°, R resets, one
  Ctrl+Z per change), or set Turn / Tilt, *Reset* and *Face the listener / source* in their panels.
  Default: source faces south, listener north. The sound does not use it yet (binaural is next).
- **Draw Room undo**: Ctrl+Z undoes a drawn room, a Draw Room setting or going back to a rectangular room.
- **Binaural groundwork**: both engines record where each reflection arrives from, and the SADIE II
  KU100 HRTF set (Apache 2.0) ships in `app/data/hrtf`. Nothing sounds different yet.
- **Walk-through auralization**: the listener walks a path once at up to a brisk 1.8 m/s while the audio
  plays - a straight X/Y line, or one drawn with the mouse in any 3D view (Ctrl for straight stretches),
  any length - crossfading between room responses every 0.5 m (at most 120 points). The listener's pin
  walks it in 3D with the sound and stops when it stops; Reset path clears it. Time estimate, Cancel,
  and Export Walk Audio as a WAV. Mono.
- **Propagation by material**: each ray loses the surface's absorption at every bounce and is coloured
  by its strength (bright yellow strong, dim purple weak) - concrete keeps it, acoustic treatment soaks
  it up. SketchUp rooms are now animated as drawn, with their matched materials.
- **Material Database Editor**: the plot shows the calculated absorption (and transmission loss on its
  own axis); NRC/SAA/STC are saved. Saved materials appear in the Product Library under *My Materials*.
- **3D view**: turntable orbit about the vertical axis - it no longer rolls on its side.
- **Heatmap**: SketchUp rooms of any shape leave out points outside their walls.

## New in 0.3.0

- **Draw Room**: Room > Draw Room draws the walls in the 3D view as a top plan - click each corner, type
  a length in cm for an exact wall, Shift for 0/45/90 degrees, snapping to a 10 cm grid. Walls have a
  thickness and height, with a ceiling slab and a material per wall, floor and ceiling. Replaces the
  Custom Room point canvas. 13 building and open-air materials added.
- **Sonasync's Sonaroom folder**: room impulses are read from `<Sonasync measurements>/Sonaroom`, where
  Sonasync 3.57.1 and later export them, and still from the old `RoomAcoustic 3D` folder.
- Projects saved by 0.3.0 use project format 5; 0.2.0 still opens them.

## New in 0.2.0

- **Panel Properties**: click a placed panel in 3D to select it; set its air gap from the surface (cm),
  tilt, turn, size, position, or make it a **ceiling cloud** (absorbs on both faces). Delete or right-click
  > Remove deletes it; every change is one undo step. The gap's effect on absorption is calculated from the
  material's thickness and flow resistivity.
- **SketchUp import**: the SketchUp 2026 extension in `sketchup/` (`python sketchup/build_rbz.py` makes the
  `.rbz`) exports the room with its materials, source and listener; File > Import SketchUp room reads it.
  Format: `docs/sketchup-room-format.md`.
- Product Library: Remove panels from a surface, Reset all panels. Separate windows stay in front of the
  main window. The 3D view keeps its zoom while placing panels.
- Licensing (Ed25519 licence files, 60-day demo from the first paid version; the beta locks nothing):
  `docs/ISSUING_A_LICENCE.md`.

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
  - Integrated auralization and client-ready PDF and HTML reports

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

---

## 📄 License

Sonaroom is proprietary software, © 2026 Master Pro Sounds and Lights
Services. The beta is free to use under [LICENSE.txt](LICENSE.txt); it may
not be redistributed or resold. Paid licences come with the full release.

The bundled open-source libraries keep their own licences: see
[THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt). The release build copies
their full licence texts into the program's `licenses` folder.
