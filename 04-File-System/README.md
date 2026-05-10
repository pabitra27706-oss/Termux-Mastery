---

# The File System

## Introduction
The file system is the structure that holds all your data. Every file, every directory, every program, every configuration setting lives somewhere in the file system. In Termux, you have your own private file system that behaves exactly like a Linux file system, even though it sits inside Android. Understanding how this structure works, how to navigate it, and how to manage files and directories is one of the most essential skills you will ever learn. Without it, you cannot save your work, organize projects, or even find the scripts you wrote. With it, you have complete control over your digital environment.

## What You Will Learn
- What a file system is and how it functions as a tree structure
- How to understand absolute paths, relative paths, and home directories
- How to navigate the terminal using commands like pwd and cd
- How to safely create, copy, move, rename, and delete files and directories
- How to use the storage directory to interact with Android shared folders
- How to manage hidden files, case sensitivity, and file extensions
- How to read and modify file permissions and ownership
- How to create and utilize symbolic and hard links
- How to check file sizes and available disk space
- How to locate files by name or determine their true type
- How to safely use wildcards to select multiple files

## Main Content

### Understanding the File System Structure
Before you run any commands, it helps to understand what a file system actually is. Think of it as a giant tree. At the very bottom, or the very top depending on how you picture it, is the root directory. The root directory is written as a single forward slash. Everything else branches out from there. Inside root, there are directories like data, system, and usr. Inside those, there are more directories and files. Each item has a name, and the full list of names from the root all the way down to the item is called a path. For example, your home directory path is `/data/data/com.termux/files/home`. That string starts at root, goes into data, then another data, then com.termux, then files, and finally home. That is an absolute path because it begins from the root.

### The Home Directory and Storage
You will mostly work inside your home directory, which has a special shortcut, the tilde symbol, a little wavy line. When you see tilde in a path or a prompt, it means `/data/data/com.termux/files/home`. Your home directory is yours to fill and organize. Termux keeps its system files outside your home, in directories like `/data/data/com.termux/files/usr`, which contains all the installed programs and libraries. You typically do not need to touch those system files, and doing so can break things, so it is best to stay inside your home or the special storage directory that links to your Android shared folders.

The storage directory appears after you run the storage setup command. It is a folder inside your home called storage, and inside it you find links to your Android downloads, pictures, music, and other shared folders. These are not real copies, they are doorways to the files that other apps can see. This is how you share files between Termux and your photo gallery or file manager. If you ever see a path like `/sdcard` or `/storage/emulated/0`, those are Android paths that are not directly accessible from Termux unless you go through the storage folder links. This separation protects you from accidentally modifying system files.

### File and Directory Organization
Now let us talk about how the file system is organized. Directories are often called folders. They can hold files and other directories. A file is a container for data, like a text note, a script, a picture, or a program. File names in Termux are case sensitive, meaning `MyFile.txt`, `myfile.txt`, and `MYFILE.TXT` are three completely different files. This is one of the most important differences from Windows and one of the most common causes of confusion for newcomers. Also, file extensions like `.txt` or `.jpg` are just part of the name and do not actually control what the file contains. They are only a convention to help you and some programs recognize the type. You can have a text file named `picture.png` if you want, but it would be confusing.

Files that start with a dot are hidden. They are often used for configuration and are sometimes called dotfiles. For example, `.bashrc` is a script that runs every time you start a new shell session. In a normal file listing, you will not see these files. Hidden files are not secret; they are just kept out of your everyday view to reduce clutter. Every directory also contains two special entries. A single dot means the current directory, and two dots means the parent directory, the one above the current one. They are always present, even in an empty directory.

### Moving Around and Inspecting
The commands you use to move around and inspect the file system start with checking your absolute path. It is your you-are-here marker. Then there are commands to list contents. By itself, listing shows the names of files and folders in the current directory in a simple column view. Adding flags gives a long listing with details, the permission string, the number of links, the owner, the group, the file size, the modification date and time, and the filename. You can combine flags to show all files including hidden ones, make sizes human readable, sort by modification time, or list subdirectories recursively. 

To change your location, you use change directory commands. You can go home, go back to the previous directory like a toggle, or go up one level. You can give an absolute path or a relative path. A relative path is one that does not start with a slash; it starts from your current directory. Using relative paths saves typing, and using tab completion saves even more.

