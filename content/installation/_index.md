---
title: "Installing Ashita"
weight: 30
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

{{% notice info %}}
This page is subject to change heavily in the future when **Ashita** v4 gains its full UI launcher.
{{% /notice %}}

## Beta Installation

Currently, **Ashita** v4 is in open beta testing. Due to this, we do not have a full GUI launcher available yet which would normally handle automatically updating and installing missing files. During this time, you will need to manually download and update your **Ashita** v4 installation.

We currently host the latest beta releases and updates on GitHub here: https://github.com/AshitaXI/Ashita-v4beta

### Downloading

You can download a full snapshot of the current beta release here: https://github.com/AshitaXI/Ashita-v4beta/archive/refs/heads/main.zip

### Installing

{{% notice warning %}}
We **DO NOT** recommend installing **Ashita**, or any third-party tool, inside of any system folders.\
You should not install third-party tools into `Program Files` or `Program Files (x86)`!
{{% /notice %}}

Once downloaded, extract the zip contents to a new folder, we recommend `C:\Ashita\` to avoid issues with protected/system folders.

## Configurations

**Ashita** stores its boot configurations / profiles within its `/config/boot/` folder. Each character you wish to play on can have its own profile, or you can use a single general profile for all characters. You will find example configuration files in this folder.

  - `example-privateserver.ini` - Demonstrates configurations needed in order to launch **Ashita** for private servers.
  - `example-retail.ini` - Demonstrates configurations needed in order to launch **Ashita** for retail servers.
  - `example.ini` - General example configuration with no specific purpose enabled. _(Will not launch as-is.)_

These configuration files are heavily commented to help users understand how to change things manually.

{{% notice note %}}
Once a full launcher is released, it will include a full configuration editor so you will not need to manually edit these files!
{{% /notice %}}

## Launching

Currently, the beta version of **Ashita** is launched through its included command line injector (`ashita-cli.exe`). You can either create a shortcut to this program or manually run it from the command line. _(**Note:** You will need to run this application as Administrator!)_

The program takes a single argument which is the name of the configuration file you are trying to boot. It is the name of the file found within the `/config/boot/` folder.

For example, if you wanted to boot the `example-privateserver.ini` file, then you would run the program as: `ashita-cli.exe example-privateserver.ini`

Or, if you are creating a shortcut, simply edit the shortcut and change the `Target` path to include the configuration file at the end.

For example, your target path would look something like this: `C:\Ashita\Ashita-cli.exe example-privateserver.ini`
