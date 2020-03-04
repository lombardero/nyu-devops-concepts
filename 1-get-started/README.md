# GET STARTED: BASIC DEVELOPMENT TOOLS

These are some of the tools you will require for the Course's assignment.

# 1 Text editor
A key component to start programming is a good text editor. The text editor is the tool you will use to write all your lines of code, visualize them, check them in real time, and integrate them; where you might spend many hours trying to find the reasons why your code does not behave as you planned. And that is why you need the best editor you can find. Here is a recommendation: `VS Code` (although you can use any one you want).

## 1.1 - VS Code (Recommendation)
Visual Studio Code is Microsoft's text editor. Its main killer features are:
- Super-easy integration with any programming language or library (as the ones used on the course: `python`, `ruby`, `vagrant`, `docker` and many others), which can be searched and downloaded on the program itself, and enables syntax checking, amazing visual coding and debugging features
- A super useful shell command `code` that allows you to open any file directly into `VS Code` running `code <filename>`.
- An amazing debugging system, allowing to 'pause' the running code at any line and check the contents of variables by hovering over them
- Easy navigation though package function definitions and variables
- AI-enabled syntax propositions for `Python`, `Javascript`, and `Java`

Download VS Code for free on its official page [here](https://code.visualstudio.com/).

### 1.1.0 - Setting up VS Code
#### Adding the  `code` command on a Mac
After `VS Code` has been installed, you can install the `code` shortcut by following the below steps (or check the [Official VS Code documentation about it](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line)):
- Launch `VS Code`
- Press `F1` to open the command palette, and type 'shell command' to find the `Shell Command: Install 'code' command in PATH` command; run it
- Restart your terminal

You can now run `code <filename>` command to open files with VS Code directly!

#### General set up links
Official `VS Code` [guide for Windows in this link](https://code.visualstudio.com/docs/setup/windows).

Official `VS Code` [guide for mac in this link](https://code.visualstudio.com/docs/setup/windows).

### 1.1.1 - Some useful commands in VS Code
- `Ctrl + Space`: gives you the list of possible statements (such as available arguments of functions). Requires having the extension of the language you are working on installed (check below paragraph).
- `Alt + Shift + F`: reformats the code with the proper spacings (not useful for `Python`)

### 1.1.2 - Useful `VS Code` extensions
Extensions enhance the capabilities of `VS Code`: spelling corrections, code navigation (see what's inside objects), and AI-enabled suggestions. Check the [official extension tutorial here](https://code.visualstudio.com/docs/editor/extension-gallery). 

You can search for extensions clicking the 'extensions' button (the one that looks like a tiny window), on the left vertical bar. Here are some useful extensions that we will use on the course:
- Programming languages: the `python`, and `vagrant` extensions should be added to VS Code for this course to edit our code (`python` for our project, `ruby` for our vagrantfile)
- `GitLens`: this extension will let you know who wrote any line of code in the project when clicked

You can find a useful VS Code tutorial for using `Flask` in this [link](https://code.visualstudio.com/docs/python/tutorial-flask).

### 1.1.3 - Debugging useful tools
Find out how to use VS Code's debugger [here](https://code.visualstudio.com/docs/python/python-tutorial#_configure-and-run-the-debugger).

Find out about `Python`-specific features for debugging using VS Code on [this official guide](https://code.visualstudio.com/docs/python/debugging).

Go to `Debug > Start debugging` to start the debugging tool (we need to choose an environment - such as `Python`):
- Create 'break points' (by selecting critical lines of our code - a red dot should appear in the left side), that will allow us to check the status of our code (the contents of each variable by hovering around with the mouse, for example) just before that line is executed. (once we run the code, the red dot should appear with a yellow mark -> that means the line 'break point' selected is about to be executed).
- A 'play bar' will appear on top of the screen, allowing us to move from break point to break point (using the play button), from line to line (using the 'jump' arrow), and enter the 'layers' of our code (we can access the source code when we call a in-built function using the 'down' arrow, and go back to the top layer with the 'up' arrow of the play bar)
- Check the output of operations in real time ('what would happen if I run this code differently') using the Debug Console (can be used, for example, to 'execute' variables at each point of the code to see what is inside of the variables).

Go to `View > Debug` to access many features of VS Code Debug mode:
- Clicking on the `Variables` tab on the left menu of the screen allows us to check all defined variables of our code, and its contents in real time. It can be used (by double-clicking) to modify the values stored on the variables.
- We can define 'watchers' (also on the left menu of the screen), which will monitor the contents of a specific variable in real time through the code.

# 2 Terminal
The terminal (also called 'shell', 'console' or 'command line') is the second most important tool of a developer. Terminals enable complete control over a machine through command line statements, which allow us to run programs, install packages and access core functionalities of our machine. 

In this course, we will use the terminal to install packages, run virtual machines and access them. Once inside of the virtual machines, we the terminal will allow us to read the logs of our service, edit it and debug it.

Access to terminals in different devices:
- On **Mac**, you can run your terminal by searching for `Terminal` in the Apps tab, or go to `Dock > Launch Pad > Other > Terminal`.
- On **Windows**, go to `Start > Command Prompt`, or search for `cmd` on the Windows search tab.
- On **VS Code**, a built-in terminal (opened on the current folder where your Workspace is) can be launched by clicking `Terminal > New Terminal` on the top menu.
- Alternatively, 3rd party command prompt applications can be installed.

## Windows users: installing `git bash` command prompt
`Git bash` is an application for Windows that allows to run the `git` commands (such as the ones on the [`git` cheatsheet](../3-git/1-complete-cheatsheet.md)). It is not required for Mac since `git` commands are installed by default.

Official link for downloading `Git Bash` [here](https://gitforwindows.org/).


# 3 Postman
Postman is a very useful debugging tool to check any kind of client request to our server. Check what a 'server request' is [on this document](../0-basic-concepts/README.md#22-http-protocol).

Download postman on the follwoing [link](https://www.getpostman.com/).

Postman is a testing tool for servers; it wil allow us to send any request to our server and see how it reacts to it. To make it work we simply need to start our server locally. Once the server is running (errors should be printed out in our terminal for easy debugging), we can start sending client requests.

The things we should pay attention to are:
- The request type (`GET`, `PUT`, `POST`, `DELETE`...), on the left side of the top URL navigation bar
- The URL navigation bar, where we can set up the URL we wish to visit (such as `localhost:5000`)
- The Header of our request (should be set to `application/json` if we are sending a `json` format)
- The Body (the data we wish to send to the server, usually in `json` format) of our request

We can, for example, start by doing an initial `GET` request to the base URL: `localhost:5000`, for example (if we are running our application on port `5000`) to check if the home page is working correctly. 