### Creating, Moving, and Removing
Creating directories is done with a make directory command. You can create single directories, multiple directories at once, or a whole nested path in one command. To remove an empty directory, there is a specific command that will fail if the directory contains any files or subdirectories. That is a safety feature. To remove a directory and all its contents, you need a recursive remove command. Be extremely careful with that command; once you execute it, everything inside is gone forever.

Files themselves are created in several ways. You can create an empty file with a given name, or update its modification time if it already exists. To create a file with content directly, you can use redirection to write or append text. Copying files and directories relies on copy commands, which can target single files, rename them during the copy, or recursively copy entire folders. Moving and renaming use the exact same operation in the file system. You can rename a file in place, move it to a new folder, or move and rename simultaneously. Be aware that moving does not leave the original behind. To delete files permanently, you use the remove command. There is no trash bin.

### Permissions and Ownership
The long listing output contains a lot of information. The first column shows ten characters like `-rwxr-xr--`. The very first character tells the type: a dash for a regular file, `d` for a directory, `l` for a symbolic link. The next nine characters are three groups of three, permissions for the owner, the group, and others. `r` means read, `w` means write, `x` means execute. These permissions control what you can do with a file. To change permissions, you use modification commands with symbolic notation (like adding or removing specific rights for users, groups, or others) or numeric methods (using numbers like 4 for read, 2 for write, 1 for execute). 

Ownership in Termux is simple because you are the only user. The columns show owner and group, but they will both be your Termux user name and group. The command to change ownership exists, but you cannot use it to give files to other users because you lack root privileges and there are no other users anyway. So you can safely ignore it in Termux.

### Links, Size, and Discovery
Beyond regular files and directories, there are links. Links are references that point to other files. A symbolic link, or symlink, is like a shortcut. When you enter it, you actually go to the real folder. A hard link is different; it is another name for the exact same file data. If you delete the original file, the data remains as long as at least one hard link exists. However, hard links cannot span different file systems and cannot link to directories, so in everyday use you will mostly use symbolic links.

You often need to know how large your files and directories are. You can check individual file sizes, the total space a directory uses, or check free disk space across all mounted file systems. Keeping an eye on space is important because Termux is limited by your phone's storage.

Finding files when you lose track of them uses search commands. You can search by name, by type, or use case-insensitive matching. For quick location of files by name, you can install specialized locate tools and build a database. Determining the type of a file regardless of its name extension is done by reading the file header, which is extremely helpful when you have a file with no extension or a misleading one. 

The file system relies heavily on wildcards for efficient work. The asterisk matches any number of characters, the question mark matches exactly one character, and brackets match a set of characters. One more advanced but important concept is that everything in the file system is a file. Directories are files that list their contents. Devices are represented as files. This uniformity is a key Unix idea. In practice, you can treat almost everything as a file and use the same commands to read from it or write to it.

## Examples

```
termux-setup-storage
```
Sets up the storage directory. It creates a folder inside your home called `storage`, giving you doorways to files that other apps can see.

```
ls -a
```
Shows all files in a directory, including hidden dotfiles.

```
pwd
```
Prints the absolute path of your current working directory. It is your you-are-here marker.

```
ls -lah
```
A very popular combination that shows a long listing of all files with human-readable sizes, including hidden files.

```
ls -l /storage/downloads
```
Lists a specific directory without moving there first.

```
ls -ltr
```
Shows files with the oldest at the top and sorts by modification time, which is helpful when looking for recent changes.

```
cd
```
With no arguments, this goes to your home directory.

```
cd -
```
Goes back to the previous directory, like a toggle.

```
cd ..
```
Moves up one level to the parent directory.

```
cd storage/downloads
```
Moves into the downloads link using a relative path.

```
mkdir -p projects/websites/myblog
```
Creates a whole nested path all in one command. If any of them already exist, no error is thrown.

```
rmdir directoryname
```
Removes an empty directory. It will fail if the directory contains any files.

```
touch greeting.txt
```
Creates an empty file. If it already exists, it simply updates its modification time to the current moment.

```
echo "Hello World" > greeting.txt
```
Creates a file named `greeting.txt` containing the text. The single greater-than sign overwrites completely.

```
echo "Second line" >> greeting.txt
```
Appends text to the end of a file instead of overwriting it.

```
cp notes.txt backup/notes_copy.txt
```
Copies a file and gives it a new name in the destination folder.

```
cp -r myfolder newlocation
```
Copies a directory and its entire contents recursively.

```
mv file.txt /storage/downloads/newfile.txt
```
Moves and renames a file simultaneously. 

