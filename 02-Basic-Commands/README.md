# Basic Commands

## Introduction

You have a terminal open and a prompt waiting. The first steps of moving around and looking at files are behind you. Now it is time to learn the words and phrases that make the command line useful. These are the basic commands, the core vocabulary you will use every single time you open Termux. They let you see what is on your device, move things around, read files, find information, and manage running programs.

This guide will walk you through every essential command in detail, with real examples you can type and watch happen. By the end, you will have a solid working knowledge of the most important tools in your terminal.

## What You Will Learn

- How commands are structured with options and arguments
- How to identify where you are and who you are in the terminal
- How to list, view, and navigate files and directories
- How to create, copy, move, and delete files and directories
- How to read and search file contents
- How to find files by name and view system information
- How to manage running processes
- How to change file permissions
- How to combine commands with pipes and redirections
- How to use command history and keyboard shortcuts efficiently

## Main Content

### How Commands Are Structured

Almost every command works like this: you type the name of the command, then you add options to change its behavior, and then you provide arguments, which are the targets the command works on. Options usually start with a single dash followed by a letter, like `-l`, or two dashes followed by a word, like `--help`. Arguments are often file or directory names. Spaces separate each part.

For example, `ls -l /storage/downloads` uses the command `ls`, the option `-l`, and the argument `/storage/downloads`. Knowing this general structure will make learning new commands faster.

### Finding Out Where and Who You Are

`pwd` prints the working directory — the full path of the directory you are currently in.

`whoami` prints the username Termux assigned to you, something like `u0_a123`. This matters when you deal with permissions or when you connect to other systems later.

`hostname` outputs the name of your current machine, usually `localhost`. These small commands are helpful when you are in an unfamiliar environment.

### Listing Directory Contents with ls

`ls` is the command you will use more than any other. It lists directory contents. Options can be combined.

- `ls` — shows the names of files and folders in the current directory
- `ls -l` — long listing with permissions, owner, size, date, and name
- `ls -a` — shows all files, including hidden ones (hidden files start with a dot, like `.bashrc`)
- `ls -la` — long listing of all files, including hidden ones
- `ls -lh` — long listing with sizes in human-readable form, like `1.5K` instead of `1536`
- `ls -R` — lists directories recursively, showing contents of all subdirectories
- `ls /path/to/directory` — lists a specific directory without moving there first

The permissions column looks something like `-rw-------` and describes who can read, write, or execute the file. Capital letters and lowercase letters are sorted separately by default. Hidden files are not shown unless you use `-a`.

### Navigating with cd

- `cd` — with no arguments, takes you back to your home directory
- `cd ..` — moves up one level in the directory tree
- `cd -` — takes you to the previous directory you were in, useful for toggling between two locations
- `cd ../../storage/downloads` — moves up twice and then into a folder in one command

Remember that paths are case-sensitive. `cd Downloads` is not the same as `cd downloads`. Linux uses forward slashes; Windows uses backslashes. In Termux, always use the forward slash.

### Reading File Contents

- `cat filename.txt` — prints the entire file to the screen in one go; good for short files
- `cat -n filename.txt` — prints the file with line numbers
- `less filename.txt` — opens the file in a scrollable pager; use arrow keys to scroll, Q to quit; install with `pkg install less`
- `head filename.txt` — prints the first 10 lines of a file
- `head -n 5 filename.txt` — prints the first 5 lines
- `tail filename.txt` — shows the last 10 lines
- `tail -f filename.txt` — follows the file and shows new lines as they are added; press Ctrl+C to stop

`less` is preferred over `more` for longer files. `less` is more flexible.

### Creating Directories with mkdir

- `mkdir newfolder` — creates a new directory inside the current one
- `mkdir dir1 dir2 dir3` — creates multiple directories at once
- `mkdir -p a/b/c` — creates a whole nested path all at once, even if none of them existed before

Without the `-p` option, trying to create nested directories that do not yet exist will produce an error.

### Removing Directories with rmdir

`rmdir` only works on directories that have no files in them. That is a safety measure. To remove a directory and everything inside it, use `rm -r dirname`, covered in the next section.

### Creating Files with touch

- `touch newfile.txt` — creates an empty file with that name
- If the file already exists, `touch` updates its modification timestamp to the current time

### Copying Files with cp

- `cp source destination` — copies a file; for example, `cp myfile.txt backup/` creates a copy inside the `backup` directory
- `cp -r sourcefolder destinationfolder` — copies a directory and its entire contents recursively

