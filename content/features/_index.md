---
title: "Features"
weight: 10
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

**Ashita** comes packed full of various built-in features to greatly enhance a players experience. Complimenting the built-in features, **Ashita** also offers a feature-rich plugin SDK allowing developers to further enhance the game client. The included core plugin, `Addons`, also further extends how developers can further extend **Ashita** via Lua scripting.

{{% notice note %}}
This page will cover the various features included in **Ashita**, however it does not include built-in commands.\
Please refer to the [Commands](/commands/) documentation for more details about those.
{{% /notice %}}

{{% notice info %}}
Sections on this page will include collapsed information sections and screenshots.\
Be sure to expand them for more information and to see example screenshots!
{{% /notice %}}

## Command Line & Graphical Launchers

**Ashita** comes with two methods of launching and injecting itself into the game client.

  - The command line launcher. (`ashita-cli.exe`)
  - The graphical launcher. (`Ashita.exe`)

The command line launcher (`ashita-cli.exe`) can be used to quickly and easily launch a selected profile immediately. This is useful for those who run multiple characters and need to get running quickly. This bypasses any additional loading or processing for **Ashita** that the graphical launcher adds such as its auto-updates.

The graphical launcher instead is used for a more complete launching experience. It includes a full configuration editor, the ability to download most addons and plugins available, as well as keep things automatically up to date.

## Injected Hook

In order to offer the best level of customizations and features, **Ashita** operates by being directly injected into the game client process. Doing so gives **Ashita** direct access to the games functions and memory. This makes things such as function hooking, pointer usage and memory object wrapping much easier and with little to no overhead as an external program would have.

This also allows **Ashita** to take over parts of the client such as the Direct3D device, allowing **Ashita** to render its own content into/onto the game scene.

Being injected also allows **Ashita** to hook game functions allowing it to further extend things such as adding its own commands or overriding how existing commands function.

## Direct3D Hook

By being directly injected into the game client, **Ashita** hooks onto and fully wraps the games Direct3D device. This allows **Ashita** to render its own content into/onto the game scene. This also allows blocking various rendering calls (primitives), alter/block/change render states, and loads more graphics pipeline alterations. **Ashita** makes use of this hooking to allow itself to render additional information, custom fonts/primitives and a full UI system ontop of the game.

### Custom In-Game Fonts / Primitives

**Ashita** contains its own custom built-in font and primitive rendering systems which allow addons and plugins to further expand the information displayed by the game client. These two systems are designed to allow both basic text information to be displayed on-screen but also allow for building custom UI-like elements. _(However, this system is not designed or intended to be a full-scale UI renderer.)_

The current (and older) base font system makes use of Direct3D and GDI directly to render text ontop of the scene. Due to how this system works, fonts may not look as great as they should as the general GDI handling of text does not include more modern features such as proper aliasing, kerning, and more.

Primitives are designed to be able to handle two different styles of rendering. The first is just a basic rectangle rendering mode to display boxes, generally behind text to make things easier to see/read. The other is to allow rendering sprites, which enables rendering images to the screen.

The font system also includes a custom inline coloring setup, similar to what is used in modern triple-A games, such as World of Warcraft. This allows users to easily make colorful text to help uniquely display various information.

For example, you can render some text as blue like this: `|cFF0000FF|This is some blue text!|r`

{{% expand "Click to show some screenshots of various font and primitive usages.." %}}
![d3d_fonts_fps_clock.png](/features/images/d3d_fonts_fps_clock.png)
{.slim-img}
_The FPS and clock addons displaying some basic text._
{.center}
![d3d_fonts_recast.png](/features/images/d3d_fonts_recast.png)
{.slim-img}
_The recast addon displaying some cooldown timers. Including color changes for timers almost expiring._
{.center}
{{% /expand %}}

### In-Game UI (ImGui)

