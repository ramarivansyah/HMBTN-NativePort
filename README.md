<p align="center">
  <img src="logo.png" width="420" alt="Harvest Moon - Back to Nature Port by Rexaver">
</p>

<h1 align="center">Harvest Moon - Back to Nature Port by Rexaver</h1>

<p align="center"><em>No emulator. No BIOS. The game's own program, translated to C and compiled
natively - sharper, with co-op and quality-of-life options.</em></p>

An unofficial, native version of *Harvest Moon: Back to Nature* (PlayStation, USA, `SLUS-01115`) for
Windows, Linux and Android, made by **static recompilation**: the game's original PlayStation program
was translated ahead of time into C and compiled into an ordinary native program. No emulator runs the
game and no PlayStation BIOS is involved; the console's hardware (graphics and sound chips, CD drive,
controller port, memory card, geometry coprocessor, timers) is reimplemented natively.

**This repository holds the ready-to-play builds only.** The port's source code stays in a private
repository: what is here is a README, its logo and the release assets, never code, never history and
never a build script. Every build is the whole game - no disc image, no emulator and no BIOS are
needed to play.

## Contents

- [Requirements](#requirements)
- [Download](#download)
- [Install and play](#install-and-play)
- [What is in the build](#what-is-in-the-build)
- [Settings](#settings)
- [Controls](#controls)
- [Troubleshooting](#troubleshooting)
- [Version history](#version-history)
- [Credits and legal](#credits-and-legal)

## Requirements

| Platform | Needs | Asset |
|---|---|---|
| Windows | Windows 10 or 11, 64-bit | `HarvestMoonBTN-Windows-x64.zip` |
| Linux | An x86-64 distribution with glibc 2.17 or newer - Debian 8, Ubuntu 14.04 and everything since: neither the game nor the SDL2 carried beside it asks for anything newer | `HarvestMoonBTN-Linux-x64.zip` |
| Android | Android 5.0 (API 21) or newer on a 64-bit device: `arm64-v8a`, or `x86_64` for emulators and Chromebooks | `HarvestMoonBTN-Android-1.2.apk` |

- **Windows** installs nothing to play: the folder carries `SDL2.dll` next to the executable, and the
  launcher is a single `.exe` that needs no Python. `HarvestMoonBTN-Setup-<version>.exe` installs that
  same folder into `C:\Program Files` - it asks for administrator rights once, and `/CURRENTUSER`
  installs it for your account alone instead - with a Start Menu shortcut and an uninstaller, and
  leaves saves, screenshots and recordings in place when you remove it.
- **Linux**: the folder carries `libSDL2-2.0.so.0` (SDL2 2.32.10, built against glibc 2.17 like the game),
  and the game loads that copy first; when it does not load - a system whose C library is not glibc,
  such as Alpine - the game falls back to the system library, so `libsdl2-2.0-0` (Debian/Ubuntu),
  `SDL2` (Fedora) or `sdl2` (Arch) has to be installed then. If that library is too old the game names
  the missing call and stops. The launcher in the folder is `launcher.pyw`, which needs Python 3 with
  tkinter; the game itself (`./HarvestMoonBTN`) needs neither. `sh install.sh` copies the folder into
  `~/.local/share/HarvestMoonBTN` and adds a menu entry; `uninstall.sh` in that folder removes it and
  keeps your saves unless you say otherwise.
- **Android**: the package is sideloaded, not distributed on Google Play, and it is signed with a
  debug key, so Android asks you to allow installing from the app you open the file with. The data
  pack travels inside the APK, and the folder it writes to needs no permission, so the first start
  asks for nothing.

What has actually been exercised, so you know what to expect: the Windows build is the one played
through here (title screen, new game, farm, house, town, saving and loading). The Linux build passes
its data check and a headless run, but no windowed session on a Linux desktop has been run yet. The
APK installs on a phone and its settings screen was looked at; the game itself on a device, its touch
input and Vulkan on Android are still unproven. macOS and iOS are not published in this repository.

## Download

Open [Releases](../../releases/latest) and take the asset for your platform. Every asset has its
SHA-256 published beside it in a `.sha256` file.

| Asset | What it is for |
|---|---|
| `HarvestMoonBTN-Windows-x64.zip` | The game folder for Windows x64: unpack it anywhere and open `HarvestMoonBTN-Launcher.exe`. |
| `HarvestMoonBTN-Setup-<version>.exe` | The same Windows folder as an installer: run it - it asks for administrator rights once to install into `C:\Program Files`, and `/CURRENTUSER` installs it for your account alone - and open the game from the Start Menu; an uninstaller sits in the same place. |
| `HarvestMoonBTN-Linux-x64.zip` | The game folder for Linux x64: unpack it anywhere and open `launcher.pyw` (or run `./HarvestMoonBTN` directly); `sh install.sh` installs it with a menu entry instead. |
| `HarvestMoonBTN-Android-<version>.apk` | The Android package: install it on a phone and open the app. |
| `HarvestMoonBTN-Launcher.exe` | The launcher on its own, for an install you already have: the **Update** button replaces the copy in the game folder with it. |
| `<asset>.sha256` | The digest of the asset beside it, as `sha256sum` writes it: `<hex>  <name>`. |

Each game folder is the whole game - the executable, the launcher and `HarvestMoonBTN.pak` with the
game's own graphics, music and text - so no disc image, no emulator and no BIOS are needed to play.

### Checking a download

The launcher already does this for you: **Download and play** and **Update** fetch the published
`.sha256` and refuse a file that does not match it, before they unpack or replace anything. To check
one by hand:

```sh
sha256sum -b HarvestMoonBTN-Linux-x64.zip           # Linux
```
```
certutil -hashfile HarvestMoonBTN-Windows-x64.zip SHA256    :: Windows (cmd)
```

The printed digest must equal the one in the `.sha256` file of the same name.

## Install and play

Nothing is installed system-wide on Windows or Linux: the folders are portable, and where you unpack
one is where the game, its settings and its memory cards stay.

### Windows 10 or 11, x64

1. Download `HarvestMoonBTN-Windows-x64.zip` and **unpack the whole folder** - right-click, "Extract
   All", or 7-Zip. Unpacking only `HarvestMoonBTN.exe` out of the zip leaves the data pack behind and
   the game will say it cannot find the game data.
2. Open the folder and run **`HarvestMoonBTN-Launcher.exe`**. Windows may warn the first time
   ("Windows protected your PC"): the launcher is not code-signed, so choose "More info" then "Run
   anyway".
3. The Start page shows **Game found** with the path of the data pack. Press **Save and play**: the
   game opens, and settings you change are written to `hmbtn.ini` in the same folder.
4. Play. Saving is the game's own: sleep in your bed, pick one of the three diaries, and the card is
   written to `saves/card1.mcd` next to the executable.

The folder carries `HarvestMoonBTN.exe` (the game), `HarvestMoonBTN-Launcher.exe`,
`HarvestMoonBTN.pak` (the game's data), `SDL2.dll`, `hmbtn.ini`, `README.txt` and the launcher's
`launcher-assets/`. You can also run `HarvestMoonBTN.exe` directly, and open the launcher whenever
you want to change a setting.

### Linux x64

1. Download `HarvestMoonBTN-Linux-x64.zip` and unpack it: `unzip HarvestMoonBTN-Linux-x64.zip`. The
   game inside is already executable; if your unpacker dropped the permission, run
   `chmod +x HarvestMoonBTN-Linux-x64/HarvestMoonBTN`.
2. Run the game with `./HarvestMoonBTN`, or open the launcher with
   `python3 HarvestMoonBTN-Linux-x64/launcher.pyw` (it needs Python 3 with tkinter) and press **Save
   and play**. Both read `HarvestMoonBTN.pak` from their own folder.
3. Saving works the same: the card is `saves/card1.mcd` in that folder.

The folder carries `HarvestMoonBTN`, `launcher.pyw`, `HarvestMoonBTN.pak`, `libSDL2-2.0.so.0`,
`hmbtn.ini`, `LICENSE-SDL2.txt`, `README.txt` and `launcher-assets/`. If the game stops with "SDL2
was not found", install your distribution's SDL2 package - the bundled copy needs a newer C library
than an older distribution provides.

### Android 5.0 or newer

1. Download `HarvestMoonBTN-Android-1.2.apk` and open it on the phone (or `adb install -r
   HarvestMoonBTN-Android-1.2.apk` over USB).
2. Allow the install when Android asks: the package is sideloaded and signed with a debug key, so the
   phone asks you to permit installing from the app you opened the file with. It is not on Google Play.
3. Open **Harvest Moon BTN**. It starts in landscape, with an on-screen gamepad that appears when you
   first touch the screen. The data pack is inside the APK, so the first start downloads nothing.
4. Settings and saves live in the app's own visible folder, which needs no permission at all:

   ```
   /storage/emulated/0/Android/media/com.rexaver.harvestmoonbtn/HarvestMoonBTN/
     hmbtn.ini   saves/card1.mcd   screenshots/   recordings/   textures/   HarvestMoonBTN.log
   ```

   **Settings → Data → Use /HarvestMoonBTN** moves them to the easier-to-find
   `/storage/emulated/0/HarvestMoonBTN/` instead, which needs "All files access"; a restart applies it.
   The settings screen is the gear (**SET**) under L1 on the on-screen gamepad.

## What is in the build

### The original game

The same game logic, graphics, music and timing: the original 320x240 picture, the original NTSC rate
(59.29 fps, and its speed-dependent gameplay with it), and the PlayStation memory card format. Two
bugs of the original are fixed: the farm score now reaches 100%, and the hothouse eggplant has the
right colours when carried.

### Sharper graphics

- **Internal resolution** 2-4x (up to 8x with the Vulkan renderer), with perspective-correct textures.
- **PGXP**: precise 3D vertex positions, so models no longer wobble - with the thin cracks it opens
  between models closed again.
- **Widescreen** 16:9, 16:10 and 21:9: a wider 3D view, with the HUD and 2D objects keeping their
  shape and the title screen and menus filling the screen.
- **60 fps camera**: the camera and the scenery move every VBlank while the game keeps its own 30 Hz
  logic.
- **Texture packs** and **redrawn portraits**: replacement images in `textures/` and
  `textures/portraits/` next to the game.
- **Display**: window or fullscreen, sharp-bilinear, sharp or smooth scaling, 4:3 or square pixels,
  screenshots, and an optional frame-rate readout in the game's own font.

### Co-op

- **Local co-op**: two farmers on one PC, each in a window of their own (experimental). Farmer 2 uses
  a second controller or the numeric keypad, takes tools from the tool chest and trades with farmer 1
  by standing in front of them and pressing Cross. Farmer 2 can also go into buildings alone.
- **Online co-op**: two players, each on their own PC, in one game over TCP. Both need the same build
  version, which the window title shows; the host's settings, mods and cheats count for both, and the
  guest's own memory cards are never touched.

### Time savers

All of them optional, all of them original behaviour when switched off: shorter loading
(`fastcd`), quicker menus and shorter fades (`quickui`), faster dialogue text (`textspeed`), saving
and loading without the memory card slot menu (`autoslot`), no waiting while a card is read or
written (`fastcard`), cutscenes at full speed while START is held (`skipscenes`), hold-to-fast-forward
(`fastforward`), and a CPU speed up to 400% (`overclock`) so the game stops dropping frames when a lot
is going on - video, sound and timing stay the same.

### Mods and cheats

Four mods, off unless switched on: the cabinet opens in the first house, walking through crops, a
stamina and tiredness panel the game never shows, and buying food in bulk. Cheats (money, endless
stamina, a stopped clock, the biggest rucksack, materials and top-level tools) are on the launcher's
Cheats page and in-game; what a save made with them contains stays in the save.

### Saves

Memory cards as the PlayStation writes them: `saves/card1.mcd`, a standard 128 KB raw card image that
emulators such as DuckStation, ePSXe and PCSX read and write too, so an existing save can be brought
in and taken back out. Four cards (F1-F4) hold three diaries each. If the game folder is not
writable, the cards live in `%APPDATA%\Rexaver\HarvestMoonBTN` (Windows) or
`~/.local/share/Rexaver/HarvestMoonBTN` (Linux).

### The launcher

Every setting has a row on one of its pages - video, game, mods, keyboard, controller, local and
online co-op, cheats - and it writes `hmbtn.ini` next to the game. It starts the game, shows whether
the data pack is found and intact, downloads the game when the folder has none, and updates itself
from a newer release of this repository.

## Settings

Every setting lives in **`hmbtn.ini` next to the executable** (on Android, in the data folder above),
a commented file the launcher writes and you can also edit by hand: remove the `#` in front of an
option to change it. The launcher's rows are the same settings with their explanations.

| Written to `hmbtn.ini` | Applies |
|---|---|
| `scale`, `fullscreen`, `scaling`, `aspect43`, `showfps`, every `[keyboard]` and `[controller]` binding, the `[touch]` group, the cheats, and the `[behaviour]` time savers (`overclock` included) | While the game runs: it re-reads the file twice a second |
| `renderer`, `upscale`, `drawthreads`, `pgxp` with `crackfix`, `perspective`, `interp`, `texturepack`, `portraits`, `dumptextures`, `widescreen`, `savedir`, `p2view_upscale`, `record`, `split` | Only when the game starts - the launcher marks those rows **Restart the game to apply** |

A headless run, an input replay and online co-op never re-read the file: they run with the settings
they started with.

## Controls

|  | Keyboard | Xbox controller |
|---|---|---|
| D-pad | Arrow keys | D-pad / left stick |
| ✕ Cross | X / Space / K | A |
| ○ Circle | Z / L | B |
| □ Square | S / J | X |
| △ Triangle | A / I | Y |
| L1 / R1 | Q / W | LB / RB |
| L2 / R2 | 1 / 2 | LT / RT |
| Start | Enter | Start (Menu) |
| Select | Right Shift / Backspace | Back (View) |

| Key | |
|---|---|
| F11 or Alt+Enter | toggle fullscreen (Esc leaves fullscreen) |
| F12 | screenshot, saved in `screenshots/` |
| F5 | cheats window; changes apply at once (not in online co-op) |
| F9 | 60 fps camera on / off, to compare |
| F1-F4 | put memory card 1-4 in slot 1 |
| Tab (hold) | fast-forward (can be switched off) |
| START (hold, in a cutscene) | run the cutscene at full speed |

Every key and button can be remapped in the launcher or in `hmbtn.ini`, and any controller SDL2
recognises as a game controller works (Xbox, PlayStation, Switch Pro and others), with the layout
above. Controllers can be plugged in and out at any time. On a phone the on-screen gamepad does the
same job: it appears when the screen is first touched, and its **SET** gear under L1 opens the
settings screen, **START** under R2 starts the game, **SELECT** under L2 is Select, and **FF** under
R1 toggles fast-forward.

Farmer 2's controls in local co-op are the second controller or the numeric keypad, on the launcher's
**Local co-op** page.

## Troubleshooting

- **"Game data not found"** - `HarvestMoonBTN.pak` is not where the game looks. Put it back beside
  the executable (a `data` folder next to the game is searched too). If the game came from a zip,
  unpack the whole folder, not the `.exe` alone, and run `HarvestMoonBTN --verify-data` to check the
  pack (about two seconds, exit 0 when it is intact).
- **No sound** - the game opens the default audio device when it starts and picks up a device plugged
  in later. Check `HarvestMoonBTN.log` beside the executable: a line beginning `cannot open audio
  device` says which device failed. Set the right output as the system default and start the game
  again.
- **Where the window and settings are** - `hmbtn.ini` and `HarvestMoonBTN.log` sit beside the
  executable, and so do `saves/`, `screenshots/` and `recordings/`. If that folder is not writable
  (a read-only drive, or an app bundle), everything goes to `%APPDATA%\Rexaver\HarvestMoonBTN` on
  Windows or `~/.local/share/Rexaver/HarvestMoonBTN` on Linux instead; on Android it is the data
  folder in the section above. The launcher's Start page names the data file it found.
- **The memory cards** - the card is `saves/card1.mcd` in that same folder: a standard 128 KB raw
  memory card image, readable by DuckStation, ePSXe and PCSX, so an existing save can be copied in
  and yours can be taken to an emulator. F1-F4 switch between the four cards (`card1.mcd`,
  `card1_2.mcd`, `card1_3.mcd`, `card1_4.mcd`), three diaries each. Back that folder up before you
  move the install: the saves are not inside the zip you downloaded.
- **"SDL2 was not found" on Linux** - keep `libSDL2-2.0.so.0` next to the game, or install the
  distribution's SDL2 package (`libsdl2-2.0-0`, `SDL2`, `sdl2`).
- **Vulkan renderer** - without a working Vulkan driver the game falls back to the CPU renderer and
  the log says so. Update the graphics driver, or set `renderer = cpu`.
- **Anything else** - `HarvestMoonBTN.log` next to the executable usually says what happened. This
  project has no public issue tracker.

## Version history

- **v1.2** (2026-11-14) - the first release under this repository's new name: the launcher inside the
  folders and on its own is 1.2 and reads this repository, and the Android package is
  `HarvestMoonBTN-Android-1.2.apk` with versionCode 2, so it installs over the earlier 1.0 one. The
  game itself is the same code as v1.1; its executable was relinked for this build, which is what
  changes its hash. [v1.2](../../releases/tag/v1.2)
- **v1.1** (2026-11-14) - the Windows and Linux folders, the Android package (1.0) and the launcher
  exe (1.1), with a `.sha256` beside each. [v1.1](../../releases/tag/v1.1)
- **v1.0** (2026-11-16) - the version before the download page existed, built again from the commit
  that still said 1.0 and published for the record: the Windows and Linux folders, the Android package
  (`HarvestMoonBTN-Android-1.0.apk`) and the 1.0 launcher exe, with a `.sha256` beside each. It has no
  Windows installer and its launcher has no *Download and play*: the folder is the game.
  [v1.0](../../releases/tag/v1.0)

Each release carries its assets with a `.sha256` beside each, so an installed launcher can update
itself and download the game from the newest one. Every release is on the
[releases page](../../releases).

## Credits and legal

This is an unofficial fan project, not affiliated with or endorsed by Marvelous Inc., Natsume Inc.,
Victor Interactive Software or Sony Interactive Entertainment. *Harvest Moon* and *Back to Nature*
are trademarks of their respective owners.

The port's own code - the recompiler, the runtime and the launcher - is MIT-licensed, copyright
Rexaver. That licence covers the port's code only, and this repository publishes no code. The game's
data in these builds (graphics, music, text) and the translated game program are derived from
*Harvest Moon: Back to Nature* and are not this project's to license; they remain the property of
their copyright holders, and the folders are for personal use.

The port uses [SDL2](https://libsdl.org) (zlib license - the text ships as `LICENSE-SDL2.txt` in
every game folder), and the launcher and the phone's settings screen are lettered in
[Silkscreen](https://github.com/googlefonts/silkscreen) (SIL Open Font License 1.1 - the text ships
as `launcher-assets/fonts/OFL.txt`). The Vulkan renderer includes parallel-psx (ISC/MIT), volk (MIT),
SPIRV-Cross and the Vulkan headers (Apache-2.0). The launcher exe is made with
[PyInstaller](https://pyinstaller.org). Hardware information came from the public PlayStation
documentation, above all [psx-spx](https://psx-spx.consoledev.net/).

Every download, and the notes that came with it, is on the
[releases page](../../releases?expanded=true).
