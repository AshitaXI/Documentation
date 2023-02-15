---
title: "[Beta] Install via Git"
weight: 2
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

{{% notice info %}}
Installing and updating the **Ashita** v4 beta using Git is considered more advanced. If you are not familiar with or comfortable with using Git, you can instead install (or update) using the latest repository snapshot.\
See [Install via Zip](/installation/install_zip/) for more information.
{{% /notice %}}

Currently, the recommended method of installing the **Ashita** v4 beta is by using a Git client. At this time, the latest beta release is maintained in a single GitHub repository which makes it easy to find the main project files and first-party addons/plugins in one place. By using a Git client, you can easily keep your installation up to date as well by pulling the latest changes. You can either use Git via the command line or install your personal favorite Git client or shell integration. _There is no 'best' client or means of using Git, that is entirely personal choice on which you prefer to use._

_**Please note:** When using a Git client to install and update, it is wise to not make use of any of the default included configuration files to avoid overwriting them when updating!_

Some recommended free solutions are:

  - Git For Windows _(Direct Git command line access.)_ - [https://git-scm.com/download/win](https://git-scm.com/download/win)
  - TortoiseGit _(Windows shell integration.)_ - [https://tortoisegit.org/](https://tortoisegit.org/)
  - GitHub Desktop _(Git GUI client.)_ - [https://desktop.github.com/](https://desktop.github.com/)
  - Sourcetree _(Git GUI client.)_ - [https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/)

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

## Cloning The Beta Repository

Please note, because there are many different Git clients available, it is not possible for us to write a full guide for each one. Instead, this guide will demonstrate how to install using three different methods. Two UI based clients and the command line.

{{% notice warning %}}
If you install `Git for Windows`, it is important to choose `Checkout as-is, commit as-is` when installing for the `line endings` configurations. This will avoid issues when any future usage of Git on your system with **Ashita** and other projects. The other configuration options while installing can all be left default unless you wish to change them.
{{% /notice %}}

### Installing via `GitHub Desktop`

1. First, download and install the `GitHub Desktop` client. Once installed, launch it and either sign in with your existing GitHub account, or skip the sign in step. _(**Note**: You do not need to sign in to clone the **Ashita** beta repository, so you can skip the sign in step if you do not want to or do not wish to create an account with GitHub.)_
2. From the top menu, click `File` then `Clone Repository...`
3. In the clone window, click the `URL` tab at the top, then enter the repository URL: `https://github.com/AshitaXI/Ashita-v4beta.git` For the local path, ensure you follow the guidelines above and place **Ashita** into a valid path. For example, `C:\Ashita\`
4. Click `Clone`.

If everything was successful, you're done and should have **Ashita** now installed to the selected folder!

### Installing via `TortoiseGit`

1. First, download and install `Git for Windows` and `TortoiseGit`. Follow the various prompts to fully install both tools.
2. Restart your computer. _(This is recommended as `TortoiseGit` is a shell extension.)_
3. Navigate to the parent folder where you plan to install **Ashita** to. For example: `C:\`
4. Right-click within the parent folder and choose `Git Clone..` _(Be sure you are not right-clicking on a folder!)_
5. In the clone window, enter the repository URL: `https://github.com/AshitaXI/Ashita-v4beta.git` For the `Directory` ensure the path is correct. _In this example, it should be `C:\Ashita-v4beta` by default, but you can edit this to be `C:\Ashita` instead._
6. Click `OK` to clone.

If everything was successful, a second window should show with some information about the clone and that it was successful. If so, then you're done and should have **Ashita** now installed to the selected folder!

### Installing via `Git Command Line`

1. First, download and install `Git for Windows`. Follow the various prompts to fully install.
2. Open a new command prompt window. _(cmd, powershell, Windows terminal, bash, etc. are all suitable for this.)_
3. Navigate the command prompt to the parent folder you wish to install **Ashita** to. For example: `cd C:\`
4. Enter the following command: `git clone https://github.com/AshitaXI/Ashita-v4beta.git Ashita`

If everything was successful, you're done and should have **Ashita** now installed to the selected folder!

## Updating Your Installation

One of the advantages of using a Git client to install the **Ashita** v4 beta is that you can easilly pull updates with little effort. In order to do this, you should avoid altering/editing any included file with the beta installation otherwise you may cause merge conflicts when pulling the latest update.

Things to avoid editing and using are:

  - The included boot configurations. _(Make a copy and rename it to something else.)_
  - The included default script. _(Make a copy and rename it to something else, and point your boot configuration to use the copy instead.)_
  - Any included configuration files.
  - Any included addons source code. _(If you find any bugs report them to be fixed in the main repo. If you need to make edits to an addon, you should make a copy and rename it to something else!)_

Assuming you have not made any edits to files that will cause conflicts, you can update using the below methods based on how you installed or use which ever client you prefer.

### Updating via `GitHub Desktop`

1. Open `GitHub Desktop`.
2. On the top-left, click the `Current Repository` block and make sure your **Ashita** v4 beta repo is selected.
3. Click `Repository` from the menu and choose `Pull`. _(Or click the `Fetch origin` button.)_
4. Wait for the pull to complete.

Your installation should now be up to date if there were no conflicts.

### Updating via `TortoiseGit`

1. Open the folder where you installed **Ashita** to.
2. Right-click the folder and choose `Git Sync...` from the menu.
3. Click the `Pull` button.
4. Wait for the pull to complete.

Your installation should now be up to date if there were no conflicts.

### Updating via `Git Command Line`

1. Open a new command prompt window. _(cmd, powershell, Windows terminal, bash, etc. are all suitable for this.)_
2. Navigate the command prompt to the folder you installed **Ashita** to. For example: `cd C:\Ashita\`
3. Enter the following command: `git pull`
4. Wait for the pull to complete.

Your installation should now be up to date if there were no conflicts.