While the font and primitive systems offer some means of creating custom user interfaces, they lack the ability to make things more contextual and in-depth. Instead, **Ashita** also includes `ImGui` to allow developers of addons and plugins to create feature-rich user interfaces. ImGui comes stock with many different control types such as:

  - Labels / Text
    - Basic, wrapped, colored, etc.
    - Bulleted
  - Buttons
    - Small, invisible, arrow, etc.
    - Radio Buttons
  - Checkbox
  - Progress Bars
  - Images
  - Combo Boxes
  - List Boxes
  - Drags & Sliders
  - User Input
    - Text
    - Int / Float (Single, double, triple, quad value inputs.)
    - Scalar / ScalarN
  - Color Editors
  - Tree Nodes
  - Selectables
  - Plotting
    - Lines
    - Histograms
  - Menus / Menu Bars
  - Tooltips
  - Popups / Modals
  - Tables
  - Columns
  - Tabs / Tab Bars
  - And more!

You can find more information about ImGui here: <https://github.com/ocornut/imgui>

{{% expand "Click to show screenshots of ImGui being used.." %}}
![d3d_imgui_blucheck.png](/features/images/d3d_imgui_blucheck.png)
{.slim-img}
_Blucheck addon used to display BLU spell information._
{.center}
![d3d_imgui_minimap.png](/features/images/d3d_imgui_minimap.png)
{.slim-img}
_Minimap configuration editor used to customize the Minimap plugin._
{.center}
![d3d_imgui_renamer.png](/features/images/d3d_imgui_renamer.png)
{.slim-img}
_Renamer addon used to easily rename entities._
{.center}
{{% /expand %}}

### Ambient Lighting

![d3d_ambient.png](/features/images/d3d_ambient.png)

While in certain zones and depending on graphics settings, it can become hard to see various parts of the game world. **Ashita** comes stock with the ability to alter the games ambient lighting. _In most cases, users will just toggle this on and off as needed with the stock white color, however you can set the color hue used with the ambient lighting to your liking as well._

### Fill Mode

![d3d_fillmode.png](/features/images/d3d_fillmode.png)

As a fun extra, **Ashita** also has the ability to change the games current Direct3D fill mode. This is generally used to toggle wireframe mode on and off. This feature can allow you to see through walls, easily target something that may be behind something or otherwise obstructed from your view, etc.

## DirectInput / XInput Hooks

Similar to the Direct3D hook, **Ashita** also hooks onto the DirectInput device and wraps any device creations used for input to the game client. _(ie. Keyboard, Mouse, Controller)_ The keyboard and mouse are hooked and wrapped to allow **Ashita** to both interact with its own objects (fonts, primitives, ImGui, etc.) but also to allow further extending the devices capabilities, with things such as keybinds.

For controllers, **Ashita** handles both DirectInput and XInput devices, allowing for addons and plugins to take full control of the button presses and overall controller usage.

### Keyboard & Mouse

By hooking onto the keyboard and mouse devices, **Ashita** is able to do a number of useful features.

  - Handle input from either device before the game sees it, allowing **Ashita** to pass the input to its own objects to handle first. _(Fonts, Primitives, ImGui, addons/plugins, etc.)_
  - Block the input from reaching the game.
  - Inject input not actually done by the user. _(ie. Controlling the game externally.)_
  - Create custom binds to trigger various functionality when desired buttons or button combinations are pressed.
  - Enable or disable the Windows key on the fly.

Plugins can also register to callback events to react to, alter or block input from the keyboard and mouse.

**Ashita** offers a rich custom keybind system for the keyboard, including modifier keys such as:

  - `!` - Modifier symbol for the `ALT` key.
  - `#` - Modifier symbol for the `APPS` key.
  - `^` - Modifier symbol for the `CTRL` key.
  - `+` - Modifier symbol for the `SHIFT` key.
  - `@` - Modifier symbol for the `WIN` key.

For example, you can bind `CTRL+ALT+F1` to `/wave` like this: `/bind ^!F1 /wave`

### Controllers

