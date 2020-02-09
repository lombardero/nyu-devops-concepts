# VAGRANT 

The documentation is divided in three parts:

**[0 - Basics of Vagrant and intuition](#0---basics-of-vagrant-and-intuition)**: why is Vagrant useful at all?

**[1 - Useful commands to run Vagrant](#1---useful-commands-to-run-vagrant)**: some useful commands (to be run in the terminal) to run Vagrant

**[2 - Defining the `Vagrantfile`](#2---defining-the-vagrantfile)**: the syntax of the Vagrantfile (Ruby language) that will allow us to launch the Virtual Machines as coded. (In progress)

## 0 - Basics of Vagrant and intuition
Vagrant is one of the components we will use the most during the course, and a very handy DevOps tool. In a nutshell, Vagrant allows us to define a set of basic commands to get a Virtual Machine ready according to a set of specifications (which will be defined in the `Vagrantfile`). 

It is a DevOps tool since it **automates** the process of starting and adding packages to VM, ensuring the it will run the same way every time we run the same `Vagrantfile`, even across different computers!

### The `Vagrantfile`
The basic file we need to take care once vagrant is installed is `Vagrantfile` (which uses the `Ruby` syntax), and lists the requirements for running the VM. We will encode statements such as `Allocate 1024 MB of RAM for the VM`,  `Download Python 3`, `Forward any traffic received on port 5000 in the VM to port 5000 in the local machine`, etc.

The `Ruby` syntax will be explained in the second part of this document.

### The commands
Vagrant also installs a set of commands on our local machine, which will allow us to manage VMs though command-line statements (described in the paragraph below).


## 1 - Useful commands to run Vagrant
These commands must be run in the terminal in order to control a Vagrant-generated VM.

### 1.1 Launching the VM
```vagrant up```
- initializes the virtual machine, with the specifications of the Vagrantfile since last time we ran `provision`. Note that the terminal must be 'looking' in the folder where the Vagrantfile is.

```vagrant provision```
- checks the Vagrantfile, and downloads the required packages (if any is missing) to make the virtual machine work.

```vagrant reload --provision```
- restarts Cagrant VM with a new Vagrantfile configuration, provisioning all required packages (same as running `provision`). This command is useful to reload the VM after we modified the Vagrantfile.

### 1.2 Connecting to the VM
```vagrant ssh```
- Vagrant accesses the initialized VM through SSH. After running this command, we 'enter' the VM and can pass commands to it. (To 'get out' of the VM, the command `exit` can be used).

Note: if we `exit` a running VM, it will not stop running, for that we need to explicitely halt it, as show below.

### 1.3 Halting the VM
```vagrant halt```
- stops the current vagrant VM running

```vagrant suspend```
- suspends current VM running (same as 'hibernating': saves the current state of the machine)

```vagrant resume```
- resumes suspended VM

```vagrant destroy```
- removes the VM from your hard disk

 ### 1.4 Checking status
```vagrant status```
- shows the status of the virtual machine on the current folder (tells us if it is running or not)

```vagrant gobal-status```
- shows the status of all created VMs in the machine

## 2 - Defining the `Vagrantfile`

(In progress)