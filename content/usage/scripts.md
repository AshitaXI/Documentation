---
title: "Text Scripts"
weight: 4
disableToc: false
chapter: false
---

![ashita](/images/ashita.png?width=64px)
{.slim-img}

One of **Ashita**'s built-in features is the ability to execute text-based scripts which can contain additional commands to be executed within them. Scripts were originally created to vastly improve on the games extremely limited macro system _(PS2 limitations!)_ by allowing players to execute more than six command entries, having multiple waits, and doing more than just normal game related functions.

As the client has gained new features (ie. gear sets, more macro space via books, etc.) and as third-party tooling has vastly expanded with things such as AshitaCast, LuashitaCast and so on that automatically handle swapping gear, scripts have become less of a major feature.

However, with Ashita v4, we have greatly improved the script system to add new features making scripts much more powerful than before, allowing users to create more in-depth functionality without having to write an addon.

## Executing Scripts

Text scripts are executed using the `/exec` command. This command can either be manually entered into the games chat input, or it can be used from within a macro.

You can find more information on how to use this command here: [Executing Scripts](/usage/commands/#command-exec)

## (New!) Script Arguments

The first new feature we have added to **Ashita**'s script system is the ability to pass arguments to scripts. Prior to v4, scripts were entirely static. This meant that once a script was written, there was no way to alter how it executed without having to edit the actual script file. You could not dynamically do anything with a script previously.

Arguments are done through a tokenization system. The token format is: `%#%`\
_(Where `#` is the index number of the argument being passed.)_

### Commonly Asked Questions

Here are a few answers to commonly asked questions in regards to script arugments:

  - **Q. How many arguments can my script use?**
    - _As many as you want. Your only restriction is the character limit when typing into the games chat input or macro editor._
  - **Q. Can my script use the same argument multiple times?**
    - _Yes, just use the same token for the given arguments index._
  - **Q. Can arguments contain spaces?**
    - _Yes, just wrap your argument in quotes when executing your script._
  - **Q. Can arguments use other tokens such as `<me>`?**
    - _Yes! It is encouraged to use these as well to greatly improve what your scripts can do!_

### Script Example

Here is an example script that just echos the arguments you pass to it:

**echo.txt**

```text
/echo Argument 0 was: %0%
/echo Argument 1 was: %1%
/echo Argument 2 was: %2%
```

Here are some examples of what this scripts output will look like based on the arguments you use:

![script_args1](/usage/images/script_args1.png)
{.slim-img}

![script_args2](/usage/images/script_args2.png)
{.slim-img}

![script_args3](/usage/images/script_args3.png)
{.slim-img}

## (New!) Script Includes

The second new feature to **Ashita**'s script system is the ability to include other scripts into each other.

Previously, the only way to do something like this was to use `/exec` inside of a script to execute another. However, this came with the downside that you could not guarantee the order that the commands of both scripts would execute. _Script execution is threaded and using `/exec` inside of another script causes another thread to be used to execute the second scripts commands!_

Instead, you can now directly include the contents of other scripts into your script using the new `/include` command. The `/include` command is considered a pre-processor command, meaning that before the script is actually executed, it is parsed for additional functionality, _such as the `/include` command_, and the contents of the script are edited (in memory) on the fly. _(Your scripts are not edited on disk, this all happens in memory!)_

The following screenshot shows the difference between using `/exec` vs. the new `/include` command.

![script_args1](/usage/images/script_includes.png)
{.slim-img}
