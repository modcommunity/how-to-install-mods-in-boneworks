A guide on how to **download** and **install mods** in [BONEWORKS](https://store.steampowered.com/app/823500/BONEWORKS/) on PC.

BONEWORKS is a VR-only physics sandbox built in Unity, and its mods are loaded by [MelonLoader](https://melonwiki.xyz/) rather than BepInEx. That is the main thing that makes it different from most of the Unity games people mod. Everything lives on [Thunderstore](https://thunderstore.io/c/boneworks/).

Our worked example is [Custom Maps](https://thunderstore.io/c/boneworks/p/Maranara/Custom_Maps/), a map loader that lets you drop community-made levels into the game. It needs two other mods to work, which makes it a useful demonstration of how the stack fits together.

[**View Guide On TMC (Recommended Due To Better Formatting)**](https://moddingcommunity.com/blog/how-to-install-mods-in-boneworks/)

## Table Of Contents
* [Requirements](#requirements)
* [MelonLoader, Not BepInEx](#melonloader-not-bepinex)
    * [ModThatIsNotMod](#modthatisnotmod)
    * [A Word About BONELAB Mods](#a-word-about-bonelab-mods)
* [Installing With Gale](#installing-with-gale)
* [Installing With r2modman](#installing-with-r2modman)
* [Installing MelonLoader Yourself](#installing-melonloader-yourself)
    * [The Automated Installer](#the-automated-installer)
    * [The Manual Method](#the-manual-method)
* [Installing Mods By Hand](#installing-mods-by-hand)
* [Installing With The TMC App](#installing-with-the-tmc-app)
* [Checking It Worked](#checking-it-worked)
* [Running On Linux](#running-on-linux)
* [Removing Mods](#removing-mods)
* [Troubleshooting](#troubleshooting)
* [Conclusion](#conclusion)
* [See Also](#see-also)

## Requirements
* A PC running **Windows 10** or later. Linux through Proton works with an extra environment variable, covered below.
* **BONEWORKS** on Steam, plus a VR headset and its runtime. There is no flatscreen mode.
* [Microsoft Visual C++ 2015-2019 Redistributable, 64 bit](https://aka.ms/vs/16/release/vc_redist.x64.exe). MelonLoader needs it.
* [.NET Desktop Runtime 6.0, x64](https://dotnet.microsoft.com/en-us/download/dotnet/6.0). BONEWORKS is an Il2Cpp game and MelonLoader requires this for those.
* A few hundred MB free, more if you are collecting custom maps.

BONEWORKS is single player with no anti-cheat. Nothing here puts your account at risk.

## MelonLoader, Not BepInEx
If you have modded Lethal Company, Valheim or most other Unity games, you have used BepInEx. BONEWORKS does not use it.

[MelonLoader](https://thunderstore.io/c/boneworks/p/LavaGang/MelonLoader/) is a different universal Unity mod loader, built by LavaGang, with first-class support for Il2Cpp games like this one. It works on the same principle: it hooks the game at launch and loads mods, but the folder layout and the installer are its own.

MelonLoader mods are `.dll` files that go in a `Mods` folder in the game directory, not `BepInEx/plugins`.

### ModThatIsNotMod
Almost every BONEWORKS mod you will actually want depends on [ModThatIsNotMod](https://thunderstore.io/c/boneworks/p/gnonme/ModThatIsNotMod/) by gnonme. It is the shared library for this game: it handles loading custom items, gives mod authors helpers for the game's systems, and is the thing the rest of the ecosystem is built against.

Custom Maps needs it, along with [FieldInjection](https://thunderstore.io/c/boneworks/p/WNP78/FieldInjection/). So the full stack for our example is:

```
MelonLoader  ->  ModThatIsNotMod + FieldInjection  ->  Custom Maps
```

A mod manager works all of that out for you.

### A Word About BONELAB Mods
BONEWORKS and BONELAB are separate games with separate Thunderstore communities, and some packages are listed under both. That cross-listing is not always meaningful.

[Hitmarkers](https://thunderstore.io/c/boneworks/p/NotEnoughPhotons/Hitmarkers/) is the one people run into most. It appears in the BONEWORKS listings, but every published version of it depends on **BoneLib**, which is a BONELAB library with no BONEWORKS equivalent, and its own description says it was redone for BONELAB. Installing it here will not do what you want.

The rule of thumb: if a BONEWORKS mod lists **ModThatIsNotMod** as a dependency, it is genuinely a BONEWORKS mod. If it lists **BoneLib**, it is a BONELAB mod that happens to be cross-listed.

## Installing With Gale
[Gale](https://thunderstore.io/c/boneworks/p/Kesomannen/GaleModManager/) is the easiest route and handles MelonLoader for you.

1. Download Gale from [Thunderstore](https://thunderstore.io/c/boneworks/p/Kesomannen/GaleModManager/) or [GitHub](https://github.com/Kesomannen/gale/releases).
2. Open it and select **BONEWORKS**.
3. Let it find your Steam install, or point it at the game folder yourself.
4. Open **Browse mods**, search for **Custom Maps**, and click **Install**.
5. MelonLoader, ModThatIsNotMod and FieldInjection are installed alongside it.
6. Click **Launch game (modded)**.

Launching BONEWORKS from Steam starts it unmodded. Launch from Gale.

## Installing With r2modman
[r2modman](https://thunderstore.io/c/boneworks/p/ebkr/r2modman/) works the same way.

1. Install r2modman and select **BONEWORKS**.
2. Create a profile.
3. Open **Online**, search for **Custom Maps**, and use **Download with dependencies**.
4. Click **Start modded**.

Either is fine. Gale is lighter; r2modman has broader platform support.

## Installing MelonLoader Yourself
Worth knowing if you would rather not use a manager, or if a manager is giving you trouble.

First find your game folder. Right-click **BONEWORKS** in Steam, then **Manage** and **Browse local files**:

```
C:\Program Files (x86)\Steam\steamapps\common\BONEWORKS
```

You are looking for `BONEWORKS.exe`.

### The Automated Installer
This is the recommended way and it is genuinely easy.

1. Download the [MelonLoader Installer](https://github.com/LavaGang/MelonLoader.Installer/releases/latest/download/MelonLoader.Installer.exe).
2. Run it. It scans for installed Unity games and should list BONEWORKS on its own. If it does not, use **Add Game Manually** and point it at `BONEWORKS.exe`.
3. Click BONEWORKS in the list, pick a version, and hit **Install**.

**WARNING** - Leave the nightly builds switch alone. Nightlies are generated from the latest commits and break things regularly. The stable release is what mods are built against.

### The Manual Method
1. Download [MelonLoader.x64.zip](https://github.com/LavaGang/MelonLoader/releases/latest/download/MelonLoader.x64.zip). BONEWORKS is 64 bit.
2. Extract the `MelonLoader` folder from the zip into the BONEWORKS folder.
3. Extract `version.dll` from the same zip into the BONEWORKS folder as well.
4. Launch the game once so MelonLoader generates its folders, then quit.

You should now have a `MelonLoader` folder, a `version.dll` and a `Mods` folder sitting alongside `BONEWORKS.exe`.

## Installing Mods By Hand
With MelonLoader in place, mods are straightforward.

1. Open the mod's Thunderstore page and click **Manual Download**.
2. Extract the zip.
3. Copy the `.dll` into the `Mods` folder in your BONEWORKS directory.

For Custom Maps that means three separate downloads, since you need ModThatIsNotMod and FieldInjection too. Grab each at the version the mod's **Dependencies** section names, and copy each `.dll` into `Mods`.

Some mods ship extra content alongside the `.dll`, such as map or model files. Read the mod's description for where those go. Custom Maps, for instance, reads map files out of its own folder rather than out of `Mods`.

**NOTE** - The `manifest.json`, `icon.png` and `README.md` in a Thunderstore zip are packaging files for the website. They do nothing in the `Mods` folder.

## Installing With The TMC App
Rounding out the list is our own tool. [The TMC App](https://moddingcommunity.com/tmc-app) is a mod manager and server browser we build, with one-click installs and **sandboxes**: named mod profiles per game, each with its own load order and deployment method, switchable without re-downloading a thing.

**BONEWORKS is not in its supported games list yet.** Adding a game is four JSON files and no code, so it is a small job and MelonLoader games are squarely the kind of thing the plugin system is meant to cover.

The honest bit: **the app is in very early development.** We say so in its README and we are saying so here. A lot of it is only partially tested, so treat it as something to try alongside Gale rather than as a replacement. If you do try it, please tell us what happened, because that is the most useful thing anyone can do for the project right now.

It is **open source** under GPL-3.0 at [github.com/modcommunity/tmc-app](https://github.com/modcommunity/tmc-app). Bugs and feature requests go in [the issue tracker](https://github.com/modcommunity/tmc-app/issues), pull requests are welcome, and the repository documents the per-game format if you want to add BONEWORKS support yourself.

Installing it:

* **Linux**: one line, no root and no package manager.

```bash
curl -fsSL https://raw.githubusercontent.com/modcommunity/tmc-app/main/scripts/install.sh | sh
```

* **Windows**: the `setup.exe` or `setup.msi` from the [releases page](https://github.com/modcommunity/tmc-app/releases). There is a portable build too, though it does not register the launcher entry or the `tmc://` link handler.
* **macOS**: the `.dmg` from the same releases page.

## Checking It Worked
MelonLoader opens a console window next to the game on launch. During startup it prints its own version and then a line per mod as it loads them, with the mod name, version and author.

Logs are written to disk too:

```
BONEWORKS\MelonLoader\Latest.log
```

That file is the first thing to look at when something does not work, and the first thing anyone helping you will ask for.

For Custom Maps specifically, the mod adds its own way to pick a level in-game once you have map files installed.

## Running On Linux
BONEWORKS runs through Proton. MelonLoader needs a DLL override to get loaded, so set the game's Steam launch options to:

```
WINEDLLOVERRIDES="version=n,b" %command%
```

Note this is `version`, not `winhttp`. MelonLoader uses a different hook DLL from BepInEx, and copying the BepInEx launch option across is a common mistake.

The MelonLoader installer also has a [Linux build](https://github.com/LavaGang/MelonLoader.Installer/releases/latest/download/MelonLoader.Installer.Linux) if you would rather not do it by hand. Gale and r2modman both set the override themselves when you launch through them.

## Removing Mods
Delete the `.dll` from the `Mods` folder, or uninstall it through your mod manager.

To remove MelonLoader entirely, delete the `MelonLoader` folder, `version.dll`, the `Mods` folder and the `UserData` folder from the game directory. The MelonLoader Installer also has an uninstall option that does this for you.

Steam's **Verify integrity of game files** will not clean any of this up, because Steam has no record of files it did not install.

## Troubleshooting
**No console window and no mods.** MelonLoader is not loading. Check that `version.dll` is directly next to `BONEWORKS.exe`, and that you launched from your mod manager rather than from Steam.

**MelonLoader loads but a mod does not.** Open `MelonLoader\Latest.log`. Missing dependencies and version mismatches both show up clearly there.

**MelonLoader crashes on startup.** Usually a missing prerequisite. Install the [VC++ 2015-2019 x64 redistributable](https://aka.ms/vs/16/release/vc_redist.x64.exe) and the [.NET Desktop Runtime 6.0 x64](https://dotnet.microsoft.com/en-us/download/dotnet/6.0), which Il2Cpp games need.

**A mod installed fine but does nothing at all.** Check whether it is actually a BONEWORKS mod. If its dependency list mentions BoneLib, it is a BONELAB mod that happens to be cross-listed.

**Everything broke after a game update.** BONEWORKS is not updated often these days, but when it is, MelonLoader and the mods both need to catch up. Empty the `Mods` folder to confirm the game itself is fine, then wait.

**VR runtime errors after installing mods.** Try launching without mods first to confirm the headset side is working. Mod problems and SteamVR problems look similar from inside a headset.

## Conclusion
BONEWORKS modding is simple once you know it is MelonLoader rather than BepInEx, and that ModThatIsNotMod is the library everything else sits on. Install Gale, install the mod you want, and launch through Gale.

The one BONEWORKS-specific trap is cross-listed BONELAB packages. Check the dependency list before you install: ModThatIsNotMod means BONEWORKS, BoneLib means BONELAB.

If you want to help with something, the [TMC App](https://github.com/modcommunity/tmc-app) is open source and early in development, and feedback on it is worth a great deal to us.

## See Also
* [BONEWORKS on Thunderstore](https://thunderstore.io/c/boneworks/)
* [MelonLoader Wiki](https://melonwiki.xyz/) - The loader's own documentation, worth a read.
* [MelonLoader on GitHub](https://github.com/LavaGang/MelonLoader)
* [BONEWORKS Modding Discord](https://discord.gg/mjmpUR8)
* [BONEWORKS Wiki](https://boneworks.fandom.com/wiki/BONEWORKS_Wiki)
* [TMC App](https://github.com/modcommunity/tmc-app)

We keep this guide as current as we can, but MelonLoader and the mods built on it change over time. If an instruction here no longer matches what you are seeing, please report it or open a [pull request](https://github.com/modcommunity/how-to-install-mods-in-boneworks/pulls) on this guide's GitHub repository.

Join our [Discord server](https://discord.moddingcommunity.com) if you have any questions or want a hand with anything modding related!
