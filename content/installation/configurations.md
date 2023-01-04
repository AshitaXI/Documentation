---
menuTitle: "Configurations"
title: "Configuring Ashita"
weight: 1
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

{{% notice info %}}
This page is subject to change heavily in the future when **Ashita** v4 gains its full UI launcher.
{{% /notice %}}

Once you have downloaded and extracted/installed **Ashita**, you are ready to begin configurations.

## Configuration File Locations

**Ashita** includes its own built-in `ConfigurationManager` object which makes use of `.ini` files. To help keep things organized, all configuration files that make use of this system are stored in a central location, the `/config/` folder. In addition to this manager, **Ashita** includes a `settings` library for addons to make use of which also stores per-character configurations within this folder.

The `/config/` folder also contains sub-folders for more specific usages.

These are the main sub-folders you should expect to see:

  - `/config/addons/`
  - `/config/ashita/`
  - `/config/boot/`
  - `/config/sandbox/`

{{% notice note %}}
Addons and plugins can make their own folders for their various configuration settings.
{{% /notice %}}

### Folder: `/config/addons/`

This folder contains addons' per-character settings files made using the included `settings` addon library.

### Folder: `/config/ashita/`

This folder contains **Ashita** specific configuration settings files. These are the main settings required in order for **Ashita** to function properly.

  - `ashita.datmap.ini` - _Contains the various DAT file information that **Ashita** will parse internally via the `ResourceManager`._
  - `ashita.offsets.ini` - _Contains the various memory offsets used with the pointer information internally._
  - `ashita.pointers.ini` - _Contains the various memory pointer information used to hook game functions and locate game objects._

This folder can also include custom overrides for the various files that are already present in this folder. These override files are used to allow users to have **Ashita** target a different client version. _**Ashita** will attempt to always keep the included `ashita.xxx.ini` configuration files up to date, but will not overwrite/update any `custom.xxx.ini` replacement files._

  - `custom.datmap.ini` - _Can contain any overrides or new information to alter how the original datmap configurations are handled._
  - `custom.offsets.ini` - _Can contain any overrides or new information to alter how the original offset configurations are handled._
  - `custom.pointers.ini` - _Can contain any overrides or new information to alter how the original pointer configurations are handled._

{{% notice warning %}}
You should **NEVER** alter the `ashita.xxx.ini` settings files! These will be overwritten when running the launcher by the latest available files. Instead, make use of the `custom.xxx.ini` files if you need to alter how **Ashita** functions.
{{% /notice %}}

### Folder: `/config/boot/`

This folder contains the boot configurations/profiles used to launch the game. Players can create a single file and share it between all characters they wish to play, or you can create individual profiles for each character. These files hold the various configurations for **Ashita** settings as well as the game registry configuration overrides.

_You can find more information about profile configurations below._

### Folder: `/config/sandbox/`

New to **Ashita** v4 is the `Sandbox` plugin. This plugin can completely emulate/virtualize the game installation allowing you to run FFXI without having to install it. _(You must have a working copy of the game before making use of Sandbox!)_ This allows you to make FFXI portable and run it [nearly] anywhere.

This folder contains the required configuration files for `Sandbox` to function.

## Boot Configurations

In order to launch the game and load **Ashita**, a boot configuration must be provided. These configuration files are stored within the `/config/boot/` folder and hold the various configuration settings needed to prepare **Ashita** for usage, as well as handle the game registry settings.

**Ashita** v4 holds boot configurations within the `.ini` format.  If you would like to learn more about this file format, you can find information here: https://en.wikipedia.org/wiki/INI_file

Following the normal format of `.ini` files, the boot configurations are broken into sections.\
Below is information about each section and the settings available to that section.

### Section: `[ashita.launcher]`

Contains configuration settings used with the **Ashita** launcher.

  - `autoclose` - _(boolean)_
    - **Default:** 1
    - Sets if the launcher should automatically close after successfully launching this configuration.
  - `name` - _(string)_
    - **Default:** _(empty)_
    - The name of the configuration to display in the launcher. If left empty, the launcher will use the file name instead.

### Section: `[ashita.boot]`

