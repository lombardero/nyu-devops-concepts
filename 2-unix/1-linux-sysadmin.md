# Basics of Linux system administration

# 1 - Introduction

## 1.1 Everything is a file

The very basic concept one must grasp when working on a Linux system is this: everything
is a file. Directories, processes, external components (such as keyboards or mouses) are
files which can accept standard input (receive information) and standard output (send
information). In a linux system, for example, a keyboard is a file on the `/??` folder
that emits as standard output the letters that the user types on the keyboard. This stream
of data is then captured by running processes (such as the code editor) that are
expected to use this data.

## 1.2 The Kernel

The kernel is an important concept to grasp while entering the world of Linux system
administration. As explained [in the introduction of this documentation](),
it is the central part of the Operating Systems that manages the computer resources
in order to performs the tasks the user asks it to do.



# 2 - Filesystem structure

All Linux systems come with the same file structure,


Here is a description of all basic directories:
* `/boot`: contains all the files needed for the system to boot. When it starts, it looks for a hardcoded file (ex: file `grub.cfg` tells the system which OS to boot).
* `/root`: the home directory of the root user (not to be confused with the `/` directory)
* `/dev`: system devices, all devices (ex: keyboard, mouse, etc) will be a file inside this directory
* `/etc`: configuration files of applications that are built on top of linux, or that come with linux (mail, etc). Important to do a backup of the folder before touching any config file
* `/bin` (link to `/usr/bin`): contains the binaries for everyday user commands
*  `/sbin` (link to `/usr/sbin`): contains binaries for system commands
* `/opt`: optional add-on applications (not part of OS).
* `/proc`: folder storing files (created by the kernel) for each running program (when it computer starts, it should be empty)
* `/lib` (now points to `/usr/lib`) stores C programming library files needed by commands and apps (ex: `cd` and `pwd` use some C libraries)
* `/tmp`: contains all temporary files 
* `/home`: directory for user (each user has a directory inside “home”
* `/var`: where the system stores its logs (error logs, etc.)
* `/run`: stores temporary runtime files (ex: PID files) used by system daemons that start very early 
* `/mnt`: used to mount external filesystems
* `/media`: used for cdroms (ex: if you mount a virtual ISO image, it will show in this folder)

# 2 - File attributes
## 2.1 - File types
When the command `ls -l`  is run, a list of attributes is displayed for each file:
1. Type (ex: `drwxrwxrwx`), there are seven file types:
	* `d`: directory
	* `l`: link
	* `-` regular file
	* `c`: special file or device file (ex: keyboard)
	* `s`: socket
	* `p`: named pipe
	* `b`: block device
2. Number of links associated to that file
3. Owner of the directory
4. Group of the directory
5. Size
6. Month / Day / Time
7. Name
