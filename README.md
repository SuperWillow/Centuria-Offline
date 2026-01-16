# Fer.al Offline Mode
This mod adds to Emuferal (OG Fer.al) and Centuria an offline mode, which was originally added to earlier versions of Emuferal.
Centuria is a work-in-progress server emulator for the now-defunct MMORPG Fer.al. The main server project can be found [here](https://github.com/CPeers1/Centuria). Centuria is developed by a group of developers from the Fer.ever discord. The software was originally released by the AerialWorks Software Foundation (SkySwimmer's small organization) but is now owned [Owenvii](https://github.com/CPeers1).

<br/>

# Building the client mods
The project is split up into multiple parts, `feraltweaks`, `feraltweaks-bootstrap` (FTL modloader), the launcher and the server modules needed for the mod handshake and mod download system.

<br/>

## Using the Desktop mod
After putting the mod folder in the `FeralTweaks/mods` folder of your client (you may need to create this directory), it should load automatically as long as you have FTL installed. Note that the client mod doesn't have content, content is streamed (or will stream) from the  server.

You can however change client-specific options in `FeralTweaks/config/feraltweaks/settings.props` which contains some settings you may find useful. Note that client settings are overriden by the server when playing on a feral-tweaks enabled Centuria server.

<br/>

# List of server modules
Here is the list of server modules that are a part of the project:
 - [feraltweaks-server-module](https://github.com/SkySwimmer/Centuria-Modding/tree/main/feraltweaks-server-module): core server logic required for some features of the client mod. This module provides required handshake logic for chat and game bindings and provides a way for servers to keep client mods up-to-date.
 - [gcs-for-feral](https://github.com/SkySwimmer/Centuria-Modules): group chats for Fer.al, technical side functions like DM conversations which is why thet are vanilla-compatible. GCs are created via commands and work on both vanilla and modded clients, modded clients distinguish GCs from DMs and separate them into two tabs.

<br/>

# Building the server modules
Each server module project is built with Gradle, you will need Java 17 on your device for this.

<br/>

## Building on Windows
On windows, run the following commands in cmd or powershell (inside a module subdirectory):

Set up a local server to build against:
```powershell
.\createlocalserver.bat
```

Set up a development environment (optional):
```powershell
.\gradlew eclipse createEclipseLaunches
```

Build the project:
```powershell
.\gradlew build
```

<br/>

## Building on Linux and OSX
On linux, in bash or your favorite shell, run the following commands in a module subdirectory: (note that this requires bash to be installed on OSX, most linux distros have bash pre-installed)

Configure permissions:
```bash
chmod +x createlocalserver.sh
chmod +x gradlew
```

Set up a local server to build against:
```bash
./createlocalserver.sh
```

Set up a development environment (optional):
```bash
./gradlew eclipse createEclipseLaunches
```

Build the project:
```bash
./gradlew build
```

<br/>

## Installing the modules on a Centuria server
After building, modules will be placed in `build/libs` (of the module subdirectory), simply copy the jar file into the `modules` folder of a Centuria server.

### Exception to this build directory
Apart from `centuria-discord`, all modules build in `build/libs`, however the Discord bot module has more dependencies. After building, you should copy the contents of `build/moduledata` to the server directory. This directory includes all dependencies of the module.