Copying preserves the original file.

### Moving and Renaming with mv

`mv` serves as both the move command and the rename command.

- `mv oldname newname` — renames the file or directory
- `mv file.txt /storage/downloads/` — moves the file to that directory, keeping the same name
- `mv file.txt /storage/downloads/newname.txt` — moves and renames at the same time

`mv` does not leave the original behind. Moving a file is effectively cutting and pasting it. There is no recycle bin, so be deliberate.

### Deleting Files with rm

- `rm filename.txt` — removes the file immediately with no undo
- `rm -r directoryname` — deletes a directory and all its contents recursively
- `rm -i filename.txt` — asks for confirmation before each deletion; slow but safe
- `rm -ri myfolder` — asks before every deletion inside a folder

**Avoid `rm -rf` unless you are absolutely sure.** The `-f` flag forces deletion without any prompts. A misplaced `rm` can delete all your work. Always double-check the path before pressing Enter. Get into the habit of running `ls` first to see what is there.

### Printing Text with echo

- `echo "Hello Termux"` — outputs that string to the terminal
- `echo "This is a line of text" > myfile.txt` — writes that line to a file, overwriting if it exists
- `echo "Another line" >> myfile.txt` — appends that line to the end of a file

This is the simplest way to create small text files without an editor.

### Searching File Contents with grep

- `grep pattern filename` — searches for lines containing the pattern in that file
- `grep error mylog.txt` — shows every line that has the word "error"
- `grep -i error mylog.txt` — case-insensitive search
- `grep -r pattern directory` — searches recursively through all files in a directory

Always put patterns that contain spaces in single quotes, like `grep 'error occurred' log.txt`.

### Finding Files with find

- `find directory -name filename` — searches for a file by name
- `find /storage -name '*.pdf'` — finds all PDF files in shared storage and subdirectories
- `find . -name myfile.txt` — searches only the current directory

The single quotes around `*.pdf` prevent the shell from expanding the asterisk too early. Running `find` on a large directory without specifying a name can take a long time and produce enormous output.

### System and Session Information

- `date` — prints the current date and time
- `cal` — prints a calendar of the current month
- `cal 2026` — prints the calendar for the entire year
- `uptime` — shows how long the system has been running
- `df -h` — shows available disk space in human-readable form; the `/data` line shows your device's free space
- `du -sh directoryname` — shows how much space a specific directory and its contents use; for example, `du -sh ~` for your home directory

`df` reports file system usage. `du` reports directory usage.

### Managing Processes with ps and kill

- `ps` — shows processes associated with your current terminal session
- `ps aux` — shows all processes running under your user

The PID (process ID) in the output is important because you can stop a process with it.

- `kill PID` — sends a termination signal to the process with that ID
- `kill -9 PID` — forces the process to stop; use only when necessary
- `pgrep -f python` — finds processes whose command line contains "python" and prints their PIDs

Using `pgrep` to find a PID and then `kill` on that PID is safer than `killall`, which kills all processes with a given name and can be dangerous if you type the wrong name.

### Managing Command History

- `history` — prints a numbered list of commands you have typed recently
- `!42` — reruns the command with that number from your history

The history is stored in a file called `.bash_history` in your home directory. Do not type passwords directly into the command line if you do not want them saved. Many commands that require a password will prompt securely without echoing. You can clear the in-memory history with `history -c`.

### Changing File Permissions with chmod

- `chmod +x myscript.sh` — adds execute permission, making the script runnable
- `chmod -w file.txt` — removes write permission so the file cannot be accidentally modified
- `ls -l` — view permissions for files

Permissions appear as three groups of three characters in the `ls -l` output: owner, group, others. Read is `r`, write is `w`, execute is `x`. For example, `-rwxr-xr--` means the owner can read, write, and execute; the group can read and execute; others can only read. Making scripts executable is an everyday task in Termux.

### Combining Commands with Pipes and Redirections

A pipe, written with the vertical bar symbol `|`, takes the output of one command and feeds it as input to another.

- `ls -l | less` — opens a long directory listing in the pager so you can scroll
- `cat myfile.txt | grep error` — filters file content to show only lines with "error"
- `ps aux | grep termux` — finds processes related to Termux

Redirection sends output to a file:

- `>` — redirects output to a file, overwriting if it exists
- `>>` — appends output to a file
- `2>` — redirects error messages to a file; for example, `ls nonexistent 2> error.log`

### Small but Useful Commands

- `clear` — clears the terminal screen; Ctrl+L does the same
- `reset` — resets the terminal if it gets garbled
- `exit` — closes the terminal session
- `sleep 5` — pauses for five seconds; useful in scripts
- `wc -l filename.txt` — counts the number of lines in a file
- `wc -w filename.txt` — counts the number of words in a file
- `tee output.txt` — duplicates a stream, writing to a file and to the terminal at the same time; for example, `./myscript.sh | tee output.txt`
- `file somefile` — tells you what type a file is: text, directory, PDF, executable, etc.
- `time ls` — shows how long a command takes to run
- `type ls` — shows whether a command is an alias, a builtin, or an external program and where it is located

### Getting Help

- `command --help` — outputs a brief summary of options for almost any command; for example, `sort --help`
- `pkg install man` — installs the manual system; then `man ls` shows the full manual for `ls`
- `whatis ls` — gives a one-line description of a command; requires `man` to be installed

In practice, searching the web for "ls command linux" provides the same information as the manual.

### Aliases and Shell Shortcuts

Aliases are shortcuts you can define to save typing.

- `alias l='ls -lh'` — creates an alias so that `l` runs `ls -lh`; lasts for the current session only
- To make aliases permanent, add them to your `.bashrc` file

Keyboard shortcuts for editing the command line:

- `Ctrl+A` — jump to the start of the line
- `Ctrl+E` — jump to the end of the line
- `Ctrl+K` — cut from the cursor to the end of the line
- `Ctrl+U` — cut from the cursor to the beginning of the line
- `Ctrl+Y` — paste what you cut

## Examples

### Viewing where you are and who you are

```
pwd
```

Prints the full path of your current directory.

```
whoami
```

Prints your Termux username.

```
hostname
```

Prints the device hostname, usually `localhost`.

### Listing files with different options

```
ls -la
```

Shows a long listing of all files including hidden ones in the current directory.

```
ls -lh /storage/downloads
```

Shows a detailed listing of your Downloads folder with human-readable file sizes.

### Navigating directories

```
cd storage
```

Moves into the `storage` directory.

```
cd -
```

Switches back to the previous directory you were in.

```
cd ../../storage/downloads
```

Moves up two levels and then into `storage/downloads` in one command.

### Reading a file

```
cat myfile.txt
```

Prints the entire file to the screen.

```
less readme.txt
```

Opens the file in a scrollable pager. Press Space to page down and Q to quit.

```
head -n 5 readme.txt
```

Shows only the first 5 lines of the file.

```
tail -f ~/mylog.txt
```

Follows the log file and displays new lines as they are added. Press Ctrl+C to stop.

### Creating nested directories

```
mkdir -p a/b/c
```

Creates the full path `a/b/c` all at once, even if none of the folders exist yet.

### Copying a directory

```
cp -r sourcefolder destinationfolder
```

Copies the entire folder and all its contents into the destination.

### Moving and renaming a file

```
mv file.txt /storage/downloads/newname.txt
```

Moves `file.txt` to the Downloads folder and renames it to `newname.txt` in one step.

### Safe deletion with confirmation

```
rm -ri myfolder
```

Asks for confirmation before deleting each file inside `myfolder`. Slow but safe.

### Writing to a file with echo

```
echo "This is a line of text" > myfile.txt
```

Creates `myfile.txt` and writes that line to it. Overwrites if the file exists.

```
echo "Another line" >> myfile.txt
```

Appends that line to the end of `myfile.txt` without overwriting.

### Searching file contents

```
grep -i error mylog.txt
```

Finds every line containing "error" in the log file, ignoring case.

```
grep -r 'error occurred' ~/projects
```

Searches recursively through all files in the `projects` directory for that phrase.

### Finding files by name

```
find /storage -name '*.pdf'
```

Searches all of shared storage and its subdirectories for files ending in `.pdf`.

```
find . -name myfile.txt
```

Searches only the current directory and its subdirectories.

### Checking disk and directory space

```
df -h
```

Shows available disk space for all file systems in human-readable form.

```
du -sh ~
```

Shows how much total space your home directory is using.

### Managing a process

```
ps aux
```

Lists all running processes for your user.

```
pgrep -f python
```

Finds processes whose command line contains "python" and prints their PIDs.