Contains configuration settings used with the boot loader and initial startup of the game.

  - `file` - _(string)_
    - **Default:** _(empty)_
    - Sets the boot file to launch to start FFXI.
    - _If playing on retail, this can be left empty. **Ashita** will automatically find a valid install and launch the game. However, you may want to directly set this still if you have multiple game installs of FFXI. If playing on a private server, this should point to the boot loader used with the server.)_
  - `command` - _(string)_
    - **Default:** _(empty)_
    - Sets the boot command that is passed to the boot loader (file) on launch.
    - _If playing on retail, this can be left empty or set to `/game eAZcFcB` to show the quick-play icon inside of PlayOnline to log into FFXI faster. If playing on a private server, this should be the commands required by the server you are playing on in order to properly connect. (Usually the `--server \<ip\>` command is enough.)_
  - `gamemodule` - _(string)_
    - **Default:** _(empty)_
    - Sets the name of the main game module **Ashita** should use when doing game module lookups.
    - _If left blank, this will resolve to `FFXiMain.dll`. This should only be changed if the private server you are playing on has renamed `FFXiMain.dll` to something else._
  - `script` - _(string)_
    - **Default:** _(empty)_
    - Sets the script file to execute after **Ashita** has successfully injected into the game.
    - _If left blank, **Ashita** will not execute any script automatically._
  - `args` - _(string)_
    - **Default:** _(empty)_
    - Sets the script arguments to pass to the 'script' (if set) above when it's executed.
    - _This can be useful if you share a script between multiple characters, but want to use specific values for token replacements. Such as binds/aliases that use the profiles specific character name._

### Section: `[ashita.language]`

Contains configuration settings used to determine which language data is used for defaults.

  - `playonline` - _(number)_
    - **Default:** 2
    - Sets the default PlayOnline language the launcher will use when trying to launch retail and no direct boot file was given.
    - _If set to 0, **Ashita** will default to English._
    - Valid values are: `0 = Default`, `1 = Japanese`, `2 = English`, `3 = European`
  - `ashita` - _(number)_
    - **Default:** 2
    - Sets the default language used with the internal ResourceManager string data.
    - _If set to 0 or 3, **Ashita** will default to English. (SE no longer translates strings to European.)_
    - Valid values are: `0 = Default`, `1 = Japanese`, `2 = English`, `3 = European`

### Section: `[ashita.logging]`

Contains configuration settings used for **Ashita**'s debugging/logging features.

  - `level` - _(number)_
    - **Default:** 5
    - Sets the level of debugging information **Ashita** will output to its log files.
    - Valid values are: `0 = None`, `1 = Critical`, `2 = Error`, `3 = Warn`, `4 = Info`, `5 = Debug`
  - `crashdumps` - _(number)_
    - **Default:** 1
    - Sets if **Ashita** should create crash dumps automatically when a critical error occurs.

### Section: `[ashita.taskpool]`

Contains configuration settings used with **Ashita**'s internal task queue system.

  - `threadcount` - _(number)_
    - **Default**: -1
    - Sets the maximum number of threads the task queue will attempt to use.
    - _If set to 0 or lower, the internal task queue will query the system for the available number of logical cores and determine the best number of threads to use. It is recommended to leave this as -1 and let the system determine the best number itself._

### Section: `[ashita.resources]`

Contains configuration settings used with **Ashita**'s custom resource data override configuration files.

  - `offsets.use_overrides` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should load and merge in the custom overrides within the `custom.offsets.ini` configuration file.
  - `pointers.use_overrides` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should load and merge in the custom overrides within the `custom.pointers.ini` configuration file.
  - `resources.use_overrides` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should load and merge in the custom overrides within the `custom.datmap.ini` configuration file.

### Section: `[ashita.window.startpos]`

Contains configuration settings used to set the startup position of the game window.

  - `x` - _(number)_
    - **Default:** -1
    - Sets the X screen position to start the game window at.
    - _If set to -1, will use the center X position of the screen._
  - `y` - _(number)_
    - **Default:** -1
    - Sets the Y screen position to start the game window at.
    - _If set to -1, will use the center Y position of the screen._

### Section: `[ashita.input]`