`Final Fantasy XI` supports both DirectInput and XInput controller devices. **Ashita** is able to hook onto and handle both of these interfaces. The controller API allows addon and plugin developers to easily monitor for, override and inject controller input easily.

**Ashita** offers the ability to easily toggle some additional controller features on the fly:

  - `Background Controller Usage` - Easily toggle if the gamepad should work while the game is out of focus.
  - `Disable Gamepad Enumeration` - Easily disable the game from trying to find controllers. _(This is a useful feature to remove a known stutter issue that DirectInput causes when no gamepad is found.)_

## Hooked Win32 API

In order for **Ashita** to fully function, it must hook several Win32 API that the game makes use of. Some of these are for cosmetic purposes, while others are required to prevent certain issues from happening within the client. Below is a list and quick rundown of each API that is hooked and why:

  - **d3d8.dll**
    - `Direct3DCreate8` - _Hooked to catch the Direct3D device creation and wrap it._
  - **dinput.dll**
    - `DirectInput8Create` - _Hooked to catch the DirectInput device creation and wrap it and all created devices._
  - **xinput1_3.dll**
    - `XInputGetState` - _Hooked to obtain and modify the XInput device gamepad state._
  - **advapi32.dll**
    - `RegQueryValueExA` - _Hooked to allow **Ashita** to control the game configurations without relying on the actual registry values._
  - **kernel32.dll**
    - `CreateMutexA/CreateMutexW` - _Hooked to rename mutex objects to be unique per-`Final Fantasy XI` instance._
    - `OpenMutexA/OpenMutexW` - _Hooked to rename mutex objects to be unique per-`Final Fantasy XI` instance._
    - `ExitProcess` - _Hooked to catch unexpected client closes to cleanup **Ashita**'s resources._
    - `SetPriorityClass` - _Hooked to force `Final Fantasy XI` to always be set to `NORMAL_PRIORITY_CLASS`._
  - **user32.dll**
    - `CreateWindowExA` - _Hooked to catch the creation of the `Final Fantasy XI` window and store / modify its properties._
    - `CreateWindowExW` - _Hooked to catch the creation of the POL window and store / modify its properties. Also catches the creation of the mask windows and forces them to be hidden._
    - `GetForegroundWindow` - _Hooked to fake if `Final Fantasy XI` is the current foreground window to prevent the client from closing itself under certain window mode conditions._
    - `GetFocus` - _Hooked to fake if `Final Fantasy XI` is the current foreground window to prevent the client from closing itself under certain window mode conditions._
    - `GetSystemMetrics` - _Hooked to correct the mouse position under certain windowed mode conditions._
    - `GetWindowTextA` - _Hooked to modify the `PlayOnline` window caption._
    - `GetWindowTextW` - _Hooked to modify the `PlayOnline` window caption._
    - `LoadBitmapW` - _Hooked to alter the splash screen displayed when PlayOnline is launched._
    - `RegisterClassA` - _Hooked to alter the window icons for any created windows for `PlayOnline` and `Final Fantasy XI`._
    - `RegisterClassW` - _Hooked to alter the window icons for any created windows for `PlayOnline` and `Final Fantasy XI`._
    - `RegisterClassExA` - _Hooked to alter the window icons for any created windows for `PlayOnline` and `Final Fantasy XI`._
    - `RegisterClassExW` - _Hooked to alter the window icons for any created windows for `PlayOnline` and `Final Fantasy XI`._
    - `RemoveMenu` - _Hooked to reenable the close window button of the `Final Fantasy XI` window._
    - `SendMessageA` - _Hooked to alter the window icons for any created windows for `PlayOnline` and `Final Fantasy XI`._
    - `SetCursorPos` - _Hooked to prevent the game from snapping the mouse cursor to menus, if desired._
    - `SetFocus` - _Hooked to fake if `Final Fantasy XI` is the current foreground window to prevent the client from closing itself under certain window mode conditions._
    - `SetForegroundWindow` - _Hooked to fake if `Final Fantasy XI` is the current foreground window to prevent the client from closing itself under certain window mode conditions._
    - `SetWindowsHookExA` - _Hooked to override the used thread id for input purposes._
    - `SetWindowTextA` - _Hooked to modify the `PlayOnline` window caption._
    - `SetWindowTextW` - _Hooked to modify the `PlayOnline` window caption._

