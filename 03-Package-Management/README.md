---

# Package Management

## Introduction
Package management is what makes Termux truly powerful. When you first open Termux, you have a working terminal with a few built-in commands, but you cannot yet write Python scripts, compile C programs, or connect to remote servers. All those extra tools, and thousands more, are available as packages that you can install with a single command. Package management is the system that lets you find, install, update, and remove software without ever visiting a website or touching a download button. It is one of the most important skills you can learn because everything you do later, writing scripts, editing text, managing projects, connecting to networks, depends on having the right software installed. Understanding package management also gives you control. You will know what is on your system, why it is there, and how to keep it healthy.

## What You Will Learn
- What a package is and how remote repositories work
- The difference between the dpkg, apt, and pkg tools
- How to update package lists and upgrade your system
- How to install, remove, search, and view detailed package information
- How to clean up local caches and automatically remove unused dependencies
- How to fix broken packages and reinstall corrupted files
- How to understand repository configurations and find specific commands
- How to handle configuration file prompts during upgrades
- Useful tips, aliases, and shortcuts to speed up package management

## Main Content

### Understanding Packages and Repositories
Before you start typing package commands, it helps to know what a package is and where it comes from. A package is simply a compressed archive containing a program, its configuration files, and instructions on how to set it up. Each package also lists its dependencies, other packages that must be installed for it to work. For example, if you install a music player, it might need a library to decode audio files. The package manager handles dependencies automatically so you do not have to hunt them down. In Termux, packages come from remote repositories, just like an app store. These repositories are web servers full of package files maintained by the Termux project. When you request a package, Termux downloads it from the repository, unpacks it, configures it, and places the program in the correct directories. All of this is done with careful checks to ensure nothing breaks.

### The Package Managers: dpkg, apt, and pkg
The underlying system Termux uses is based on Debian's package tools, specifically dpkg and apt. dpkg is the low-level tool that actually installs and removes individual package files. apt is the higher-level tool that fetches packages from repositories, handles dependencies, and manages upgrades. Termux provides a simplified front-end command called pkg that wraps apt and adds some convenient shortcuts. For most daily tasks, you will use pkg. However, it is good to know that apt is there under the hood, and sometimes you may need to use it directly for advanced troubleshooting. Throughout this guide we will use pkg primarily, but we will also look at what happens behind the scenes.

### Updating and Upgrading
The very first package management operation you should perform after a fresh Termux install is updating the package lists. This does not install or change any software yet. It simply downloads the latest list of available packages from the repositories. Because the Termux project actively maintains and updates software, new versions appear frequently. Without updating the lists, your local system does not know about the latest versions. You should run a package update regularly, at least every time before you install new software.

Once the package lists are up to date, the next step is to upgrade the packages you already have installed. This brings your entire system to the latest available versions. Upgrading is safe and recommended. It fixes bugs and adds features. However, if you are on a limited mobile data connection, be aware that upgrades can sometimes be large. Always upgrade on WiFi if possible. After the upgrade completes, your Termux environment is current.

### Installing and Removing Packages
The most exciting operation is installing new packages. The package manager figures out the best order and takes care of everything automatically, including dependencies. Removing a package is equally simple. To free up space or clean up software you no longer need, you can remove it. Removing a package also removes any configuration files that came with it, but it does not automatically remove dependencies that were installed with it, because those might be needed by other packages. To remove unused dependencies, there is a separate cleanup command we will cover shortly.

### Searching and Viewing Package Info
Before you install something, you often want to know if it exists and what it does. The search command finds packages by name or keyword. Another useful informational command is showing package details. This displays detailed information about a specific package, including version, size, dependencies, and a longer description. This helps you understand what you are adding to your system. To see every package currently installed on your Termux, you can list them. Similarly, you can see all packages available in the repositories, whether installed or not. Be careful, the output of all available packages is enormous. It is usually better to pipe it into a pager or use search for a narrower view.

### Cleaning Up Storage
Now let us talk about cleaning up. Over time, as you install and upgrade packages, downloaded package files are cached locally. This cache can grow to use significant storage space. To clear the cache and reclaim that space, you run a clean command. It is safe and recommended if storage is tight. Another cleanup operation is removing packages that were automatically installed as dependencies but are no longer needed by any manual installs. This helps keep your Termux lean. It is a good habit to run an autoremove after uninstalling something you no longer need.