Contains configuration settings used with the various input devices to interact with the game.

  - `gamepad.allowbackground` - _(boolean)_
    - **Default:** 0
    - Sets if controllers should still work if the game is out of focus.
  - `gamepad.disableenumeration` - _(boolean)_
    - **Default:** 0
    - Sets if **Ashita** should disable the ability for game controllers to be discovered.
    - _This is useful to turn on if you leave controllers enabled but not use one. You may notice a micro-stutter while playing. Turning this on will usually fix that micro-stutter. However, while this is on, you will not be able to use a controller until its turned off._
  - `keyboard.blockinput` - _(boolean)_
    - **Default:** 0
    - Sets if **Ashita** should completely disable all keyboard input.
  - `keyboard.blockbindsduringinput` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should ignore keybinds while the game is expecting input.
    - _This will block keybinds while entering chat into the chat box, or editing things like search comments, bazaar comments, etc._
  - `keyboard.silentbinds` - _(boolean)_
    - **Default:** 0
    - Sets if **Ashita** should announce bind related information, such as setting a new keybind.
    - _If enabled, **Ashita** will not print bind related messages to the chat log._
  - `keyboard.windowskeyenabled` - _(boolean)_
    - **Default:** 0
    - Sets if the Windows key should be enabled and work like normal.
  - `mouse.blockinput` - _(boolean)_
    - **Default:** 0
    - Sets if **Ashita** should completely block all mouse input.
  - `mouse.unhook` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should unhook the mouse from being automatically repositioned by the game menu system.

### Section: `[ashita.misc]`

Contains configuration settings used for various **Ashita** related settings.

  - `addons.silent` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should stop announcing loading and unloading addons to the chat window.
  - `aliases.silent` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should stop announcing alias related command results to the chat window.
  - `plugins.silent` - _(boolean)_
    - **Default:** 1
    - Sets if **Ashita** should stop announcing loading and unloading plugins to the chat window.

### Section: `[ashita.polplugins]`

Contains the list of plugins **Ashita** will launch immediately as it injects. (IPolPlugin instances.)

{{% notice warning %}}
This does not work with normal plugins! This will only work for 'PlayOnline Plugins'.
{{% /notice %}}

This section expects each entry to be the name of the plugin and a boolean value (0 or 1) if it should be enabled.

```ini
[ashita.polplugins]
sandbox = 1
pivot = 0
```

_In this example, `Sandbox` would be loaded, but `Pivot` would not._

### Section: `[ashita.polplugins.args]`

Contains the plugin-specific arguments to pass to a 'PlayOnline Plugin' when its loaded.

This section expects each entry to be the name of the plugin and a string value of arguments to be passed to the plugin when its loaded. _In most cases, plugins will not require arguments to load and do not need an entry here. Consult the desired plugins documentation to see if any arguments are required._

As an example:

```ini
[ashita.polplugins.args]
sandbox = args1 args2 args3 args4
```

_This would pass the string `args1 args2 args3 args4` to `Sandbox` when its loaded._

### Section: `[ffxi.direct3d8]`

Contains configuration settings used to override Direct3D8 device creation parameters.

{{% notice warning %}}
**Note**: This is for advanced users only! Edit with caution!
{{% /notice %}}

  - `presentparams.backbufferformat` - _(number)_
    - **Default:** -1
    - Sets the back buffer format passed with the device creation present parameters.
  - `presentparams.backbuffercount` - _(number)_
    - **Default:** -1
    - Sets the back buffer count passed with the device creation present parameters.
  - `presentparams.multisampletype` - _(number)_
    - **Default:** -1
    - Sets the multisample type passed with the device creation present parameters.
  - `presentparams.swapeffect` - _(number)_
    - **Default:** -1
    - Sets the swap effect passed with the device creation present parameters.
  - `presentparams.enableautodepthstencil` - _(number)_
    - **Default:** -1
    - Sets the auto-depth stencil enabled flag passed with the device creation present parameters.
  - `presentparams.autodepthstencilformat` - _(number)_
    - **Default:** -1
    - Sets the auto-depth stencil format passed with the device creation present parameters.
  - `presentparams.flags` - _(number)_
    - **Default:** -1
    - Sets the flags passed with the device creation present parameters.
  - `presentparams.fullscreen_refreshrateinhz` - _(number)_
    - **Default:** -1
    - Sets the fullscreen refresh rate passed with the device creation present parameters.
  - `presentparams.fullscreen_presentationinterval` - _(number)_
    - **Default:** -1
    - Sets the fullscreen presentation interval passed with the device creation present parameters.
  - `behaviorflags.fpu_preserve` - _(number)_
    - **Default:** 0
    - Sets if the fpu preserve behavior flag is enabled by force.