## Hooked Game Functions

Similar to hooking Win32 API, **Ashita** hooks onto several game functions to allow itself to intercept certain information before the game. These include:

  - `(Chat) CommandCalc` - _The game function responsible for interpreting and handling commands being processed by the client._
  - `(Chat) CTkMsgWinData::AddString` - _The game function responsible for outputting messages to the chat windows._
  - `(Chat) FsWordCompletion::lookUp` - _The game function responsible for parsing auto-translate words and phrases._
  - `(Packets) enAcvGet` - _The game function responsible for receiving, decrypting and decompressing an incoming packet chunk._
  - `(Packets) enAcvSet` - _The game function responsible for compressing and encrypting an outgoing packet chunk._

By hooking onto these functions, **Ashita** is able to do multiple things to their parameters / data, including:

  - **Read**: See any time the function(s) are called and log, view, or react to the parameters they were called with.
  - **Block**: Prevent the game client from ever seeing the call was made.
  - **Modify**: Alter the parameters to change how the call will actually be invoked by the game client.
  - **Inject**: Manually invoke the original function to easily inject custom data.

{{% expand "Click here for an example of how hooks work..." %}}
To better demonstrate and explain how hooking works, and what benefits it brings, let's take a closer look a the `(Chat) CommandCalc` function.

This function is responsible for processing all commands that are being handled within the client.\
This function is called anytime the client is handling a command that should be interpreted. This includes things such as:

  - The player first logged in, `/servmes` is automatically processed and sent to obtain the current server message.
  - The player manually typed in a message or command into the chat window.
  - The player pressed a macro. _(Each line of the macro will be sent through this function.)_
  - The player selected an option through a menu, such as to attack a target, use a spell, tried to fish, etc.

The function looks like this internally:

```cpp
int32_t __cdecl CommandCalc(char* command, uint32_t mode)
{
    // Function body removed for simplicitys sake..
    return 0;
}
```

Each time a command or message is being processed by the client, it will first pass through this function. Once hooked, **Ashita** will attempt to handle the command first. It does so by passing the function arguments around internally to a few different steps to see if any loaded plugin or addon can handle the command, then finally trying to handle the command itself if nothing else has yet.

Using pseudo code, this is how the hook looks once applied:

```cpp
int32_t __cdecl CommandCalc(char* command, uint32_t mode)
{
    // Allow loaded plugins to handle the command first..
    if (AshitaCore::instance().m_PluginManager->HandleCommand(mode, command, false) ||
        AshitaCore::instance().m_PolPluginManager->HandleCommand(mode, command, false))
        return 0;

    // Allow Ashita to handle the command next..
    if (AshitaCore::instance().m_ChatManager->HandleCommand(mode, command, false))
        return 0;

    // Allow the game to finally handle the command as normal if nothing else did first..
    return Real_CommandCalc(command, mode);
}
```

_**Note:** **Ashita** does additional things in this hook, however to keep the pseudo code simple, other code has been removed._

