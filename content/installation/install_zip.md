---
title: "[Beta] Install via Zip"
weight: 3
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

{{% notice info %}}
It is recommended that you use Git to install the **Ashita** v4 beta for easy updating. See [Install via Git](/installation/install_git/) if you are comfortable doing so.
{{% /notice %}}

## Picking An Installation Folder

When picking a folder to install **Ashita** to, it is important that you **DO NOT** break the following guidelines:

{{% notice warning %}}
**Ashita** should **NOT** be installed into a system protected folder.\
\
This means it should not be put into folders (or folders within) such as:\
`C:\Program Files (x86)\`, `C:\Program Files\`, `C:\Windows\`
{{% /notice %}}

{{% notice warning %}}
**Ashita** should **NOT** be installed into the game client folder!\
\
You should never install **Ashita** into the game client folder for safety reasons.\
It should be in its own separate folder entirely!
{{% /notice %}}

A recommended and safe installation location would be something such as:

  - `C:\Ashita\`
  - `C:\Users\Your_Username_Here\Desktop\Ashita\`
  - `Z:\Some\Other\Folder\Ashita\`

## Downloading The Beta Repository Snapshot

You can download the latest beta repository snapshot for **Ashita** v4 here: https://github.com/AshitaXI/Ashita-v4beta/archive/refs/heads/main.zip

## Installing The Beta Repository Snapshot

To 'install' the beta package you just downloaded, you can simply extract its contents to your desired installation folder.\
We recommend `C:\Ashita\`.

If extracted properly, you should see a similar file layout as the following:

![install_zip_folder.png](/installation/images/install_zip_folder.png)
{.slim-img}

## Updating The Beta Repository Snapshot

Before doing this, it is important that you make sure you have backups of any changes you have made to any files that will be overwritten! Ideally, you should not be using any files included in the beta packages directly.

Things to avoid editing and using are:

  - The included boot configurations. _(Make a copy and rename it to something else.)_
  - The included default script. _(Make a copy and rename it to something else, and point your boot configuration to use the copy instead.)_
  - Any included configuration files.
  - Any included addons source code. _(If you find any bugs report them to be fixed in the main repo. If you need to make edits to an addon, you should make a copy and rename it to something else!)_

Once you have made sure to make backups of any changes or ensured all your modifications are in custom files that will not be overwritten, you can continue to the next steps.

1. Redownload the latest snapshot of the beta repository here: https://github.com/AshitaXI/Ashita-v4beta/archive/refs/heads/main.zip
2. Extract the contents of the latest snapshot over your current installation.
3. You should be prompted to overwrite existing files, choose 'Yes' for all files.
4. Reapply any modifications you had to backup and ensure all your changes and configurations are set/valid.

At this point you should be updated.
