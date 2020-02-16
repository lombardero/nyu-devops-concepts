# Understanding the syntax of the `Vagrantfile`

As mentioned in the [introduction](/4-vagrant/README.md#basics-of-vagrant-and-intuition) of this part, the `Vagrantfile` is simply a 'list of tasks' that Vagrant needs perform to set up our application's environment. These tasks follow in four categories (each one will be a chapter of this document):
- **[1 - Launching the VM](#1---launching-the-vm)**: Vagrant needs to know which operating system to use, how much CPU and RAM it requires, which ports should we forward, and which files should we share with the VM.
- **[2 - Setting up the evironment](#2---setting-up-the-environment)**: Vagrant will need to run Unix commands to get the evironment ready for us to run our application in.
- **3 - Launching Docker containers**: (to be done)

Before jumping into these parts, it is important to mention the basics of the `Vagrantfile` syntax, which is written in `Ruby`. Luckily, it is not necessary an extensive knowledge of `Ruby` to use Vagrant; all we need to understand is on the chapter 'zero' below.

# 0 - Understanding the `Vagrantfile`
Vagrant works by introducing a `Vagrant` object that sets up the configuration. The only thing we need to understand for this course is that all commands in the `Vagrantfile` simply update this `Vagrant` object, which will be the one used by Vagrant to launch and set the VM.

Normally, all `Vagrantfile`s have this basic syntax:
```Ruby
Vagrant.configure(2) do |config|

  # Configuration definition (see section 1 'Launching the VM')
end
```
- The code above allows us to modify the `Vagrant` object just created; The `|config|` statement defines the name we will use to access it (inside the `do` statement, everytime we call `config`, the `Vagrant` object will get updated).

> Note: the number `2` inside the `.configure()` method represents the version of the configuration object that will be used between the `do` and the `end`. 

All commands defined in the below parts should be added between the `do` and `end` statements above.

# 1 - Launching the VM
In this section, we will add the commands required to tell Vagrant the infrastructure (CPU, RAM), and the operating system required. We will define these commands through the `.vm` statement.
## 1.1 Setting up the VM requirements
To set up the Infrastructure requirements (CPU, RAM) needed for the VM, we need to define the the VM provider (in our case, it will always be `"virtualbox"`), as well as access the arguments associated to it:
```Ruby
#...
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 1
    vb.memory = "4096"
#...
```
- Defines the configuration for the VM launched by Virtualbox: `.cpus` defines the number of CPU workers, while `.memory` defines the number of MB of RAM required.

## 1.1 Setting up the Operating System
```Ruby
#...
  config.vm.box = "ubuntu/bionic64"
#...
```
- Sets up the OS to the one specified (in the case above, we are using an Ubuntu Bionic 64-bit distribution).

```Ruby
#...
  config.vm.hostname = "name-of-our-vm"
#...
```
- Sets up the display name for when we ssh into the machine (by default, thi will be set up to `vagrant`).

## 1.2 Setting up the network requirements
### Forwarding ports
During the course, we will run applications inside our VM. In order to access them in the browser of our local machine, we will need to forward the ports [as explained in this section](../0-basic-concepts/README.md#what-is-port-forwarding).

```Ruby
#...
  config.vm.network "forwarded_port", guest: port_inside_VM, host: port_local_machine, host_ip: "127.0.0.1"
#...
```
- The code above connects all traffic on the VM running in `port_inside_VM` to the `127.0.0.1:port_local_machine`.

> Note: we can remove the last part of this statement `host: "127.0.0.1"` in order to forward all traffic running inside the VM in the port specified to any IP in the host IP, although this might cause problems in Windows machines.

### Setting up the VM's private IP
In order to SSH inside the VM, its process requires to have a private IP address. We set it up with the following command:
```Ruby
#...
  config.vm.network "private_network", ip: "192.168.33.10"
#...
```
- Sets up a private network IP address which will allow vagrant to ssh into the VM (it is not necessary to specify the IP address).

## 1.3 Sharing folders with the VM
By default, Vagrant will create a `/vagrant` folder inside the VM with all contents of the folder where the `Vagrantfile` is stored (the contents of these files will be accessible both through the VM and the local machine).

To share folders with the VM we can use:
```Ruby
  config.vm.synced_folder "<folder-in-local>", "<folder-in-VM>"
```
- The code above shares the `<folder-in-local>` with `<folder-in-VM>` (both entities can modify its contents).

As an example, let's look at how sharing the working folder with the VM as a folder called `/vagrant` (what vagrant does by default) would look like:
```Ruby
  config.vm.synced_folder ".", "/vagrant"
```

## 1.4 Copying files inside the VM
We can also copy some files in our local machine to the VM using the below syntax:
```Ruby
#...
  config.vm.provision "file", source: "<path-in-local>/local-file", destination: "<path-in-vm>/filename"
#...
```
- Shares file called `local-file` in the local machine, and puts it in the specified path inside the vm.

> Note: this command will only work once `provision` is run (since we use the `vm.provision` method)

A useful implementation uses an if statement to check if the file exists. In the case it does, it forwards it inside the VM. The example below copies the `.gitconfig` (which keeps configuration about GitHub) file in our local home address (`~`) and shares it with the home address of the VM, if the file exists:
```Ruby
#...
  if File.exists?(File.expand_path("~/.gitconfig"))
    config.vm.provision "file", source: "~/.gitconfig", destination: "~/.gitconfig"
  end
#...
```

# 2 - Setting up the environment
Once the VM is set up, we can start installing and running packages on it. We do so by asking Vagrant to run command-line Unix statements (review all [unix statements on this section](../2-unix/README.md)) with the below syntax:
```Ruby
#...
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git
  SHELL
#...
```
- The code above runs the unix commands `apt-get update` and `apt-get install -y git` inside the VM after it is provisioned. Any Unix command can be automated thanks to this command

> Note: this command will only work once `vagrant provision` is run (since we use the `vm.provision` method)