To explain the call chain that takes place once the function is hooked, here's a quick rundown.\
As an example, we'll assume the player typed `/wave` into the chat input.

  1. The player opens the chat input and types the command: `/wave`
  2. The game client invokes the input callback function to handle when input has been entered.
  3. The input callback invokes: `CommandCalc("/wave", 1);`
  4. The `CommandCalc` begins execution _(executes its prologue code)_ then jumps to the **Ashita** hook callback.
  5. **Ashita** begins attempting to handle the command by doing the following:
      1. The command is passed to the `PluginManager` to allow loaded plugins to try and handle the command.
          - _If the `Addons` plugin is loaded, then the command is passed to all loaded addons to allow them to try to handle the command._
      2. The command is passed to the `PolPluginManager` to allow loaded POL plugins to try and handle the command.
      3. The command is passed to the `ChatManager` to allow **Ashita** to try and handle the command internally.
  6. **Ashita** returns back to the `CommandCalc` function, which then continues based on the return from **Ashita**.
      1. If **Ashita** considered the command handled:
          - The rest of the `CommandCalc` function is skipped, preventing the game from seeing the command.
      2. If **Ashita** considered the command unhandled:
          - The rest of the `CommandCalc` function is executed, allowing the game to handle the command as normal.
  7.  The `CommandCalc` ends execution _(executes its epilogue code)_ and returns.

During this entire chain, any loaded plugin (or addon if the `Addons` plugin is loaded) has the chance to either block or alter the command being handled. For example, if the command being handled is `/wave`, a plugin could instead tell the game to handle it as `/dance`. Or, the plugin can out-right block the command from being seen by the game at all.

Along with being able to see, block and/or modify the parameters of the function, by hooking the call **Ashita** also gains the ability to directly call the original function. This allows **Ashita** to directly inject message/command input to the game. This allows plugins (or addons) to directly inject commands as they see fit, giving the player even more control.
{{% /expand %}}

## Hooked Function Features

While some of the hooks listed above are done to ensure stability and prevent the client from having issues with things such as ALT+Tabbing, some of the hooks are used to implement some cosmetic features.

### Virtualized Registry Settings

`Final Fantasy XI` stores it's client configurations within the Windows system registry. Things such as the games various resolutions, window mode, sound and graphics settings, etc. are stored here. _(Generally, anything used at the time of the creation of the game window and devices is stored here. In-game settings are not.)_ When dualboxing or dual-installing, it is easy to cause bugs or issues with multiple loaders trying to use the same registry settings. To avoid these issues, **Ashita** virtualizes these settings causing the game client to not actually touch the registry for its settings.

Instead, the configuration settings that would normally be found in the registry are stored in each boot configuration used to launch **Ashita**. This allows players to easily configure and customize every configuration differently for all their characters.

{{% notice note %}}
New with **Ashita** v4 is a plugin called `Sandbox`. This plugin fully virtualizes the game client install allowing it to run entirely without being installed. _(No registry headaches or DLL registrations at all!)_
{{% /notice %}}

### Custom Window Icon

**Ashita** replaces the window icons used for both the `PlayOnline` and `Final Fantasy XI` windows. This is done to help users easily see which game clients are affected/hooked by **Ashita** while playing.

### Custom Window Title

**Ashita** replaces the window titles for both the `PlayOnline` and `Final Fantasy XI` windows.

  - The `PlayOnline` window title is changed to include the current **Ashita** project version that is injected.
  - The `Final Fantasy XI` window title is changed to the current logged in players name. This makes it very easy to switch between different clients by being able to quickly see which window is taking focus.

### Log File Fix

When `Final Fantasy XI` was originally designed and then ported to PC, it was designed in a manner that was not dual-box friendly. The game was originally forced into fullscreen mode and trying to ALT+Tab would cause the game to crash. _(Fixing this was the original purpose and goal of windowing the game.)_ However, even though bypassing this limitation is no longer needed as the game supports proper windowed mode itself now, SE never fixed the other shortcomings that happen when trying to run multiple instances of the game.

One of those is that the game stores and uses log files on disk to handle the text within the chat windows. When you expand the windows to read the backlog, these log files are referenced to load previous chat output history. If you are dualboxing, then trying to open the chat log can lead to the window output disappearing, becoming corrupt, or completely crashing the game.

**Ashita** includes a custom patch/fix to create individual folders and log files for each character that is logged in, this way there are no more log conflicts.

## Detailed Logging

