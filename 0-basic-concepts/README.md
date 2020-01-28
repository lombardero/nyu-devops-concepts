# BASIC CS CONCEPTS FOR THE COURSE

This document contains an intuitive explanation of some elemental Computer Science concepts that are used in the course. It is intended as a 'live' document, completed each time a student has a doubt about a concept.

### Contents of the document
#### 1 - [Computing Basics](#1---computing-basics)
#### 2 - [Networking basics](#2--network-basics)

## 1 - Computing Basics
### The kernel
In a nutshell, the 'kernel' is the central software from a Unix system that manages and allocates computer resources (CPU, RAM, devices, etc.); it can be considered as the 'core of the Operating System'.

The kernel is responsible of the following tasks:
- Process scheduling: it decides how the multiple processes take use of the CPU of the machine.
- Memory management and isolation: the kernel also allocates memory for the running processes. Processes will request the kernel for data to be stored on the RAM, the kernel will allocate a physical spot on the memory, and keep a record of all used locations of the memory for every process; the kernel also ensures that the memory allocations are encapsulated (process A cannot modify any variable stored by process B; actually, it cannot even know the variables that process B has stored).
- Provision of a file system: a way of storing data on disk (allowin to create, retrieve, update, delete files).
- Creation and termination of processes: the kernel loads a new process into memory and provides the resources it needs (CPU, memory, access to files) once the process is run; once the process is terminated, the kernel ensures the resources used by it are freed again.
- Access to devices: the kernel manages the access to computer devices (keyboard, mouse, disks, etc.) by the running processes.
- Network: it sends and receives networking packets on behalf of the processes.


## 2 - Network Basics
### 2.1 IPs and Ports
#### IP addresses
An IP ('Internet Protocol') address is a unique identifyer of a 'node' on the internet graph (a point that can receive and send packets), composed of four 8-bit numbers. IPs are used to specify who should receive a specific chunk of data (or packet).
IPs can be public (a unique number, used to communicate with the web) or private (only accessible locally). An example of a private IP address is `127.0.0.1`, known as `localhost` by all machines. In the course, we will run our server on our local machine on IP `127.0.0.1`, which the browser can access when the IP address or its shortcut are visited.

#### Ports
The 'port' is simply a 16-bit number (which complements the IP address), to organize the type of data sent and received by a machine. Port numbers from 0 to 1023 are pre-assigned (by convention) to frequently used communications; for example, port `80` is used for the `HTTP` protocol (by default, browsers 'listen' to port 80 for data and ignore the rest), and port `22` is used for the `SSH` protocol. In this course, we will run applications, and direct their outputs into ports (which will be large numbers such as `8080` to avoid using a predefined number).

### 2.2 HTTP protocol
`HTTP` stands for 'Hypertext Transfer Protocol', which is used to send and receive data through the internet. HTTP codifies the messages sent by clients (the users) in a structured manner, so that the server can easily understand what the client is asking for, and send a response to it.

#### HTTP requests
[This file](https://github.com/lombardero/nyu-devops-concepts/tree/master/0-basic-concepts/request.json) contains an example of the request sent by Chrome while trying to reach the address `localhost:3000`. (I created a server in `localhost:3000` which simply logs the requests received; what you see is what the server printed).

As we can see, there is a lot of information in a request (a lot of empty fields), some private data (such as the Computer and browser used by the client), but most importantly, the URL (in the example provided, the URL is `'/'`, or the 'home' URL), and the HTTP Method (a `GET` request in the example, since the client is simply requesting the server to 'read' the `'/'` URL). 

Notes:
- Servers are structured using **URLs**, which will trigger different functions of the server. The home URL, usually `'/'`, will trigger a response (usually HTML) displaying the home page. Other URLs can be defined to do more complex actions to the server; in this course we will use the `REST API` convention for defining the URLs.
- **HTTP methods** are used as the second component for triggering different actions in the server (servers will need a method-URL pair to exactly know what to do). The typically used methods are `GET` (read data), `PUT` (update some data on the server), `POST` (send some data on the server to create a resource), and `DELETE` (delete some resource).

#### HTTP responses
Once the server has treated a request, it will send a response to the client; responses can have many forms, and are sent in a similar object as the request. The two main components of a  response is the **header** and the **body**.

The **header** contains information about the message itself; the minimum information required consists of two fields: 
- the `Content-Type`: which states the format used on the body of the message, so that the client can decode it. For example, setting `Content-Type` to `application/json` (on the header: `Content-Type: application/json`) will let the client know that the message sent back is in JSON format.
- the `Status`: which tells the client information about how the server handled the request. For example, `200 OK` tells the client the server properly understood the request, and sent it back. Find the entire list [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

The **body** is the message the server is sending to the client. It can have many formats: plain text, HTML, JSON... The browser will be the one who will render the response properly.

### 2.3 SSH
SSH stands for 'Secure Shell' protocol. It is an encrypted protocol (for security reasons) that allows a machine to take control over another machine. In the DevOps course, we will use the SSH protocol to control and run commands on the Virtual Machines we create with Vagrant.