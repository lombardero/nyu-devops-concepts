# GET STARTED: BASIC DEVELOPMENT TOOLS

## 1 Text editor
The first component required to be a killer programmer is a good text editor. The text editor is the tool you will use to write all your lines of code, visualize them, check them in real time, and integrate them. It is where you will spend hours trying to find that bug you are struggling to correct; your main tool as a programmer. And that is why you need the best editor you can find. Here are some recommendations.

### Recommendation A: VS Code
Visual Studio Code is Microsoft's text editor. Its main killer features are:
- Super-easy integration with any programming language or library (as the ones used on the course: `python`, `ruby`, `vagrant`, `docker` and many others), which can be searched and downloaded on the program itself, and enables syntax checking, amazing visual coding and debugging features
- An amazing debugging system, allowing to 'pause' the running code at any line and check the contents of variables by hovering over them
- Easy navigation though package function definitions and variables
- AI-enabled syntax propositions for `Python`, `Javascript`, and `Java`

Download VS Code for free on its official page [here](https://code.visualstudio.com/).

#### Some useful VS Code extensions:
- Programming languages: the `python`, `vagrant` and `ruby` extensions should be added to VS Code for this course to edit our code (`python` for our project, `ruby` for our vagrantfile)
- `GitLens`: this extension will let you know who wrote any line of code in the project when clicked

You can find a useful VS Code tutorial for using `Flask` in this [link](https://code.visualstudio.com/docs/python/tutorial-flask).

#### Some useful commands in VS Code
- `Ctrl + Space`: gives you the list of possible statements (such as available arguments of functions). Requires having the package of the language you are working on installed.
- `Alt + Shift + F`: reformats the code with the proper spacings (not useful for `Python`)

#### Debugging useful tools
Find out how to use VS Code's debugger [here](https://code.visualstudio.com/docs/python/python-tutorial#_configure-and-run-the-debugger).

Find out about `Python`-specific features for debugging using VS Code in this [link](https://code.visualstudio.com/docs/python/debugging).

Go to `Debug > Start debugging` to start the debugging tool (we need to choose an environment - such as `Python`).
- Create 'break points' (by selecting critical lines of our code - a red dot should appear in the left side), that will allow us to check the status of our code (the contents of each variable by hovering around with the mouse, for example) just before that line is executed. (once we run the code, the red dot should appear with a yellow mark -> that means the line 'break point' selected is about to be executed).
- A 'play bar' will appear on top of the screen, allowing us to move from break point to break point (using the play button), from line to line (using the 'jump' arrow), and enter the 'layers' of our code (we can access the source code when we call a in-built function using the 'down' arrow, and go back to the top layer with the 'up' arrow of the play bar)
- Check the output of operations in real time ('what would happen if I run this code differently') using the Debug Console (can be used, for example, to 'execute' variables at each point of the code to see what is inside of the variables).

Go to `View > Debug` to access many features of VS Code Debug mode:
- Clicking on the `Variables` tab on the left menu of the screen allows us to check all defined variables of our code, and its contents in real time. It can be used (by double-clicking) to modify the values stored on the variables.
- We can define 'watchers' (also on the left menu of the screen), which will monitor the contents of a specific variable in real time through the code.

## 2 Terminal
The terminal (also called 'shell', 'console' or 'command line') is the second most important tool of a developer. Terminals enable complete control over a machine through command line statements, which allow us to run programs, install packages and access core functionalities of our machine. 

In this course, we will use the terminal to install packages, run virtual machines and access them. Once inside of the virtual machines, we the terminal will allow us to read the logs of our service, edit it and debug it.

## 3 Postman
Postman is a very useful debugging tool to check any kind of client request to our server.

Download postman on the follwoing [link](https://www.getpostman.com/).

Postman will allow us to send any request we like to our server to see how it reacts to it. To make it work we simply need to start our server locally. Once the server is running (errors should be printed out in our terminal for easy debugging), we can start sending client requests.

The things we should pay attention to are:
- The request type (`GET`, `PUT`, `POST`, `DELETE`...), on the left side of the top URL navigation bar
- The URL navigation bar, where we can set up the URL we wish to visit (such as `localhost:5000`)
- The Header of our request (should be set to `application/json` if we are sending a `json` format)
- The Body (the data we wish to send to the server, usually in `json` format) of our request

We can, for example, start by doing an initial `GET` request to the base URL: `localhost:5000`, for example (if we are running our application on port `5000`) to check if the home page is working correctly. 