To help with debugging and other general troubleshooting, **Ashita** includes a full logging system. Detailed logging information is output to these files found within the `/logs/` folder. The output of these files is based on the logging level you have currently set in the loaded boot configuration file.

## Configuration Files (.ini Backed Files)

**Ashita** includes an optional custom configuration file system that can be used to easily load and save configurations. These configuration files are backed using the well known `.ini` file format making it easy to read/write values from and to.

## Memory Manager

In order to create feature-rich plugins, it is important to be able to access various parts of the game client data. Things such as the local players information like inventory data, current equipment, etc. **Ashita** includes a `MemoryManager` object that exposes several frequently accessed memory objects directly to plugins in a manner that helps limit the requirement of recompiling plugins after a major game update. _(See plugin info below for more details.)_

## Pointer & Offset Manager Caching

To help with performance, **Ashita** includes internal pointer and offset managers to cache known information that will not change during the runtime of the client. These are pointers and offsets used to locate important information within the client, such as object pointers to data, function pointers, etc.

By using these managers, the values are automatically cached after their first use, making all following usages of the same data instant.

## Pointer & Offset Overrides

**Ashita** makes use of `.ini` configuration files to load its pointer and offset information. Along with these files, there are custom override files that server owners can make use of when using **Ashita** to version lock to an older client. If that client has a specific different pointer signature for some important data or function, the custom override files can be used to ensure the client will operate properly with **Ashita**, within reason.

{{% notice warning %}}
While these files make it possible to keep pointers and offsets proper, it is not possible to realign structures properly. Due to this, it may be impossible to lock to an older client if changes to a structure land up breaking how **Ashita** would normally function.
{{% /notice %}}

## Custom Commands

**Ashita** comes equipped with several useful built-in functionality, mainly focused on controlling the internal aspects of the hook. _Additional commands are generally implemented via a plugin or an addon._

Please see the full [Commands](/commands/) documentation for more information on the built-in commands.

## Custom Scripting (Extended Macros)

To assist with the limitations of the games macro system, **Ashita** includes its own custom text-based scripting engine. These are basic command scripts that you can use to write out much longer macros along with some basic level scripting to control Ashita, plugins, addons and more.

Scripts can be executed via the `/exec` command.

### Script Arguments

New with v4 is the ability to pass arguments to scripts that can be tokenized within a script. This allows players to even further create more in-depth scripts.

{{% expand "Click here to see an example of using script arguments.." %}}
Arguments are handled via tokens. These tokens are formatted as `%0%` where 0 is the number of the argument to be replaced with.

For example, take this script (`/scripts/wave.txt`):

```
/wave %0%
```

And execute it via: `/exec wave.txt Atomos`

This will attempt to wave at an entity named Atomos.
{{% /expand %}}

### Script Includes

Another new to v4 feature for scripts is the ability to directly include another script. Previously, the only way to do this kind of thing was to execute a second script via `/exec` within another script. However, this had the downside of none of the commands being executed in any kind of guaranteed order.

With v4, scripts now have a preprocessor step that will look for new commands/keywords (such as `/include`) and rebuild the script on the fly before it is executed. Script execution order is now guaranteed when you make use of the new `/include` command from within a script.

{{% expand "Click here to see an example of using script includes.." %}}
![script_includes.png](/features/images/script_includes.png)
{.slim-img}

As demonstrated in the above screenshot, when running scripts directly within another script via `/exec` the order that commands are executed is not guaranteed. This is because the commands get queued into a thread pool and are executed in any order the pool wishes. However, while using `/include`, scripts can guarantee the order that commands get executed as the script is rebuilt on the fly via preprocessing before its fully executed.
{{% /expand %}}

## Feature-Rich Plugins & Plugins SDK

While the main **Ashita** hook/core is closed source, we offer everyone the ability to help extend the projects capabilities with our open source plugin SDK. The SDK is designed to make development of plugins for **Ashita** extremely quick and easy, along with helping keep the requirement of maintaining your plugin simple.

