# VAGRANT 

The documentation on Vagrant is divided in three parts:

**[0 - Basics of Vagrant and intuition](#basics-of-vagrant-and-intuition)**: why is Vagrant useful at all?

**[1 - Useful commands to run Vagrant](vagrant-commands.md)**: some useful commands (to be run in the terminal) to run Vagrant

**[2 - Defining the `Vagrantfile`](vagrantfile-syntax.md)**: the syntax of the Vagrantfile (Ruby language) that will allow us to launch the Virtual Machines as coded. (In progress)

# Basics of Vagrant and intuition
Vagrant is one of the components we will use the most during the course, and a very handy DevOps tool. In a nutshell, Vagrant allows us to define a set of basic steps to get a Virtual Machine ready according to a set of specifications (which will be defined in the `Vagrantfile`). 

It is a DevOps tool since it **automates** the process of starting and adding packages to VM, ensuring the it will run the same way every time we run the same `Vagrantfile`, even across different computers!

## The `Vagrantfile`
The basic file we need to take care once vagrant is installed is `Vagrantfile` (which uses the `Ruby` syntax), and lists the requirements for running the VM. We will encode statements such as `Allocate 1024 MB of RAM for the VM`,  `Download Python 3`, `Forward any traffic received on port 5000 in the VM to port 5000 in the local machine`, etc.

The `Vagrantfile` syntax will be explained in more detail in [this section](vagrantfile-syntax.md).

## The commands
Vagrant also installs a set of commands on our local machine, which will allow us to manage VMs though command-line statements, which are [listed in this section](vagrant-commands.md).