### Fixing and Reinstalling Broken Packages
Occasionally, a package may become broken, for example if an upgrade was interrupted or a file got corrupted. To fix broken dependencies, you can use an install command with a fix flag. If you ever see error messages about unmet dependencies, this command is your first aid. Another subcommand you might need is reinstalling. If a package's files are accidentally deleted or corrupted, reinstalling it restores the original files. This does not change your personal configuration files, but it resets the program's system files to their default state. It can resolve strange behavior. You can also see exactly which files a package installed. This is useful if you wonder where a program's files ended up.

### Differences Between pkg and apt
Now we must talk about the difference between pkg and apt. In Termux, pkg is actually a shell script that calls apt with various options to make it simpler and safer. For example, installing via pkg runs the apt install command but with Termux-specific tweaks, like checking for storage space and setting up the right terminal colors. Experienced users sometimes use apt directly for operations like listing, checking policy, or running a distribution upgrade. The most common apt command you might use is searching, which works similarly to pkg search. However, for most tasks, pkg is the recommended tool because it is specifically tailored for Termux. If you look at online tutorials and see apt-get commands, you can usually substitute pkg in Termux. For example, updating with apt-get becomes a pkg update, and installing with apt-get becomes a pkg install. Under the hood, pkg update runs the apt-get update command, and pkg upgrade runs the apt-get dist-upgrade command, which is smarter about dependency changes than a plain upgrade.

### Understanding Repositories
The repositories themselves are worth understanding. A repository is configured by a file that tells the package manager where to find packages. In Termux, the main repository is set up automatically, and it is the only one you need. The configuration is in `/data/data/com.termux/files/usr/etc/apt/sources.list` and sometimes files in `sources.list.d`. You do not need to edit these unless you are an advanced user who needs to add a testing or community repository. For everyday use, the default repositories give you thousands of stable packages. Adding random third-party repositories can break your system, so stick to the official ones unless you have a specific, well-understood need.

### Finding the Right Package
A very common beginner's question is which package to install to get a specific command. For instance, you know you want to use the ssh command, but you are not sure which package provides it. You can search for the command and look for a package that sounds right. Often the package name matches the command name, like the package openssh provides the ssh command. But sometimes they differ. For example, the command dig is in the package dnsutils. In that case, searching by description helps. You can also use advanced tools like apt-file if you install them. For now, just searching and using online documentation or the Termux wiki will guide you.

### Conclusion
Now, to wrap up with a complete overview, package management in Termux is not just a single tool but a philosophy. You maintain your environment actively. You use updates and upgrades to keep the ground healthy. You use installations to bring in new capabilities. You search, show, list, remove, and clean to stay organized. You understand that every new package integrates neatly into your system without hunting for downloads or installers. This is the command-line way, and it is far more efficient than any graphical app store once you know it. Take the time now, while your Termux is fresh, to practice. Install a few small tools, search for something obscure, check the details, remove them, and clean up. Notice how quickly and silently everything happens. This confidence will fuel your excitement for all the advanced topics to come. You are no longer just a user of pre-installed software; you are building your own set of tools, piece by piece, with understanding and control.

## Examples

```
pkg update
```
When you run this, you see a series of lines showing which repository sources are being fetched. The process uses your internet connection and typically finishes in a few seconds.

```
pkg upgrade
```
After pressing Enter, apt calculates which packages need to be downloaded, how much space they require, and whether any new dependencies are needed. You then see a summary and a prompt asking for confirmation. Type Y and press Enter to proceed, or N to cancel.

```
pkg install package-name
```
Replace package-name with the actual name of the software.

```
pkg install python
```
Termux will show you what it will do. It lists the main package plus any dependencies, how much space they need, and asks for confirmation. Type Y and press Enter. You will see download progress bars, then installation messages. Once the prompt returns, the software is ready. You can then run the Python program and the interactive Python interpreter starts.

```
pkg install git vim curl
```
To install multiple packages at once, list them separated by spaces. This one line installs Git, the Vim text editor, and the curl network tool.

```
pkg remove package-name
```
Use this to free up space or clean up software you no longer need.