{{% notice note %}}
The **Ashita** plugin SDK is designed for use with C++ and assumes your compiler will support the latest C++ standard features. While other languages should be able to implement the SDK, the **Ashita** development team will only give support to those writing plugins in C++
{{% /notice %}}

For those seeking to implement the SDK in another language, your language will need to support the following:

  - The ability to specifically implement calls as `__stdcall` calling convention.
  - The ability to properly export unmangled functions from your compiled DLL.
  - The ability to properly implement a C++ style object that properly inherits from the `IPlugin` object within the SDK.

_Failure to follow these guidelines will most likely result in your plugin crashing the client!_

### Open Source

Our plugin SDK is completely free and open source. Anyone is welcome to write plugins for **Ashita**!

By using the `Addons` plugin you can also make use of the SDK through the means of Lua based scripting, in the form of addons. _(These are basically mini-plugins written in Lua.)_

### Easy To Use

The plugin SDK is designed to be easy to read, quick to understand, and fast to implement.

Because of this and with the use of our example plugin template, you should be able to get a plugin compiled and running within minutes of getting started.

We also include several helper headers to make use with in your plugin. These include:

  - `/d3d8/...` - Contains the various Direct3D8 headers and libs used by the Ashita project that plugins may need to compile against.
  - `/ffxi/...` - Contains `Final Fantasy XI` related structure definitions for various objects of the games memory.
  - `BinaryData.h` - Contains helper functions for working with bit level data. _(Generally used with packets.)_
  - `Chat.h` - Contains definitions and helper functions for working with `Final Fantasy XI`'s chat window output.
  - `Commands.h` - Contains helper functions for parsing and working with command arguments.
  - `ErrorHandling.h` - Contains Ashita's custom exception object and scoped translator helper for catching exceptions easily.
  - `ImGuiFontAwesome.h` - Contains definitions for using FontAwesome with ImGui.
  - `Memory.h` - Contains helper functions for working with memory related information.
  - `Registry.h` - Contains helper functions for working with `Final Fantasy XI`'s registry information.
  - `ScopeGuard.h` - Implements a basic scope guard helper to execute functions when leaving a given scope.
  - `Threading.h` - Implements various thread based objects. (Event, LockableObject, Thread)
  - `imgui.h` - Exposes ImGui to the plugin SDK, contains and implements the IGuiManager interface for the SDK.

### Easy Maintenance

Within a plugin, it is common to want to make use of game related object information, such as:

  - Accessing your party member information.
  - Accessing your own player information.
  - Accessing information about your equipment.
  - Accessing information about your inventory.
  - Accessing information about your current target.
  - etc.

The main two methods of doing this are either tracking the information via packets, or reading them from memory. To avoid potential ban issues, **Ashita** opts to do everything through memory. _(Plugins are free to use packets if they wish though.)_ An issue with plugins using any kind of data like this (memory or packets) is that the game can update and alter the structure of the data. If there are 15 plugins that make use of the inventory structure and the game updates and breaks this structure, then all 15 plugins would require being updated and recompiled to work again.

To fix this kind of plugin maintenance nightmare, **Ashita** has wrapped and implemented custom memory objects around the most commonly used memory structures. Instead of plugins directly accessing the memory objects themselves, they can instead use the wrappers exposed through **Ashita**'s `MemoryManager` object.

Now if those same 15 plugins instead make use of the `MemoryManager` object wrapper for the inventory, if the game updates again and breaks the structure, only **Ashita** needs to be updated. Once it is, all 15 plugins will continue working as normal without needing to be updated or recompiled.

### Performance First

**Ashita** aims to be as optimized as possible, putting performance first whenever it can. Our plugin SDK is no exception to this. Plugins are implemented in a manner that is focused on ensuring they do not cause more of an impact on performance than they should.

Plugins operate mainly through event callbacks. These are exposed to plugins via the `IPlugin::HandleXXX` calls, that can be overridden. Each of these functions are considered part of a given event category. In order for a plugin to receive a given event, it must tell the core that it uses that event via the return value it gives within the `IPlugin::GetFlags` function.

