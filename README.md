# SteamDeck Toolkit — Skyrim SE 1.7.104.0

[![Steam Deck](https://img.shields.io/badge/Steam%20Deck-SteamOS-1b2838?logo=steam)](https://store.steampowered.com/steamdeck)
[![Skyrim](https://img.shields.io/badge/Skyrim%20SE%2FAE-1.7.104.0-6b6b6b)](https://store.steampowered.com/app/489830/The_Elder_Scrolls_V_Skyrim_Special_Edition/)
[![SKSE](https://img.shields.io/badge/SKSE64-2.3.1-blue)](https://skse.silverlock.org/)
[![Languages](https://img.shields.io/badge/UI-EN%20%7C%20RU-4c8bf5)](https://github.com/rnxdvr/SteamDeck_Toolkit_SkyrimSE_1.7.104.0)

**English** | [Русский](README_RU.md)

A Steam Deck-focused installer and configuration toolkit for **The Elder Scrolls V: Skyrim Special Edition** on Steam, tested against **runtime 1.7.104.0**.

The project automates the repetitive parts of a manual Skyrim setup on SteamOS: locating the game and Proton prefix, preparing required SKSE components, installing selected mods from user-downloaded archives, checking the required Visual C++ runtime, configuring frame pacing and graphics presets, setting a persistent FOV, and installing a controller-friendly settings utility for later use.

> [!IMPORTANT]
> This project currently targets **Skyrim Steam runtime 1.7.104.0**.
> In SKSE terminology this runtime belongs to the **AE branch**, even if Steam displays the game as *Skyrim Special Edition*.

## What the toolkit does

The setup wizard is designed to behave like a normal desktop installer instead of a collection of terminal commands.

It can:

- detect Skyrim on the Steam Deck internal drive or a Steam library on an SD card;
- detect the Skyrim Proton prefix (`AppID 489830`);
- let the user choose **English or Russian** at the start of the installation;
- separate **required components** from optional quality-of-life mods;
- explain what each mod is used for before installation;
- open the official download pages for all selected mods;
- wait while the user downloads the archives manually;
- verify that the required archives are present in `~/Downloads`;
- validate archives by their contents instead of relying only on filenames;
- install the selected mods into the Skyrim directory;
- configure plugin load order where required;
- check the Proton prefix for the required Visual C++ runtime;
- install **VC++ 2022 x64** through Protontricks when it is missing;
- handle Steam libraries located on an SD card;
- configure initial graphics, synchronization and FOV settings;
- install **Skyrim SE Presets**, the included controller-friendly settings utility;
- create a Desktop shortcut and a Steam / Gaming Mode shortcut;
- keep third-party mod files outside this repository.

## Supported Skyrim version

| Component | Supported / tested version |
|---|---:|
| Skyrim Special Edition / Anniversary runtime | **1.7.104.0 (Steam)** |
| Steam AppID | **489830** |
| SKSE64 | **2.3.1** |
| Address Library | **v13 — All in One for 1.7.104.0** |
| SSE Display Tweaks | **0.5.25** |
| Microsoft Visual C++ runtime | **2022 x64** |
| Platform | **Steam Deck / SteamOS / Proton** |

The toolkit intentionally checks for the supported runtime because native SKSE plugins are version-sensitive.

## Required components

These are the core components used by the toolkit.

| Component | Version | Why it is needed |
|---|---:|---|
| [SKSE64](https://skse.silverlock.org/) | **2.3.1** | Script extender required by native SKSE plugins and advanced mods. |
| [Address Library for SKSE Plugins](https://www.nexusmods.com/skyrimspecialedition/mods/32444) | **v13** | Provides address mappings for Skyrim **1.7.104.0**. |
| [SSE Display Tweaks](https://www.nexusmods.com/skyrimspecialedition/mods/34705) | **0.5.25** | Used for frame pacing, VSync, FPS behavior, latency-related settings and Havok timing. |
| Microsoft Visual C++ Redistributable | **2022 x64** | Runtime required by SSE Display Tweaks and many modern SKSE DLL plugins. Installed into the Proton prefix when needed. |

Third-party files are **not bundled** with this repository. The wizard opens the original download pages and works with archives downloaded by the user.

## Optional author's mod set

These mods are **not required for the toolkit itself**. They are offered as an optional setup used by the author for a more comfortable Steam Deck experience.

| Mod | Version used/tested | Purpose |
|---|---:|---|
| [Better Jumping SE](https://www.nexusmods.com/skyrimspecialedition/mods/18967) | **1.9.5** | Improves jumping behavior, including sprint jumping and movement-related fixes. |
| [Pristine Vanilla Movement](https://www.nexusmods.com/skyrimspecialedition/mods/66635) | **1.1** | Polished vanilla-style walk, run and sprint animations. |
| [True Directional Movement](https://www.nexusmods.com/skyrimspecialedition/mods/51614) | **2.3.1** | Modern third-person movement, target lock and camera-direction behavior. |
| [SmoothCam](https://www.nexusmods.com/skyrimspecialedition/mods/41252) | **1.8.1** | Highly configurable third-person camera. |
| [SmoothCam 1.7.104 compatibility patch](https://www.nexusmods.com/skyrimspecialedition/mods/192993) | **v2** | Required for the tested SmoothCam setup on Skyrim **1.7.104.0**. Install after SmoothCam. |
| [Achievements Mods Enabler](https://www.nexusmods.com/skyrimspecialedition/mods/245) | **1.41** | Allows Steam achievements while using mods. |

The installer resolves additional dependencies when a selected mod needs them.

## SkyUI, MCM and the Steam Deck UI

Some optional mods use an MCM configuration menu and therefore need SkyUI-related components.

The tested setup uses:

| Component | Version / branch |
|---|---:|
| [SkyUI](https://www.nexusmods.com/skyrimspecialedition/mods/12604) | **SkyUI 6 Update / 1.7.104-compatible build** |
| [MCM Helper](https://www.nexusmods.com/skyrimspecialedition/mods/53000) | **1.6.3** |
| [SkyUI Vanilla Menus](https://www.nexusmods.com/skyrimspecialedition/mods/93039) | **1.3 / Full Vanilla 1.3b** |

### Recommended UI on Steam Deck

The installer recommends keeping the **vanilla Skyrim menus** when SkyUI is required.

Why?

The standard SkyUI layout is information-dense and can be difficult to read on the Steam Deck display. The recommended configuration keeps SkyUI installed for MCM and mod compatibility while restoring the original Skyrim menus with **SkyUI Full Vanilla Menus**.

This gives you:

- MCM support;
- SkyUI backend functionality;
- compatibility with mods that require SkyUI;
- the larger and more readable vanilla inventory, map, favorites and crafting interfaces.

Users who prefer the normal SkyUI interface can select it during installation.

## Installation

### 1. Prepare Skyrim

Install **Skyrim Special Edition** through Steam and make sure the game runtime is:

```text
1.7.104.0
```

The toolkit is not currently intended for other Skyrim runtimes.

### 2. Download the latest toolkit release

Open the repository's [Releases](https://github.com/rnxdvr/SteamDeck_Toolkit_SkyrimSE_1.7.104.0/releases) page and download the latest installer archive.

Extract it anywhere on the Steam Deck. The installer is portable and does **not** require a hardcoded Desktop path.

### 3. Run the installer

Switch to **Desktop Mode** and launch:

```text
Install_Toolkit.desktop
```

Choose:

```text
EN
```

or:

```text
RU
```

and follow the wizard.

### 4. Choose mods

The wizard first shows only the required components.

Optional mods are shown separately under the author's recommended extras. If a selected mod introduces another dependency, the installer adds it automatically.

If SkyUI is required, the wizard asks whether you want:

- **Vanilla Skyrim UI — recommended for Steam Deck**
- **SkyUI interface**

### 5. Download requested mods

The wizard opens the original pages for the selected mods.

Download the requested versions with **Manual Download** and leave the archives in:

```text
~/Downloads
```

Do not unpack them manually.

Return to the installer and confirm that the downloads are complete. The wizard checks the archives before proceeding and reports anything that is missing or incorrect.

### 6. Automatic setup

After verification, the toolkit performs the selected setup automatically:

```text
Mod installation
        ↓
Plugin configuration
        ↓
VC++ / Protontricks check
        ↓
Graphics preset
        ↓
Sync / frame pacing mode
        ↓
Persistent FOV
        ↓
Skyrim SE Presets installation
        ↓
Desktop + Gaming Mode shortcuts
```

## Skyrim SE Presets

After the initial setup, settings can be changed with the included **Skyrim SE Presets** utility.

Launch it from either:

**Gaming Mode / Big Picture**

```text
Library → Non-Steam → Skyrim SE Presets
```

or the Desktop shortcut:

```text
Skyrim_SE_Presets.desktop
```

The utility is designed for controller use and includes:

### Presets

Ready-to-use Steam Deck graphics profiles.

```text
BATTERY
BALANCED
PERFORMANCE
```

### Sync

Frame-pacing modes such as:

```text
SMOOTH + LOW LATENCY
SMOOTH DEFAULT
UNLIMITED
```

The smooth modes can follow the display refresh rate instead of forcing an unrelated fixed FPS cap.

### Custom

Individual graphics and display settings with selectable values. Manual text entry is not required.

### Current

Displays the currently detected values from the Skyrim configuration files and SSE Display Tweaks configuration.

### FOV

Persistent FOV adjustment is available directly in the utility.

The FOV selector uses a continuous range:

```text
0 ───────────────────────────── 200
```

and includes a reset option for the Skyrim default.

## Restart required

> [!IMPORTANT]
> Most graphics, display and SSE Display Tweaks settings are read when Skyrim starts.
>
> After changing those settings, **restart Skyrim** before judging the result.
>
> The configuration utility marks such changes with **RESTART REQUIRED**.

Changing an INI while Skyrim is running does not guarantee that the running game will reload the value, and Skyrim may write some settings back when it exits.

## Files modified by the toolkit

Depending on the selected options, the toolkit may work with:

```text
Skyrim Special Edition/
├── SkyrimSELauncher.exe
├── skse64_loader.exe
└── Data/
    ├── SKSE/
    ├── Interface/
    └── *.esp / *.esl / *.bsa
```

and the Proton-side configuration:

```text
compatdata/489830/pfx/
└── drive_c/users/steamuser/
    ├── Documents/My Games/Skyrim Special Edition/
    │   ├── Skyrim.ini
    │   ├── SkyrimPrefs.ini
    │   └── SkyrimCustom.ini
    └── AppData/Local/Skyrim Special Edition/
        ├── plugins.txt
        └── loadorder.txt
```

The game may be located on internal storage or an SD-card Steam library.

## Troubleshooting

If something fails:

1. Make sure Skyrim itself is completely closed.
2. Confirm that the Steam version is **1.7.104.0**.
3. Verify that the requested mod archives are still in `~/Downloads`.
4. Do not substitute an older SKSE build such as 2.0.x.
5. If a native DLL plugin fails to load, check its exact runtime compatibility.
6. If the game is on an SD card, make sure Protontricks has access to that Steam library.
7. Open an [issue](https://github.com/rnxdvr/SteamDeck_Toolkit_SkyrimSE_1.7.104.0/issues) and attach the installer/runtime log when possible.

## Project scope

This project is intended to provide a **small, understandable and reproducible Steam Deck setup**, not to replace a full desktop mod manager.

It deliberately focuses on:

- Skyrim **1.7.104.0**;
- a known set of tested SKSE dependencies;
- Steam Deck-friendly frame pacing;
- readable UI;
- controller operation;
- easy recovery and configuration.

## Third-party mods and credits

This repository does **not** redistribute SKSE, Nexus Mods files, DLLs, ESP/ESL/BSA files, or other third-party mod assets.

All third-party projects remain the property of their respective authors and are downloaded from their original distribution pages.

Please endorse the mods you use and follow the permissions and licensing terms set by their authors.

## Compatibility warning

Bethesda game updates can change the Skyrim runtime and break native SKSE plugins.

Before updating Skyrim, check that the following are compatible with the new runtime:

```text
SKSE64
Address Library
SSE Display Tweaks
True Directional Movement
SmoothCam / compatibility patch
other SKSE DLL plugins
```

A newer Skyrim version is **not automatically supported** just because the game launches.

## Repository

**SteamDeck Toolkit — Skyrim SE 1.7.104.0**

https://github.com/rnxdvr/SteamDeck_Toolkit_SkyrimSE_1.7.104.0

Bug reports and suggestions are welcome through [GitHub Issues](https://github.com/rnxdvr/SteamDeck_Toolkit_SkyrimSE_1.7.104.0/issues).
