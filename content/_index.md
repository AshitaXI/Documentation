---
title: "Index"
---

![ashita](./images/ashita.png?width=64px)
{.slim-img}

# Ashita

{{% button href="https://discord.gg/Ashita" icon="fa-brands fa-discord" %}}Discord Chat{{% /button %}}
{{% button href="https://github.com/AshitaXI" icon="fa-brands fa-github" %}}GitHub Group{{% /button %}}
{{% button href="https://github.com/AshitaXI/Ashita/issues" icon="fa-brands fa-github" %}}Bug Reports{{% /button %}}
{{% button href="https://docs.ashitaxi.com" icon="fa-solid fa-book" %}}Documentation{{% /button %}}
{.center}

---

Welcome to the **Ashita** project documentation website. This site is used to help users of **Ashita** get familiar with its features, commands, as well as help developers further extend the project via `plugins` and `addons`. Please use the sidebar to the left to navigate through the various pages of information, or, use the search bar at the top left to look for a specific bit of information.

## What is `Ashita`?

**Ashita** is a free feature-rich third-party enhancement/modification for the MMORPG, Final Fantasy XI.

**Ashita** operates by launching and directly injecting itself (`Ashita.dll`) into the games main process. _(Generally `pol.exe` unless using a modified boot loader for private servers.)_ Once injected, **Ashita** will begin applying custom hooks, patches and other modifications to the games memory. These include things like hooking onto the games chat and packet functions, allowing **Ashita** to see the games chat, commands and other text output along with the incoming and outgoing packets of the game.

**Ashita** can then further extend the client by adding its own commands, allowing for outputting custom text to the chat, injecting packets to the client and server, and much much more.

_(See the Features page for a full list of **Ashita's** features.)_

Players can also enjoy additional features provided by `plugins` and `addons` _(via the Addons plugin)_ which can be loaded within **Ashita**, directly in-game.

## Ashita's History

**Ashita** was originally created, by RZN, on Aug 19, 2011 and was originally named ‘FFACE 5’. The idea was to replace the FFACE project with a full windowing ability and feature set that would replace the traditional FFACE.dll.

### Ashita v1

Later, due to major design changes, adjustments and alterations the project was instead separated from the FFACE project and was given its name **Ashita** on Feb. 20, 2012.

Around version 1.0.0.10 of **Ashita**, atom0s had joined the project as a plugin developer with the means of becoming a core developer to help the project grow. After creating several key plugins that users were accustomed to from another project, atom0s began working with RZN on the core. Soon after atom0s became a core/lead developer with RZN on the whole project.

**Ashita** underwent lots of changes and improvements and partial rewrites of various parts of the core. Soon after, the project had grown in popularity and it saw many new third-party plugins from various players alike.

### Ashita v2

Due to limitations in how **Ashita** was currently coded, it was decided that a rewrite would be in the best interest of **Ashita**. atom0s began development on **Ashita** v2 shortly after the discussions.

Soon after, **Ashita** v2 was beginning beta testing and had its full release in early 2014. **Ashita** v2 brought many new things to the **Ashita** project such as:

  * Much cleaner and more optimized code base.
  * Much more flexible plugin system that would prevent plugins from breaking due to core updates.
  * Lots of bug fixes from **Ashita** v1 that were hard to track down in the old code base.
  * New font object system rewrite to make font objects even more customizable.
  * And much much more!

### Ashita v3

**Ashita** v3 was developed to better extend some of the functionality of callbacks to plugins from the core. At the time, v2 had some limitations on what could be done with certain events and it limited the abilities of some major plugins. v3 was discussed between some of the core developers on how to better extend these events and further improve the plugin system. Once some solid ideas were made, work on v3 began. **Ashita** v3 was started around October 2016 with the hopes to build out an even more enjoyable platform for players.

During the rewrite, atom0s took the time to further improve the core code of the project making it much easier to update various parts of the core for any additional major changes that may come to the project. Another key adjustment made here was the removal of the old AnTweakbar UI system in favor of the newly added ImGui system. This resulted in the project being rewritten rather than being adjusted. With some guidelines in place, atom0s began working on **Ashita** v3 in his spare time while still focusing on keeping v2 up to date and working properly. Some key points on what were focused on with **Ashita** v3 were:

  * Full rewrite to optimize and modernize the **Ashita** core. (C++11/14 features, cint types, etc.)
  * Core code cleanup and commenting, now making use of JSDoc style comments across the whole project.
  * Enhanced plugin system with better callbacks for things such as the packet handlers and similar.
  * Added and improved callbacks for things such as command handling and incoming/outgoing text.
  * Exposure of more Direct3D calls that are commonly used in hacks/cheats to assist with various things.
  * Removal of old unused things such as AnTweakBar UI system, which has been succeeded by the newer ImGui UI system.
  * Massive overhaul and cleanup of the plugin SDK (known as the ADK).
  * And much more!

_A full list of changes during this time were kept over on the forums here:_
https://forums.ashitaxi.com/viewtopic.php?f=15&t=66

_**Ashita** v3 is considered end of life and feature-complete as of 2022._

### Ashita v4

During the year 2018, internal discussions of how to improve parts of **Ashita** began. These discussions covered various aspects of things that were seen as shortcomings or means to better the project as a whole to add new features. While some discussions did turn into features added to the current v3 project, more larger scale changes or ideas were kept on hold for the potential future v4 project.

While some larger idea testing began towards the end of 2019, the more main focused development of v4 began in 2020.

Due to the larger scale goals and changes with the new ideas for v4, a full rewrite was again considered the best plan of action. However, larger portions of v3's current codebase could be easily reused while still focusing on refreshing different parts of the code that needed adjustments.

**Ashita** v4 entered semi-public beta testing on May 24th, 2020 via a Discord announcement seeking testers. Then, shortly after, on June 13th, 2020 public beta testing started.

_As of the writing of this documentation, **Ashita** v4 is still in beta testing._