{{% notice note %}}
To help keep performance high, plugins should only ever request events they actually use. For example, if your plugin does not use either packet event, then don't return `Ashita::PluginFlags::UsePackets` as part of your plugins flags.
{{% /notice %}}

### Plugin Arguments

When a plugin is loaded, it is passed the entire command line that was passed to load it. This allows plugins to react to specific parameters when being loaded or require some bit of information before being loaded. _While not encouraged, as an example, you could use this as a means of locking your plugin behind a password._

## POL Plugins

While normal plugins have been a normal feature of **Ashita** since the start, v4 has introduced a new kind of plugin, called `POL Plugins`. These are special plugins that are loaded immediately when **Ashita** is first injected into `PlayOnline` _(or the given boot loader)_. These allow a developer to target `PlayOnline` specific tasks or just access a lower level means of interacting with the client in general.

An example use of this new plugin system is the new v4 plugin, `Sandbox`. _(See further below for more information.)_

Like normal plugins, `POL Plugins` inherit from a base object, to be properly implemented. This time being `IPolPlugin` instead of `IPlugin`.

{{% notice warning %}}
Due to when they are loaded, `POL Plugins` have less access to various events and must be coded with a bit more care to prevent crashes. Because they are loaded right at the launch of the client, many of **Ashita**'s objects are not created/initialized yet.
{{% /notice %}}

## Internal DAT Parsing (`ResourceManager`)

In order to make use of various game related information, **Ashita** includes its own internal DAT parser system. This includes the ability to read several types of the games resources that are stored within the DAT files found within the various `ROM` folders and expose the information back to developers.

The `ResourceManager` includes the ability to parse information such as:

  - Ability and spell information.
  - Item information.
  - Dialog tables.
  - String tables.
  - Status icons.

Developers can then make use of the `ResourceManager` to lookup and reference this information with the various functions exposed for each type of information.

**Ashita** comes preconfigured to read most important information that developers would want access to. This includes the following:

  - `(strings)` Ability Names
  - `(strings)` Ability Descriptions
  - `(strings)` Spell Names
  - `(strings)` Spell Descriptions
  - `(spdata)` Ability and Spell Information _(ie. Mana/TP cost, valid targets, ranges, level requirements, etc.)_
  - `(status icons)` Status Icon Information _(Icon image, cancel flag, hidden timer flag, etc.)_
  - `(strings)` Action Messages
  - `(strings)` Augments
  - `(strings)` Buff Names _(Full and log based names.)_
  - `(strings)` Game Command Help
  - `(strings)` Game Weekdays
  - `(strings)` Game Directions
  - `(strings)` Emotes
  - `(strings)` Equipment Slot Names
  - `(strings)` Equipment Slot Names (old)
  - `(strings)` Job Points
  - `(strings)` Job Points (Gifts)
  - `(strings)` Job Names
  - `(strings)` Job Names (Abbreviations)
  - `(strings)` Key Item Names _(Full and plural.)_
  - `(strings)` Key Item Descriptions
  - `(strings)` Merits
  - `(strings)` Monster Ability Names
  - `(strings)` Monster Groups _(Full and plural.)_
  - `(strings)` Moon Phases
  - `(strings)` Mount Names
  - `(strings)` Mount Descriptions
  - `(strings)` Race Names
  - `(strings)` Region Names
  - `(strings)` Titles
  - `(strings)` Weather Names
  - `(strings)` Weather Effect Names
  - `(strings)` Zone Names
  - `(strings)` Zone Names (Abbreviations)
  - `(strings)` Zone Names (Search Abbreviations)
  - `(items)` Armor
  - `(items)` Currency
  - `(items)` General
  - `(items)` Instinct
  - `(items)` Monstrosity
  - `(items)` Puppet
  - `(items)` Slips
  - `(items)` Usable
  - `(items)` Weapons
