# Getting Started with Termux

## Introduction

You have opened Termux for the first time and you are looking at a screen with a blinking cursor, a dollar sign, and probably a dark background. This little application is a complete Linux terminal environment running directly on your Android phone or tablet. It does not need root access. It does not modify your device in any dangerous way. It simply provides a sandbox where you can run command line programs, write scripts, install tools, and learn how a Unix-like system works from the palm of your hand.

This first guide will take you from the very beginning, from installation to running your first commands, and will make sure you understand everything that is happening and why.

## What You Will Learn

- What Termux is and how it works as a Linux environment on Android
- How to install Termux correctly and from the right source
- How to update packages and set up storage access after first launch
- How to navigate the terminal using essential commands
- How to use the Termux interface, keyboard shortcuts, and extra keys row
- How to understand absolute and relative paths
- How to create and delete files and directories safely
- How to get help and stop running commands
- How to use command history and tab completion
- How to download files from the internet inside Termux

## Main Content

### What Termux Actually Is

Termux is a terminal emulator and a Linux environment for Android. A terminal emulator is a program that gives you a text-based interface, just like the command prompt on Windows or the Terminal app on a Mac or the console on a Linux desktop. Inside this terminal, you type text commands that tell the system what to do.

Termux is special because it bundles a minimal Linux user space, meaning it includes many of the standard programs you would find on a Linux computer — things like a shell, a package manager, and various command line utilities. The shell is the program that reads your input and runs the commands. In Termux, the default shell is called bash, although zsh and fish are also available if you want them later.

### Why Use Termux

Termux turns your Android device into a portable programming and learning environment. You can use it to manage files efficiently, write Python scripts, connect to remote servers over SSH, keep track of your projects with Git, and even run small web servers for testing. It is a fantastic way to learn the command line without needing a separate computer. Everything stays on your phone, and you can pick it up and practice whenever you have a few minutes. Because Termux is a real Linux environment, the skills you gain here will transfer directly to a desktop Linux system or to a Mac terminal.

### Installing Termux Correctly

The recommended source is F-Droid, which is an open source app store for Android. You can download the F-Droid app from f-droid.org and then search for Termux inside it. The F-Droid version is actively maintained and has all the latest features.

If you installed it from the Google Play Store, you may encounter a warning that the app was built for an older Android version, and some things might not work. It is fine to start with the Play Store version to test the waters, but if you plan to use Termux seriously, get it from F-Droid or directly from the GitHub releases page.

The installation process is the same as any Android app. You download it, you open it, and you grant it the permissions it asks for. The first time you launch Termux, you see a message about the package manager being set up, and after a few seconds you are presented with a prompt.

### Understanding the Prompt

The blinking block or line is the cursor. It shows where the next letter you type will appear. The prompt usually shows a short piece of information, like the username, hostname, and the current working directory. In Termux, the username is usually `u0_a` followed by some numbers, and the hostname is `localhost`.

The directory part starts with a tilde symbol when you are in your home directory. The tilde is a shortcut that represents `/data/data/com.termux/files/home`, which is your personal home directory inside Termux. You do not need to type that long path. Just know that tilde means home.

### First-Time Setup Steps

#### Updating Package Lists and Upgrading Packages

The first thing you should always do is update the package lists and upgrade any installed packages. In Termux, packages are pieces of software that you can install, remove, and update. The package manager is called `pkg`, and it is a tool that handles all of that for you.

Running `pkg update` fetches the latest information about available packages from the official Termux repository over the internet. This command only updates the package information database; it does not actually change any software on your system.

Running `pkg upgrade` downloads and installs newer versions of any packages already on your system. You may see a prompt asking if you want to continue. Press Y and then Enter to confirm. It is important to run these two commands right after installation to make sure everything is up to date and to avoid problems later.

#### Granting Storage Access

By default, Termux has its own private directory that other apps cannot see. If you want to work with files from your device, or save files that other apps can access, you need to run a command that sets up a special folder.

When you run `termux-setup-storage`, Android will show a permission dialog asking you to allow Termux to access photos, media, and files. You must tap Allow. Once you do, Termux creates a directory called `storage` inside your home folder. Inside that storage directory you will find links to things like your Downloads folder, your DCIM folder for photos, your Music folder, and so on. This is a crucial step for any project that involves files you want to share or view in other apps.

### Navigating the File System

A path is a string that tells the system where a file or directory is located. Absolute paths start from the root directory, which is represented by a forward slash. So `/data/data/com.termux/files/home` is an absolute path. A relative path starts from your current directory.

The dot symbol represents the current directory, and dot dot represents the parent directory. So if you are in `storage/downloads`, typing `cd ..` moves you up to `storage`, and `cd ../..` moves you up two levels to your home. Understanding paths is essential because almost every command that works with files uses them.

### The Termux Interface and Keyboard

Long press anywhere on the terminal to access a context menu. From there you can paste text from the clipboard, select text to copy, or access Termux settings. In the settings, you can change the terminal's font size, color scheme, and font type.

The extra keys row is a bar above the on-screen keyboard that provides commonly used keys like ESC, TAB, CTRL, ALT, and the arrow keys. This extra keys row is extremely helpful if you do not have a physical keyboard. If you do not see the extra keys row, go to the Termux settings by long pressing anywhere and selecting "More" then "Settings". Under the "Terminal" section, you can toggle the extra keys.

The volume down button acts as Ctrl in Termux. So to send Ctrl+C, hold the volume down button and press C on the on-screen keyboard. The volume up key combined with a letter also sends the Ctrl combination for that letter.

### Session Management

