---
title: "Commands"
weight: 3
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

## Command Syntax

Commands implemented within **Ashita** all follow the below format for their arguments. This helps keep usage unified across all commands. It also makes documentation easier to follow when all commands make use of the same format.

| Syntax | Description |
| ---: | --- |
| `text`        | _Required; entered as shown._ |
| `<text>`      | _Required argument._ |
| `<text...>`   | _Required argument. (Multiple arguments accepted.)_ |
| `(text\|text)` | _Required, one of._ |
| `[text]`      | _Optional argument._ |
| `[text...]`   | _Optional argument. (Multiple arguments accepted.)_ |

_**Note:** Arguments surrounded with `<` and `>` are considered positional, meaning their order matters._


## Category: Ashita Related

### Command: `/about`

  - `/about`
    - _Toggles displaying the **Ashita** about/credits information._

### Command: `/ashita`

  - `/ashita`
    - _Toggles displaying the **Ashita** sidebar._

### Command: `/aver`, `/aversion`, `/ashitaversion`

  - `/aver`
  - `/aversion`
  - `/ashitaversion`
    - _Prints the current **Ashita** version information to the chat window._

## Category: General

### Command: `/paste`

  - `/paste`
    - _Pastes the current clipboard text to the chat input._

### Command: `/exit`, `/terminate`

  - `/exit`
  - `/terminate`
    - Closes the game client, by force._

{{% notice warning %}}
This does not gracefully close the game client, it is shut down by force. Settings may be lost while using these commands!
{{% /notice %}}

## Category: Scripts

### Command: `/exec`

  - `/exec <name> [args...]`
    - _Executes the given script file._

### Command: `/execstr`

  - `/execstr <string> [args...]`
    - _Executes the given script string._

### Command: `/pause`, `/sleep`, `/wait`

  - `/pause [delay]`
  - `/sleep [delay]`
  - `/wait [delay]`
    - _Suspends a script for an amount of time. (Default is 1 second if no delay is given.)_

{{% notice warning %}}
This command is not intended to be used outside of scripts! It will freeze the game client if you use it elsewhere.
{{% /notice %}}

## Category: Plugins

### Command: `/plugins`

  - `/plugins info <name>`
    - _Displays detailed information about a given loaded plugin._
  - `/plugins link <name>`
    - _Opens the given plugins link in the systems default browser._
  - `/plugins list`
    - _Opens a UI window displaying a list of plugins. (Not yet implemented.)_
  - `/plugins silent [0 | 1]`
    - _Toggles, or sets, if plugin commands should print messages to the chat window._

### Command: `/load`

  - `/load <name> [args...]`
    - _Loads the given plugin._

### Command: `/unload`

  - `/unload <name>`
    - _Unloads the given plugin._

### Command: `/unloadall`

  - `/unloadall`
    - _Unloads all currently loaded plugins._

### Command: `/list`

  - `/list`
    - _Lists all loaded plugins._

## Category: Alias & Binds

### Command: `/alias`

  - `/alias add <trigger> <command>`
  - `/alias <trigger> <command>`
    - _Adds an alias with the given trigger._
  - `/alias clear`
    - _Clears the list of registered aliases._
  - `/alias (del | delete) <trigger>`
    - _Deletes an alias._
  - `/alias list`
    - _Lists the current registered aliases._

### Command: `/bind`

  - `/bind block [0 | 1]`
    - _Toggles, or sets, blocking keybinds while game input is open._
  - `/bind list`
    - _Lists the current registered keybinds._
  - `/bind silent [0 | 1]`
    - _Toggles, or sets, if keybind commands should output messages to the chat window._
  - `/bind [!^@#+]<key> [down | up] <command>`
    - _Binds a key combination to the given command._

Keybinds make use of the `!^@#+` characters as modifiers. These characters represent:

  - `!` - Modifier symbol for the `ALT` key.
  - `#` - Modifier symbol for the `APPS` key.
  - `^` - Modifier symbol for the `CTRL` key.
  - `+` - Modifier symbol for the `SHIFT` key.
  - `@` - Modifier symbol for the `WIN` key.

### Command: `/unbind`

  - `/unbind all`
    - _Unbinds all registered keybinds._
  - `/unbind [!^@#+]<key> [down | up]`
    - _Unbinds a key combination._

## Category: Input Devices

### Command: `/controller`, `/gamepad`

  - `/controller (allowbackground | allowbg | bg) [0 | 1]`
  - `/gamepad (allowbackground | allowbg | bg) [0 | 1]`
    - _Toggles, or sets, if the gamepad should be accessible while the game is not in focus._
  - `/controller disable [0 | 1]`
  - `/gamepad disable [0 | 1]`
    - _Toggles, or sets, if the gamepad should be ignored/disabled._

{{% notice info %}}
If you do not use a control while playing, it is recommended to fully disable the gamepad to fix a potential micro-stutter the game will have.\
You can use the `/gamepad disable` command to fix this problem.
{{% /notice %}}

### Command: `/keyboard`

  - `/keyboard winkey [0 | 1]`
    - _Toggles, or sets, if the Windows key is enabled._

### Command: `/mouse`

  - `/mouse block [0 | 1]`
    - _Toggles, or sets, if the mouse should be blocked from sending input to the game._
  - `/mouse unhook [0 | 1]`
    - _Toggles, or sets, if the mouse should be unhooked from window snapping._

## Category: Direct3D

### Command: `/ambient`

  - `/ambient`
    - _Toggles the ambient lighting feature._
  - `/ambient [0 | 1]`
    - _Sets, or toggles, the ambient lighting feature off or on._
  - `/ambient <r> <g> <b>`
    - _Sets the ambient lighting color._

### Command: `/fillmode`

  - `/fillmode`
    - _Toggles the fillmode setting between solid and wireframe._
  - `/fillmode [value]`
    - _Sets the fillmode to the given value._

Valid fill mode values are:

  - `1` - Point
  - `2` - Wireframe
  - `3` - Solid

## Category: Addons

{{% notice note %}}
These commands require the `Addons` plugin to be loaded in order for them to work!
{{% /notice %}}

### Command: `/addon`

  - `/addon silent [0 | 1]`
    - _Toggles, or sets, if addon commands should print messages to the chat window._
  - `/addon load <name>`
    - _Loads the given addon._
  - `/addon unload <name>`
    - _Unloads the given addon._
  - `/addon unloadall`
    - _Unloads all currently loaded addons._
  - `/addon kill <name>`
    - _Kills the given addon._
  - `/addon reload <name>`
    - _Reloads the given addon._
  - `/addon exec <name> <str>`
    - _Executes a string of Lua code within the given addons state._
  - `/addon list`
    - _Lists all loaded addons._
  - `/addon info <name>`
    - _Displays detailed information about a given loaded addon._
  - `/addon link <name>`
    - _Opens the given addons link in the systems default browser._