```
kill 1234
```

Sends a termination signal to the process with PID 1234.

### Making a script executable and running it

```
chmod +x myscript.sh
```

Adds execute permission to the script.

```
./myscript.sh
```

Runs the script from the current directory. The `./` is required.

```
./myscript.sh | tee output.txt
```

Runs the script, shows output on screen, and saves it to `output.txt` at the same time.

### Organizing downloaded files

```
cd /storage/downloads
```

Navigate to the Downloads folder.

```
ls -l
```

See what is there.

```
mkdir PDFs Images
```

Create two new directories.

```
mv *.pdf PDFs/
```

Move all PDF files into the PDFs folder. The `*` wildcard matches any characters.

```
mv *.jpg Images/
```

Move all JPG files into the Images folder.

```
find . -name 'report'
```

Find a specific file starting from the current directory.

### Counting lines in a file

```
wc -l myfile.txt
```

Outputs the number of lines in the file.

### Checking what type a file is

```
file /bin/ls
```

Outputs a description of the file type, such as whether it is an executable or a text file.

### Measuring how long a command takes

```
time ls
```

Shows the real time, system time, and user time taken to run `ls`.

### Checking what a command is

```
type ls
```

Shows whether `ls` is an alias, a shell builtin, or an external program, and where it is located.

```
type cd
```

Shows that `cd` is a shell builtin, meaning it is part of bash itself.

### Monitoring a log file in real time

Open one terminal session and run:

```
tail -f ~/mylog.txt
```

In a second session, append something to the log:

```
echo "New entry" >> ~/mylog.txt
```

The first terminal updates immediately to show the new line.

## Common Mistakes

- Confusing `>` and `>>` — a single `>` overwrites the file completely; `>>` appends; many people have accidentally destroyed file contents by using `>` when they meant `>>`
- Using `rm` with wildcards without previewing — before running `rm *.tmp`, first run `ls *.tmp` to see exactly which files will be deleted
- Forgetting to quote file names with spaces — `ls My Documents` tries to list two separate things; use `ls 'My Documents'` or let tab completion handle the escaping
- Forgetting `./` when running a script — typing `myscript` alone will not work because the shell looks in the PATH, not the current directory; you must type `./myscript`
- Running `find` without a name on a huge directory — this can take a long time and produce overwhelming output
- Thinking a command hung when it returned no output — `grep` finding nothing returns no lines and gives back the prompt silently; if the prompt does not return, the command may be waiting for input; use Ctrl+C to break out
- Accidentally running `cat` or similar commands without a filename — they will wait for you to type input from standard input; press Ctrl+C to exit
- Running `rm -rf *` in the wrong directory — the asterisk means everything in the current directory; this is one of the most destructive mistakes possible; always verify your location with `pwd` first
- Forgetting that paths are case-sensitive — `cd Downloads` and `cd downloads` are different
- Using a backslash instead of a forward slash — Termux uses forward slashes in paths, not backslashes

## Quick Tips

- Use Tab completion relentlessly — it completes file names and paths, prevents spelling errors, and handles spaces and special characters in names automatically
- Use the up arrow to recall previous commands and fix typos without retyping the entire command
- Use `Ctrl+R` to search your command history by typing part of a command
- Use `Ctrl+A` and `Ctrl+E` to jump to the start and end of the current line
- Use `Ctrl+K` and `Ctrl+U` to cut text from the cursor position, and `Ctrl+Y` to paste it back
- Use `ls` before `rm` to preview what you are about to delete
- Use `rm -i` or `rm -ri` when you are not fully sure — the confirmation prompts are worth the extra keystrokes
- Use `ls -lh` instead of `ls -l` for easier-to-read file sizes
- Use `tail -f` to monitor a log file as it grows in real time
- Use `less` instead of `cat` for files that are longer than your screen
- Use `grep -r` to search across all files in a project directory at once
- Use `find . -name` with single quotes around patterns that contain wildcards
- Use `pgrep` to find a process PID safely before using `kill`
- Use `file somefile` when you are not sure what a file is before opening it
- Use `time` in front of any command to measure how long it takes
- Use `type commandname` to find out if a command is a builtin, alias, or external program
- Use `alias` to create shortcuts for commands you type repeatedly; add them to `.bashrc` to make them permanent
- Use `pkg install coreutils` if a command option you found online does not work — Termux may use a minimal version of some utilities by default