Swiping from the left edge of the screen opens a drawer with your active sessions. You can have multiple terminal sessions running at the same time. Tap the plus button to start a new session. Sessions keep running in the background even if you switch away, so be careful not to leave processes running that you do not need.

### The File System Hierarchy

Termux stores all its data under a private directory: `/data/data/com.termux/files`. Inside it, `home` is your personal folder. The `usr` directory inside `files` contains the equivalent of `/usr` on a traditional Linux system, with `bin`, `lib`, `share`, and so on. Do not delete or modify things outside your home directory unless you know exactly what you are doing. Your playground is your home directory and the storage directory.

### Case Sensitivity

In Linux and Termux, file names and commands are case-sensitive. `myfile.txt`, `MyFile.txt`, and `MYFILE.TXT` are three different files. Commands like `ls` and `Ls` are not the same; only lowercase `ls` works. Pay close attention to capitalization.

## Examples

### Updating packages

```
pkg update
```

Fetches the latest package information from the Termux repository. Run this first, right after installation.

```
pkg upgrade
```

Installs newer versions of any packages already on your system. Press Y when prompted to confirm.

### Setting up storage access

```
termux-setup-storage
```

Grants Termux access to your device's shared storage. Tap Allow when Android asks for permission. Creates a `storage` folder in your home directory with links to Downloads, DCIM, Music, and more.

### Checking your current directory

```
pwd
```

Stands for print working directory. Outputs the full path of the directory you are currently in. You should see something like `/data/data/com.termux/files/home`.

### Listing files

```
ls
```

Lists the contents of the current directory.

```
ls storage/downloads
```

Lists the files in your device's Downloads folder by providing a path to `ls`.

### Changing directories

```
cd storage
```

Changes your current directory to the `storage` folder.

```
cd
```

With no arguments, returns you to your home directory.

```
cd ..
```

Moves up one level to the parent directory.

### Clearing the screen

```
clear
```

Clears all text from the terminal screen to make things tidy.

### Getting help for a command

```
ls --help
```

Prints a description of `ls`, all its options, and how to use them. The `--help` flag works with almost every command.

### Viewing system information

```
termux-info
```

Prints details about your Termux installation, including the Android version, CPU architecture, and the package repository being used.

### Installing common packages

```
pkg install coreutils
```

Provides a full set of essential file, text, and system utilities.

```
pkg install termux-tools
```

Provides the `termux-setup-storage` and `termux-info` commands, among others.

```
pkg install nano
```

Installs Nano, a simple beginner-friendly text editor that works entirely in the terminal.

### Listing and searching packages

```
pkg list-installed
```

Outputs a list of all currently installed packages.

```
pkg search keyword
```

Replace `keyword` with something like `python` or `git` to search for available packages.

### Creating a directory

```
mkdir testfolder
```

Creates a new directory called `testfolder` inside your current working directory. Verify it with `ls`.

### Removing an empty directory

```
rmdir testfolder
```

Removes an empty directory. Safe to experiment with because it only works on empty directories.

### Creating an empty file

```
touch myfile.txt
```

Creates a file with no content. You can then see it with `ls`.

### Removing a file

```
rm myfile.txt
```

**Be very careful with `rm`. There is no trash can. Once a file is removed this way, it is gone forever.**

### Downloading a file from the internet

```
curl -O https://example.com/file.txt
```

The `-O` option saves the file with its remote name in your current directory. Termux uses your device's normal WiFi or mobile data connection.

## Common Mistakes

- Typing commands with a typo — the shell is very literal. If you type `l s` instead of `ls`, it will say command not found. There is no autocorrect.
- Running a command that is not installed yet — if you type `python` and get a not found error, you need to install it first using `pkg install python`.
- Accidentally locking up the terminal by running a command that waits for input and then not knowing how to stop it — use Ctrl+C to break out instead of closing and reopening the app.
- Confusing the Termux home directory with Android's internal storage — your Termux home is separate from your phone's internal storage. Use the `storage` folder created by `termux-setup-storage` to access device files.
- Pressing Ctrl+D at an empty prompt accidentally — this sends an end-of-file signal and closes the Termux session. Only press it when you intend to exit.
- Pasting commands from unfamiliar sources without checking them first — always read what you are pasting before running it.
- Ignoring capitalization — file names and commands in Termux are case-sensitive.

## Quick Tips

- Use `Ctrl+C` (or volume down + C on a touch keyboard) to interrupt and stop any running command.
- Use the up and down arrow keys on the extra keys row to recall previous commands from your history. This saves you from retyping long commands.
- Use `Ctrl+R` (or volume up + R) to open reverse history search. Start typing and the most recent matching command appears. Press Ctrl+R again to cycle through matches.
- Use Tab completion — start typing part of a directory or file name and press Tab to auto-complete. Press Tab twice to see all possible matches. This speeds up typing and prevents spelling errors.
- Use `cd` with no arguments to return to your home directory from anywhere.
- Use `clear` to tidy up a busy terminal screen.
- The `--help` flag works with almost every command and shows you what it does and how to use it.
- Change the font size and color scheme in the Termux settings to make the terminal more comfortable for your eyes.
- You can have multiple terminal sessions open at once. Swipe from the left edge to open the session drawer and tap the plus button to add a new one.
- Do not use `sudo` in Termux. Termux does not use sudo because you do not have root access. If a command from a guide starts with `sudo`, you can usually run the core part without it in Termux.
- Exit sessions cleanly by typing `exit` rather than just closing the app, to avoid leaving processes running in the background.
- Long press anywhere in the terminal to access copy, paste, and settings options.
