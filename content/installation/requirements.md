---
title: "System Requirements"
weight: 1
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

In order to make use of **Ashita**, there are some requirements you will need to install. While some of these are optional, it is suggested to install everything listed on this page to ensure anything you may use with **Ashita**, or additional third-party tooling, works without dependency issues.

## Supported Operating Systems

**Ashita** supports the following operating systems:

  - Windows 7 _(Must install latest service packs.)_
  - Windows 8, Windows 8.1
  - Windows 10
  - Windows 11

{{% notice warning %}}
While **Ashita** may work on other operating systems not listed above, we do not give any kind of direct support for them!
{{% /notice %}}

## Game Client

Due to how changes can happen with the game client, not all client versions are supported. **Ashita** v4 targets the latest retail client, but can work with older clients.

The current release of **Ashita** v4 requires, at minimum, the following client version _(or newer)_ in order to fully work properly: `Nov. 10, 2021`

## System Requirements

Your system should meet the following recommended requirements (as of January 2020):

|| Recommended Requirements |
| ---: | --- |
| **Operating System**    | Windows® 8.1 / 10* |
| **CPU**                 | Intel® Core™ i3 2.4GHz (or higher) |
| **Memory**              | 2GB or more |
| **Graphics Card**       | NVIDIA® GeForce® GT 740 (or higher) _(Driver must be compatible with DirectX® 8.1.)_ |
| **Sound Card**          | DirectX®8.1 compatible sound card |
| **HDD/SSD**             | 15GB or more free space. |
| **Internet Connection** | Continuous internet connection required. |
| **Other**               | Keyboard, mouse, Gamepad, DirectX®8.1 _(Must have DirectX® End-User Runtime installed.)_ |

_The game client should still work on Windows 7 with the latest service packs installed, however it is not directly supported by SE. Certain Windows 10 updates may cause the game client to work improperly._

## Game Requirements

In order to launch and play `Final Fantasy XI` itself, you must have the following installed:

  - [Download](https://www.microsoft.com/en-us/download/details.aspx?id=8109) - `DirectX Runtime (June 2010)`

### Enabling DirectPlay

`Final Fantasy XI` makes use of `DirectPlay` as well and on newer operating systems (Windows 8 and newer) you may need to manually enable this feature. You can enable this via the following steps:

  1. Press the `Windows` key on your keyboard or manually open the start bar.
  2. Type `Control Panel` and select `Control Panel` from the list of results to open.
  3. Depending on the view displayed, click the following button:
      - `Programs` -> `Uninstall a Program`
      - `Programs & Features`
  4. On the left side bar, click the `Turn Windows features on or off` .
  5. Locate `Legacy Components` and expand it to reveal its additional options.
  6. Check `DirectPlay` in the list.
  7. Click `Ok` to save the changes.

## .NET Frameworks

**Ashita**, and many other third-party tools, makes use of the .NET Framework from Microsoft. There are several versions of the framework that you may want to install to best support as many tools as possible. We mainly recommend installing the following versions:

  - [Download](https://www.microsoft.com/en-us/download/details.aspx?id=17718) - `.NET Framework 4.0`
  - [Download](https://www.microsoft.com/en-us/download/details.aspx?id=42642) - `.NET Framework 4.5.2`
  - [Download](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net48) - `.NET Framework 4.8`
  - [Download](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net481) - `.NET Framework 4.8.1`

## Microsoft VC++ Redistributables

**Ashita** is developed and compiled on Windows using `Microsoft Visual Studio 2022`. Because of this, users will need to install the below VC++ Redist. packages. The latest package is required for **Ashita**, however you may want to install the previous versions as well to ensure the best compatibility with all other third-party tools and third-party plugins.

**Required:**

  - [Download](https://aka.ms/vs/17/release/vc_redist.x86.exe) - `VC++ Redist. 2015, 2017, 2019, 2022`

**Optional (but recommended):**

  - [Download](https://www.microsoft.com/download/details.aspx?id=26347) - `VC++ Redist. 2005 SP1`
  - [Download](https://download.microsoft.com/download/5/D/8/5D8C65CB-C849-4025-8E95-C3966CAFD8AE/vcredist_x86.exe) - `VC++ Redist. 2008 SP1`
  - [Download](https://download.microsoft.com/download/1/6/5/165255E7-1014-4D0A-B094-B6A430A6BFFC/vcredist_x86.exe) - `VC++ Redist. 2010 SP1`
  - [Download](https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe) - `VC++ Redist. 2012 Update 4`
  - [Download](https://aka.ms/highdpimfc2013x86enu) - `VC++ Redist. 2013`