```
rm unwanted.txt
```
Removes a file forever; there is no trash bin.

```
rm -ri myfolder
```
Asks for confirmation before each file deletion. This is slow but prevents catastrophic mistakes.

```
echo *.txt
```
Previews wildcard expansion to see the list that the asterisk will match before running a destructive command.

```
chmod +x script.sh
```
Adds execute permission for everyone. For everyday use, making scripts executable is the most common task.

```
chmod 755 script.sh
```
Sets permissions to `rwxr-xr-x` using the numeric method.

```
ln -s /storage/downloads ~/downloads
```
Creates a symbolic link in your home that points to the downloads folder.

```
du -sh ~
```
Shows the total space your home directory uses in a human-readable format.

```
df -h
```
Checks free disk space across all mounted file systems.

```
find ~ -name "*.py"
```
Finds all Python files in your home directory. The pattern needs to be quoted to prevent the shell from expanding the asterisk early.

```
file myfile
```
Reads the file header and tells you if it is ASCII text, a PDF document, an ELF executable, a PNG image, and so on.

### Real-Life Organization Example Step-by-Step

```
cd
```
Start in your home directory.

```
ls -la
```
Check what is there. You see some dotfiles and maybe a previous folder.

```
mkdir myproject
```
Create a project directory.

```
cd myproject
```
Move into it.

```
mkdir src data
```
Create subdirectories for code and data.

```
touch README.md
```
Create an empty README file.

```
echo "# My Project" > README.md
```
Write a short description into it.

```
cat README.md
```
Check the content.

```
mv data docs
```
Rename the data directory to docs.

```
ls
```
List to confirm.

```
cp README.md README_backup.md
```
Create a backup of your README file.

```
rm README_backup.md
```
Remove the backup once you realize you do not need it.

```
touch setup.sh
```
Create a script file.

```
chmod +x setup.sh
```
Make the script executable.

```
du -sh .
```
Check disk usage to see the size of the entire myproject folder.

```
find . -name "*.md"
```
Find all Markdown files in the current directory.

## Common Mistakes
- Using a backslash instead of a forward slash. Typing `Documents\file.txt` will not work. The correct format is `Documents/file.txt`.
- Forgetting that the file system on Android is case-sensitive, so `documents` is not the same as `Documents`.
- Forgetting that whitespace in filenames needs quoting or escaping. If you download a file called `My Notes.txt`, you must use quotes or escape the space.
- Using `rm -rf` without a safety check. **Always double-check your current directory and look at the path before pressing Enter.** - Thinking that `cp -r` can be used to effectively move a directory. It copies it, meaning you still must delete the original. Use `mv` for moving, which handles it in one atomic operation.
- Trying to run an installed program or script from the current directory without typing `./` first. Installed programs go to your PATH, but local scripts need `./myscript.sh` to prevent malicious executions.
- Getting confused by `df` and looking at Android system partitions that Termux cannot write to. Focus only on the entry for `/data` or `/data/data/com.termux/files`.
- Using `rm -rf .*` to delete hidden files. This dangerously matches both `.` and `..`, which attempts to delete the current and parent directories, causing chaos.

## Quick Tips
- Use `tree` or `tree -L 2` to get a visual overview of nested directory structures. (Install it with `pkg install tree`).
- Use `du -sh * | sort -h` to see items sorted by size, with the largest files at the bottom.
- Use `alias ll='ls -lah'` in your `.bashrc` to have a quick long listing shortcut available at all times.
- Use `touch -t` to set arbitrary timestamps on files for testing purposes.
- Use `mkdir -p` to confidently create directories in scripts without throwing errors if they already exist.
- Use `find` with `-maxdepth 1` to limit your search strictly to the current directory.
- Use `stat filename` to view all deep file timestamps, including access time, modification time, and change time.
- Use `chmod` without fear when you need to make a script runnable; it is completely safe and reversible.
- Use `readlink -f` to resolve symlinks and clearly display the actual absolute path of any item.
- Use `shred` or `rm -P` if you need to securely delete sensitive files, though keep in mind its effectiveness on flash storage is debatable.
- Always keep an eye on `df -h /data`. Termux uses a single path, and filling your home with large files can prevent Termux from installing new packages or running system operations.
- If you want to edit a file but are unsure of its location, use `find` to locate it quickly, and combine it with `grep` to search inside files if needed. 
- Explore `/data/data/com.termux/files/usr/bin` to see all the commands you can run, and `/data/data/com.termux/files/usr/share` for documentation and data.

---
