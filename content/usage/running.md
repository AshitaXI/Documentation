---
title: "[Beta] Running Ashita"
weight: 2
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

{{% notice note %}}
We currently do not have a graphical user interface made for launching **Ashita** v4 during the beta. This documentation covers using the `ashita-cli.exe` launcher until a full UI launcher is ready.
{{% /notice %}}

Before you attempt to launch/run **Ashita** v4, please be sure to create a new boot configuration file with your desired configurations. You can find more information in regards to configurations here: [Configurations](/usage/configurations/)

Once you have setup a new boot configuration file, you are ready to launch **Ashita**.

## Launching via Shortcut

If you are not familiar with using a command line, then it is recommended that you follow these directions to create a shortcut to launch **Ashita** with.

1. Open the folder you have installed **Ashita** to. _(ie. `C:\Ashita\`)_
2. Locate the `ashita-cli.exe` file.
3. Right-click the `ashita-cli.exe` file and choose: `Create Shortcut`
4. Right-click the newly created shortcut and choose: `Rename` _(Rename the shortcut to what you would prefer it to be called. Such as the name of the character you plan to play.)_
5. Right-click the newly created shortcut and choose: `Properties`

Once you have opened the properties of the shortcut, you need to edit the shortcut `Target` field. In this field, you will see the full path to `ashita-cli.exe`, such as: `C:\Ashita\ashita-cli.exe`

At the end of this path you need to add the name of the boot configuration file that you created.\
_You **DO NOT** include the path to this file, just the file name itself!_

![running1](/usage/images/running1.png?width=250px)
{.slim-img}

In this above example I have the following:

  - **Ashita** is located at: `C:\Ashita\`
  - **ashita-cli.exe** is located at: `C:\Ashita\ashita-cli.exe`
  - **atom0s.ini** is the new boot configuration file located at:`C:\Ashita\config\boot\atom0s.ini`

Then I would update the target to look like this: `C:\Ashita\ashita-cli.exe atom0s.ini`

{{% notice note %}}
If you install Ashita to a different location than recommended, and that location has spaces in the path, then be sure to surround the path with quotes when editing the **Target** property! Failure to add quotes may result in your shortcut not working properly.\
\
For example: `"C:\Users\atom0s\Desktop\Ashita v4\ashita-cli.exe" atom0s.ini`
{{% /notice %}}

## Launching via Command Line

Users familiar with a command line can easily and directly launch **Ashita** v4.\
Simply pass the name of the boot configuration file you wish to run to `ashita-cli.exe`.

For example: `ashita-cli.exe atom0s.ini`

![running2](/usage/images/running2.png)
{.slim-img}