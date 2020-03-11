# Docker

Like [Vagrant](../4-vagrant/README.md), Docker is a DevOps tool since it automates the process of creating an environment (packaging it in an isolated container with its application) and running applications. But it is much more than that, let's see why in this document.

The full Docker documentation is distributed in four parts:
- **[0 - Basic intuition](#basic-intuitions)**: some fundamental concepts to understand what Docker is
- **[1 - Building images with the `Dockerfile`]()**: (to be done)
- **[2 - Running instances through the command line]()**: (to be done)
- **[4 - Managing multiple instances]()**: (to be done)

# Basic intuition
Here are some important intuitions on how Docker works.

## 1 - What is containerization?
Containerization is the idea of packaging the application with its dependencies. Before virtualization and Docker existed, if we wanted to run an application in a server (or in our local machine) in order to test it, we needed to download the software packages that the application would be built on: for example, a python application requires a version of Python, flask, a Database, other libraries, etc. That becomes messy pretty fast, as developers needed to run and test different applications on the same computer; packages collided, they worked differently on different machines; in essence: a nightmare.

With that, containerization appeared. The idea is pretty simple: instead of downloading all the dependencies in our local machine and create a mess, we instead create a 'clean' and isolated virtual machine where we can install all the packages that the application requires, without affecting the main environment. That way, we keep the 'mess' isolated into different containers, or 'drawers' in a closet, which can be launched and stopped every time we want.

## 1 - What's the difference between Vagrant and Docker?
Docker and Vagrant are two different ways to build an application container; they have two major differences in the way they work:

**Vagrant**'s main distinctions from Docker are:
1. Vagrant launches full a Virtual Machine. That means that in order for it to run, Vagrant needs specify how much RAM, CPU and Storage from our local device it needs to allocate. Once the VM is running, those resources will be blocked even if our VM is not using them. On top of that, VMs are heavy-weight systems: they take some time (on the dozens of seconds order) to launch. It is exactly like "a computer inside a computer": needs to be launched and halted.
2. Like in a regular computer, Vagrant requires us to build the application 'from the ground up'. With Vagrant, we start with an empty VM, on which we install an OS, the packages we require, the databases, and all we need inside of it to run our application. All of those steps are automated by the `Vagrantfile`, but each step still takes place the same way as in a regular computer (such as, for example, running the applications).

**Docker**, on the other hand, works as follows:
1. Instead of instantiating a full Virtual Machine with specific RAM, CPU and Storage, Docker containers runs a much lighter-weight virtualization layer. It still uses a hypervisor, but Docker images run as a regular process in our laptop, without 'blocking' resources: it shares the RAM and the Storage with the local machine. This allows much more flexibility, since Docker will take only what it requires.
2. Docker works with 'images'. An image is a 'snapshot' of what a VM looked like at a point in time; what we need to know about it is that it is really fast to launch: once a docker image is created, it takes around a second to launch it. Unlike a full VM, however, Docker images cannot be un-done or modified. If we want to remove or change something, a brand new image needs to be created from scratch.

## 3 - What is a Docker image, how is it created, and how does Docker use it?
A docker image is simply "how a machine looked like at a point in time". Of course, that point in time is defined by us in the `Dockerfile`.

In the `Dockerfile`, we tell Docker what steps it needs to perform before taking the snapshot and saving it as an image, so it can be copied and run later. Here is a very simple example on how Docker creates a new image through a `Dockerfile`:
- `FROM alpine`: "go to Dockerhub (online repository), download the `alpine` image (which is a Docker image with the Alpine Linux distribution installed), and run it"
- `RUN apk --no-cache add python py-pip`: "Once Alpine is running, install the Python environement"; Note that `apk` is the Alpine version of the `apt` command (which is a package manager, it installs things).
- `ADD . /app`: "share the contents of the current folder with the container, and name it `/app`" For the sake of this example, let's assume there is a file called `app.py` inside of the `/app` folder with our code in it.
- `WORKDIR /app`: "Go inside the `/app` directory"
- `CMD [ "python", "app.py" ]`: "Run the command `python app.py`" (This will launch the python application)

Once all these steps are run, Docker will take a 'snapshot' of this (the Docker image), and save it locally. This Docker image will now be used as the 'mother' of all Docker instances. 
Now, we can create an instance of that image (using the `docker run` command): once we tell it to run, Docker will take this image, make a copy, and run it from the point it was saved. The magic of this is that this process is nearly instantaneous: the python application starts running nearly instantaneously after we run the command! 
With this, if the image reaches an error or gets corrupted, no problem: we Launch another! It will start from the initial point we saved it and run normally! (Here is where Kubernetes comes in: it orchestrates Docker instances).