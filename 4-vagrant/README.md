# VAGRANT 

The documentation is divided in two parts:
- [Part 1](#1-useful-unix-commands-to-run-vagrant): the Unix commands (to be run in the terminal) in order to run Vagrant
- [Part 2](): the syntax of the `Vagrantfile` (Ruby language) that will allow us to launch the Virtual Machines as coded.

## 1 - Useful unix commands to run Vagrant
### 1.1 Launching the VM
```vagrant up```
- initializes the virtual machine, with the specifications of the Vagrantfile on the current folder

```vagrant provision```
- downloads the required packages to make the virtual machine work (checks for any updates in the Vagrantfile).

```vagrant reload --provision```
- restarts vagrant with new Vagrantfile config, provisioning all required packages (provision). This command is useful to reload the VM after we modified the Vagrantfile.

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