# UNIX COMMANDS CHEATSHEET

This document lists useful commands to be used while working on a UNIX shell: from basic file and folder navigation, to running processes. 

Note: all the commands listed on this document will only work on a UNIX terminal.

## 1 - Basic commands
### 1.0 Get help
```<command> --help```
- Will output syntax guidelines to run any command

### 1.1 File and folder navigation
#### Move through folders
```cd <path>```
- cd stands for "change directory"; this command moves the folder the terminal is looking to into to the specified absolute or relative path. Example: `cd /folder` will move to `folder` (which should be inside the folder we are currently looking to).
- `cd ..` moves to the upwards (or 'preceding') directory

Note: in some terminals, typing `cd ` (with a space), and pressing `Tab` allows the terminal to jump between available sub-folders possible options.

```pwd```
- stands for "Print Working Directory": returns the absolute path of the current directory

#### Show folder contents
```ls```
- lists current directory contents (prints the filenames)
Options:
- use `ls -l` to output the file details. `-l` stands for 'long' listing format.
- use `ls -a` to print all files (normal files and hidden ones). `-a` stands for 'all'
- use `ls -la` to combine above 

#### Create, Update, Delete files and folders
- `rm <directory>/<file>`: deletes (`rm` stands for 'remove') `<file>` in `<directory>` 
- `rm -r <directory>` deletes `<directory>` and its contents. Note: this command needs `-r` (Recursive), since the OS will need to recursively enter every folder and file in the directory to completely erase it.
- `mv <old_directory>/<file> <new_directory>/<file>` moves `<file>` from a directory to another
- `mv <old-file-name> <new-file-name>` renames file
- `mkdir <new-directory-name>` creates a new directory in current path

### 1.2 - Check file contents
#### The `cat` command
The command `cat` is one of the most useful commands to quickly check on the terminal the contents of a file. `cat` stands for 'concatenate': the contents of the file will be 'concatenated' and shown in the terminal.

```cat <filename>```
- Prints on the terminal the contents of `<filename>`

Additional arguments we can use for `cat`:
- `cat -n <filename>` will print the contents of the file with a number showing the line number

### 1.3 - 

## 2 - Environment variables
'Environment variables' are variables stored in special folders, in order to only reveal its contents locally (on the terminal), and if requested.

Environment variables very useful to store confidential data such as passwords and API keys, which we do not want to reveal in our source code or uploaded in GitHub, for example. They can also be used to run code in different machines, where the value of `HOME` is different, for example.

Note: in Unix systems, global environment variables are stored in the `/etc/environment` folder and user level variables in `.bashrc` and `.profile` files of the user's Home folder.

#### Environment variables to know
- `PATH` is the list of folder paths (separated by `:`) that our terminal will look into to understand the commands we run in the terminal.
- `HOME` is the absolute location of the user's home directory

#### Get list of environment variables
```printenv```
- prints in the terminal the list of currently set environment variables (alternatively, we can use the command `env`)

```set```
- displays the entire list of set or unset values of shell options (environment variables). Gives a much more complete list than  `env`, with all predefined evironment variables (even those that have no value assigned to it)

#### View contents of environment variables
```echo $<environment-variable>```
- Displays the value of the environment variable. Example: `echo $PATH`

Note: the `$` sign is used by Linux to access the value of environment variables

#### Update environment variables
```export <env-variable>=<variable-content>```
- Sets up the contents of an environment variable. Example: `export PATH=$PATH:opt/bin` adds an address to `PATH`.