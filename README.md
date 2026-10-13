# Sonaroom

**3D Acoustic Simulator**

Model the room in 3D, see how long it rings in every octave band, place real
acoustic panels, hear the room before and after, and check the prediction
against a measurement from [Sonasync](https://sonasync.alphabellsystems.com/).

**Website:** https://sonaroom.alphabellsystems.com/

## Download

Get the latest version from the
[Releases page](https://github.com/warlockscript/sonaroom-public/releases/latest).

| File | What it is |
|---|---|
| `Sonaroom-<version>-windows-x64-setup.exe` | Installer for Windows 10 / 11 (64-bit). No administrator rights needed. |
| `Sonaroom-<version>-windows-x64.zip` | The same program without installing: unzip and run `Sonaroom.exe`. |
| `sonaroom_<version>_amd64.deb` | Debian, Ubuntu, Mint: `sudo apt install ./sonaroom_<version>_amd64.deb` |
| `sonaroom-<version>-1.x86_64.rpm` | Fedora, openSUSE, RHEL: `sudo dnf install ./sonaroom-<version>-1.x86_64.rpm` |
| `Sonaroom-<version>-linux-x86_64.tar.gz` | Any Linux: unpack and run `Sonaroom/Sonaroom` |
| `sonaroom_export-<version>.rbz` | The SketchUp 2026 extension: exports your SketchUp room to Sonaroom |

Sonaroom is not code-signed yet, so Windows may show *"Windows protected your
PC"* on first run. Click **More info → Run anyway**.

## What it does

- **Build the room in 3D**: a box or a custom shape, with a material on every surface - or **import it from SketchUp** with its materials, in metres
- **Reverberation per octave band**: Sabine and Eyring (with air absorption), image sources and ray tracing
- **Acoustic treatment with real products**: place panels on walls and ceiling by hand; click one to set its **air gap** (cm), **tilt** and turn, or hang it as a **ceiling cloud** that absorbs on both sides
- **Auralization**: listen to the room before and after treatment
- **Sonasync import**: read a measured room impulse (EDT, T20, T30, C50, C80, D50 per band) and compare it with the prediction
- **Reports** in PDF and HTML

## Using it with Sonasync

Install both on the same computer. In Sonasync, export the room's impulse; in
Sonaroom, open the Measurement panel and choose **Import room impulse from
Sonasync**. The folder is found for you.

## Using it with SketchUp

1. In SketchUp: Extension Manager > Install Extension > `sonaroom_export-<version>.rbz`. The extension
   is not signed yet, so first set Extension Manager > Loading Policy to **Unrestricted**.
2. Name a component **Sonaroom Source** and one **Sonaroom Listener** where they are in the room.
3. Extensions > Sonaroom > **Export room to Sonaroom**, and pick the Sonaroom material for each
   SketchUp material (remembered with the model).
4. In Sonaroom: File > **Import SketchUp room**.

## Feedback

This is a beta. Bug reports, questions and measured rooms are welcome:
masterpro0115@gmail.com, or open an issue here.

## Licence

Sonaroom is proprietary software, © 2026 Master Pro Sounds and Lights
Services. The beta is free to use; it may not be redistributed or resold.
The full licence (`LICENSE.txt`) and the notices for the open-source
libraries it includes (`THIRD-PARTY-NOTICES.txt`) come with the program.