_When set to -1, any of the above values in this section will use the current value already being used by the game._

### Section: `[ffxi.registry]`

Contains configuration settings used to override Final Fantasy XI's registry settings. These settings take priority over what is actually within the system registry for the game. A value of -1 means that **Ashita** will default to what value is already in the real registry for the given setting.

  - `0000` - _(number)_
    - **Default:** -1
    - **Recommended:** 6
    - Sets the games mip mapping setting.
    - Valid values: `0 = Off`, `1 = On, Lowest Quality` ... `6 = On, Best Quality`
  - `0001` - _(number)_
    - **Default:** -1
    - Sets the games window resolution width.
  - `0002` - _(number)_
    - **Default:** -1
    - Sets the games window resolution height.
  - `0003` - _(number)_
    - **Default:** -1
    - **Recommended:** 4096
    - Sets the games background resolution width.
    - _For best performance, this value is best if divisible by 2._
  - `0004` - _(number)_
    - **Default:** -1
    - **Recommended:** 4096
    - Sets the games background resolution height.
    - _For best performance, this value is best if divisible by 2._
  - `0005` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0006` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0007` - _(number)_
    - **Default:** -1
    - Sets if the games sound is enabled.
    - Valid values: `0 = Disabled`, `1 = Enabled`
  - `0008` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0009` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0010` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0011` - _(number)_
    - **Default:** -1
    - Sets the games environment animations mode.
    - Value values: `0 = Off`, `1 = Normal`, `2 = Smooth`
  - `0012` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0013` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0014` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0015` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0016` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0017` - _(number)_
    - **Default:** -1
    - **Recommended:** 1
    - Sets the games bump mapping.
    - Valid values: `0 = Off`, `1 = On`
  - `0018` - _(number)_
    - **Default:** -1
    - **Recommended:** 2
    - Sets the games texture compression level.
    - Valid values: `0 = High`, `1 = Low`, `2 = Uncompressed`
  - `0019` - _(number)_
    - **Default:** -1
    - **Recommended:** 1
    - Sets the games texture compression level.
    - Valid values: `0 = Compressed`, `1 = Uncompressed`
  - `0020` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0021` - _(number)_
    - **Default:** -1
    - **Recommended:** 1
    - Sets the games hardware mouse option.
    - Valid values: `0 = Off`, `1 = On`
  - `0022` - _(number)_
    - **Default:** -1
    - **Recommended:** 0
    - Sets the games show opening movie option.
    - Valid values: `0 = Off`, `1 = On`
  - `0023` - _(number)_
    - **Default:** -1
    - **Recommended:** 0
    - Sets the games simplified character creation visuals option.
    - Valid values: `0 = Off`, `1 = On`
  - `0024` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0025` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0026` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0027` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0028` - _(number)_
    - **Default:** -1
    - Sets the games gamma base.
    - _Float based value, 0 is the default game value._
  - `0029` - _(number)_
    - **Default:** -1
    - **Recommended:** 20
    - Sets the games maximum number of sounds.
    - Valid values: `12 = Lowest` ... `20 = Highest`
  - `0030` - _(number)_
    - **Default:** -1
    - Sets the games 3D LCD mode.
    - Valid values: `0 = Disabled`, `1 = Enabled`
  - `0031` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0032` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0033` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `0034` - _(number)_
    - **Default:** -1
    - Sets the games windowed mode.
    - Valid values: `0 = Fullscreen`, `1 = Windowed`, `2 = Fullscreen Windowed (Undocumented)`, `3 = Borderless Windowed`
    - _**Note:** There is a bug in the official client handling of this setting where `Borderless Windowed` is actually `Fullscreen Windowed`, and `Fullscreen Windowed` is actually `Borderless Windowed`._
  - `0035` - _(number)_
    - **Default:** -1
    - **Recommended:** 1
    - Sets the games sound always on option. _(Play sound while game is in background.)_
    - Valid values: `0 = Off`, `1 = On`
  - `0036` - _(number)_
    - **Default:** -1
    - **Recommended:** 2
    - Sets the games font compression.
    - Valid values: `0 = Compressed`, `1 = Uncompressed`, `2 = High Quality`
  - `0037` - _(number)_
    - **Default:** -1
    - **Recommended:** Use the same value as your window width resolution. (0001)
    - Sets the games menu resolution width.
  - `0038` - _(number)_
    - **Default:** -1
    - **Recommended:** Use the same value as your window height resolution. (0002)
    - Sets the games menu resolution height.
  - `0039` - _(number)_
    - **Default:** -1
    - Sets the games IME mode.
    - Valid values: `0 = v1`, `1 = v2`
  - `0040` - _(number)_
    - **Default:** -1
    - **Recommended:** 0
    - Sets the games graphics stabilization option.
    - Valid values: `0 = Off`, `1 = On`
  - `0041` - _(number)_
    - **Default:** -1
    - Sets the games beta UI option.
    - Valid values: `0 = Disabled`, `1 = Enabled`
    - _**Note:** This is not available in the retail client._
  - `0042` - _(string)_
    - **Default:** -1
    - Sets the games default screenshot path.
    - _**Note:** This path is only used for the games built-in screenshots. The included `Screenshots` plugin from **Ashita** does not use this path._
  - `0043` - _(number)_
    - **Default:** -1
    - Sets the games screenshot in screen resolution option.
    - Valid values: `0 = Off`, `1 = On`
    - _**Note:** The included `Screenshots` plugin from **Ashita** does not use this option._
  - `0044` - _(number)_
    - **Default:** -1
    - Sets the games maintain window aspect ratio option.
    - Valid values: `0 = Off`, `1 = On`
  - `0045` - _(number)_
    - **Default:** -1
    - Unknown / unused.
  - `padmode000` - _(number)_
    - **Default:** -1
    - Sets the games gamepad configuration settings. _(See below for more information.)_
  - `padsin000` - _(number)_
    - **Default:** -1
    - Sets the games gamepad button map settings. _(See below for more information.)_

#### `padmode000`

The `padmode000` value is a comma-separated list of booleans, such as: `1,1,1,1,1,0`. There are 6 options in total in the following order:

| Option | Description |
| --- | --- |
| `Enable Gamepad`          | Enables or disables the gamepad functionality. |
| `Enable Force Feedback`   | Enables or disables the gamepad force feedback (rumble) features. |
| `Enable Sliders`          | Enables or disables the gamepad slider controls. |
| `Enable Hat Switches`     | Enables or disables the gamepad hat switch controls. |
| `Enable When Inactive`    | Enables or disables the gamepad working if the game window is not focused. |
| `Enable XInput`           | Enables or disables if the gamepad should be detected as XInput or not. |

#### `padsin000`

The `padsin000` value is a comma-separated list of numbers. There are 27 options in total. Each 'slot' in this list represents an in-action and the value given for that slot is the button id mapped to it. _(**Note:** The button ids are different depending if XInput mode is enabled or not in the `padmode000` value!)_

The 27 slots are in the following order:

| Index | Action Description |
| --- | --- |
| 0     | Toggle auto-run. |
| 1     | Toggle CTRL macro bar display. |
| 2     | Toggle first/third person view. |
| 3     | Toggle ALT macro bar display. |
| 4     | Toggle /heal, lock target. |
| 5     | Cancel. |
| 6     | Main menu. |
| 7     | Select, Confirm selection. |
| 8     | Select active window. |
| 9     | Toggle menu/window visibility. |
| 10    | Menu navigation with movement thumbstick while held. |
| 11    | Move camera with movement thumbstick while held. |
| 12    | Toggle logout window. |
| 13    | Player movement. (up) |
| 14    | Player movement. (down) |
| 15    | Player movement. (left) |
| 16    | Player movement. (right) |
| 17    | Camera movement. (up) |
| 18    | Camera movement. (down) |
| 19    | Camera movement. (left) |
| 20    | Camera movement. (right) |
| 21    | Menu movement. (up) _(Also handles targeting.)_ |
| 22    | Menu movement. (down) _(Also handles targeting.)_ |
| 23    | Menu movement. (left) _(Also handles targeting.)_ |
| 24    | Menu movement. (right) _(Also handles targeting.)_ |
| 25    | Take screenshot. _(Menu/windows must be hidden.)_ |
| 26    | Toggle use of movement, menu and camera controls. |

#### DirectInput Button Mappings

{{% expand "Click to reveal the DirectInput button mapping information..." %}}
When `Enable XInput` within the `padmode000` is disabled, the button map values are:

  - `0` - Square
  - `1` - Cross (X)
  - `2` - Circle
  - `3` - Triangle
  - `4` - L1
  - `5` - R1
  - `6` - L2
  - `7` - R2
  - `8` - Select (PS5: Share)
  - `9` - Start (PS5: Option)
  - `10` - L3
  - `11` - R3
  - `12` - (PS5: PlayStation Button)
  - `13` - (PS5: Touchpad Button)
  - `14` - (PS5: Mute/Mic Button)
  - `32` - Left Thumbstick (Right / Left)
  - `33` - Left Thumbstick (Up / Down)
  - `34` - Right Thumbstick (Right / Left)
  - `37` - Right Thumbstick (Up / Down)
  - `40` - DPad (Right / Left)
  - `41` - DPad (Up / Down)

_**Note:** Under certain situations, the values of these buttons can be negative to reverse them. This is generally only done with the DPad and thumbsticks._

  - `-1` - None
  - `-32` - Left Thumbstick (Right / Left) [Reversed]
  - `-33` - Left Thumbstick (Up / Down) [Reversed]
  - `-34` - Right Thumbstick (Right / Left) [Reversed]
  - `-37` - Right Thumbstick (Up / Down) [Reversed]
  - `-40` - DPad (Right / Left) [Reversed]
  - `-41` - DPad (Up / Down) [Reversed]
{{% /expand %}}

{{% notice note %}}
The `FFXiPadConfig` tool does not handle DirectInput controllers fully the same way the actual game client does. The configuration tool only supports upto 32 buttons (ie. `DIJOYSTATE`) meanwhile the actual game client will support up to 128 buttons. (ie. `DIJOYSTATE2`) It is possible to map to these extra buttons by editing the `padsin000` value manually.
{{% /notice %}}

#### XInput Button Mappings

{{% expand "Click to reveal the XInput button mapping information..." %}}
When `Enable XInput` within the `padmode000` is enabled, the button map values are:

  - `0` - B
  - `1` - X
  - `2` - Y
  - `3` - A
  - `4` - DPad (Right)
  - `5` - DPad (Left)
  - `6` - DPad (Up)
  - `7` - DPad (Down)
  - `8` - LB _(aka L1)_
  - `9` - LT _(aka L2)_
  - `10` - L Stick Button _(aka L3)_
  - `11` - RB _(aka R1)_
  - `12` - RT _(aka R2)_
  - `13` - R Stick Button _(aka R3)_
  - `14` - Start
  - `15` - Back
  - `16` - None _(`-1` is also used to represent none.)_
  - `32` - Left Thumbstick (Right / Left)
  - `33` - Left Thumbstick (Up / Down) [Reverse]
  - `35` - Right Thumbstick (Right / Left)
  - `36` - Right Thumbstick (Up / Down) [Reverse]

_**Note:** Under certain situations, the values of these buttons can be negative to reverse them. This is generally only done with the DPad and thumbsticks._

  - `-1` - None
  - `-32` - Left Thumbstick (Right / Left) [Reverse]
  - `-33` - Left Thumbstick (Up / Down)
  - `-35` - Right Thumbstick (Right / Left) [Reverse]
  - `-36` - Right Thumbstick (Up / Down)
{{% /expand %}}