```
pkg remove vim
```
For example, this will uninstall Vim. You will be asked for confirmation.

```
pkg search pdf
```
This will list all packages whose name or description contains "pdf". The output shows the package name, a brief description, and sometimes the version. You can then decide which one you need.

```
pkg show python
```
You see the exact version number, the home page, the download size, and the list of packages that Python requires to run.

```
pkg list-installed
```
This prints a long list with the package name, version, and sometimes the architecture.

```
pkg list-installed > installed-packages.txt
```
To save this list for later reference, you can redirect it to a file.

```
pkg list-all
```
To see all packages available in the repositories, whether installed or not.

```
pkg clean
```
This removes the downloaded archive files, not the installed programs.

```
pkg autoremove
```
When you run it, pkg scans the dependency tree and removes orphaned packages. It also asks for confirmation.

```
pkg install -f
```
The -f flag tells pkg to fix broken packages, attempting to download missing dependencies and configure partially installed packages.

```
pkg reinstall package-name
```
If a package's files are accidentally deleted or corrupted, reinstalling it restores the original files. Use it like this.

```
pkg files package-name
```
This lists every file and directory that belongs to the package. For example, running this on nano shows where the nano binary is located, its documentation, and configuration templates.

### Real Examples Step-by-Step

Imagine you want to turn your Termux into a Python development environment. You first make sure everything is up to date:
```
pkg update && pkg upgrade
```
The double ampersand runs the second command only if the first succeeds. Next, you install Python and a text editor:
```
pkg install python nano
```
You confirm the installation. Now you want to install Git to manage your code:
```
pkg install git
```
After this, you decide you prefer Vim over Nano, so you install Vim:
```
pkg install vim
```
Then you remove Nano:
```
pkg remove nano
```
At this point, some dependencies that were only needed by Nano might be lingering. You clean them up:
```
pkg autoremove
```
Finally, you check that everything is correct by listing installed Python-related packages:
```
pkg list-installed | grep python
```
The pipe and grep filter the list to show only packages with "python" in their name. You see that Python and its essential libraries are there.

Another example: you want to try a new tool that you heard about, but you are not sure of its exact name. You run:
```
pkg search image editor
```
The results show a few options, including imagemagick. You look at the details:
```
pkg show imagemagick
```
You see it is a powerful image manipulation toolset. You install it:
```
pkg install imagemagick
```
Now you have commands like convert and identify available. Later, you realize you do not need it and want the space back. You remove it:
```
pkg remove imagemagick
```
```
pkg autoremove
```
This cycle is fast and keeps your environment exactly as you need it.

## Common Mistakes
- Trying to install a package before updating the lists. You might get an error that a package could not be found because your package list is outdated. The error message might say "E: Unable to locate package." The fix is simple: run:
```
pkg update
```
and then try again. This happens often enough to make it a rule: always run it before installing anything new.

- Running out of disk space during installation. Termux uses your internal phone storage, and packages can be large, especially big toolchains like clang or development libraries. If you run out of space, the installation will fail and might leave the package in a half-installed state. Before installing large packages, check your free space with:
```
df -h /data
```
If it is low, you can run a clean command to free up cache, then an autoremove to remove unused packages, or delete unwanted files from your home directory. If an installation fails due to space, fix the space issue first, then run:
```
pkg install -f
```
to repair the broken package.

- Accidentally mixing packages from the Termux main repository with packages from the Play Store version's old repository. If you originally installed Termux from the Play Store and later switched to the F-Droid version without a clean reinstall, you may have conflicting sources. The Play Store version used different URLs and is no longer maintained. The solution is to back up your files, clear data, and install the F-Droid version fresh. If everything is working, you can ignore this, but if you get strange upgrade errors about unmet dependencies or hash sum mismatches, check your sources with:
```
cat $PREFIX/etc/apt/sources.list
```
It should point to packages.termux.dev or similar Termux-maintained domains, not bintray.com or something old. If it is wrong, you can edit the file, but reinstalling is often simpler.

- Ignoring prompts that ask about configuration file changes. When you upgrade, sometimes packages have new default configuration files that differ from the old ones. The package manager will stop and ask you what to do: keep the old version, use the new one, show a difference, or open a shell. The message looks intimidating. In Termux, as a beginner, it is usually safe to choose "N" or "O" to keep your currently installed version, especially for your own customizations. If you have not edited the file, you can probably accept the new one. If you are unsure, you can quit the upgrade and research the package. Do not blindly mash Y and Enter, because you might overwrite something you need.

- Encountering a broken shell or missing commands after a badly interrupted upgrade. If your package command itself stops working, you have a serious issue. Before panicking, try restarting Termux completely, or open a new session. If the shell does not start, you can try launching a failsafe session from the notification widget or using the:
```
termux-fix-shebang
```
command if available. In extreme cases, you can reinstall Termux and restore data. To avoid this, never kill the Termux app while a package operation is running. Wait for it to finish, even if it seems stuck. If it truly hangs, give it a few minutes, because it might be downloading a large file on a slow connection.

- Confusing the difference between an upgrade and an update. An update only gets new package lists. An upgrade actually updates the installed packages. If you only run an update and then try to install something, you may still have old versions, but that is fine. The install will get the latest version listed. But failing to upgrade regularly can lead to dependency problems when a package you want to install expects newer versions of libraries. It is safe to run both as a single routine.

## Quick Tips
- You can combine update and upgrade in one line with a logical operator:
```
pkg update && pkg upgrade
```
The double ampersand ensures upgrade only runs if update succeeds.

- You can create an alias for it. Add this line to your `.bashrc` file:
```
alias upd='pkg update && pkg upgrade'
```
After restarting your shell or sourcing `.bashrc`, typing `upd` performs both steps. This is a huge time saver.

- If you are scripting or want to avoid manual confirmation, you can use the `-y` flag:
```
pkg install -y package-name
```
This assumes yes to all prompts. Use this with caution because you will not see the list of packages or be given a chance to cancel. It is safe for automation, but when learning, it is better to see the prompts so you understand what is happening.

- To speed up downloads, Termux uses multiple mirrors. You can sometimes switch the mirror if one is slow. The command opens a dialog that lets you select a different set of repositories:
```
termux-change-repo
```
This is useful if your default mirror is slow or blocked in your region. Simply run it, choose a mirror group, and the sources are updated.

- If you need to know which package provides a particular file or command, you can install the command-not-found handler. In Termux, the package `command-not-found` is not pre-installed, but you can install the `apt-file` package. After installing it and updating its cache with an `apt-file update`, you can type:
```
apt-file search bin/command
```
For example, searching for `bin/convert` will show that the convert command is from imagemagick. This is an advanced technique, but keep it in mind for the future.

- You can keep a text file list of your favorite packages. Then, after a fresh Termux install, you can reinstall everything at once. Save your list with:
```
pkg list-installed | awk '{print $1}' | cut -d/ -f1 > my-packages.txt
```
Then on a new system, install them with:
```
xargs pkg install -y < my-packages.txt
```
This works, but be mindful that the new system might have different default packages. A simpler way is to manually list essential packages like git, python, nodejs, etc., and run a single install command.

- Pay attention to the architecture. Termux runs on several CPU types: arm, aarch64, i686, x86_64. When you run:
```
termux-info
```
you can see your architecture. The package manager automatically selects the correct package for your device. You never need to specify it. However, if you are copying commands from a website and see a package name like `zsh:arm`, ignore the colon part. Just use the base name.

- Do not be afraid to experiment. If you install a package and do not like it, you can remove it cleanly. This encourages exploration. The worst that can happen is you waste a bit of storage and bandwidth. There is no permanent damage as long as you do not delete critical system packages.

- Critical system packages include the bare minimum like bash, coreutils, termux-tools, and the C library. The package manager itself will warn you if you try to remove an essential package. It will say something like "You are about to do something potentially harmful." If you see that, cancel unless you know exactly what you are doing. Removing core packages can break your Termux installation, requiring a reinstall.

- If you need to see the full list of repositories being used, run:
```
pkg list-repositories
```
or look at the sources list files. This is mainly for debugging.

- Understand that Termux uses a rolling release model. There are no big version numbers like Ubuntu 20.04 versus 22.04. Instead, packages are continuously updated. This means that upgrades can change versions often. It is a good habit to upgrade at least once a week so that you do not fall too far behind, which can make dependency resolution harder.

---
