# Flask

This document is organised as follows:

**[1 - Intuitive introduction to Flask](#1---introduction-to-oop)**

**[2 - Building web applications with Flask](#2---building-web-applications-with-flask)**
- [2.1 Creating a Flask application](#21-installing-flask)
- [2.2 Creating a Flask application](#22-creating-the-flask-application)
- [2.3 Routing requests, sending responses](#23-routing-requests-sending-responses)

**[3 - Running the application]()** (To be done)

# 1 - Intuitive introduction to Flask

## What is `Flask`?
`Flask` is a Python Library that allows it to listen to client's requests and prepare back responses (recall how a server works [here](../../0-basic-concepts/README.md#22-http-protocol)). It is the main library that allows to build the backend of a server with Python. 

As any library, it imports Classes (review what a Python class is [here](2-oop-with-python.md)) and functions, which enable certain functionalities to make this work.

## What is a server backend?
The backend is the "logic" of a web application. Some applications do not require backend: for example, most classic personal web pages simply require a static display of a series of screens; these are run directly on the browser with a simple logic such as: "If the user clicks this button, display screen A, otherwise display screen B"; screen A and B are always the same (for example, the CV or the portfolio of that person). That simple logic can be run directly in the browser, or the frontend.
Other more complex web applications, such as for example Amazon, need to do fancier stuff: they tailor products displayed in the home page to the user, they get and store information such as items added in the shopcart (which need to be remembered the next time the user enters the page), store the items purchased by the user so it can recommend more... Lots of things! All this complex logic that requires user input, data storage or heavy weight machine learning algorithms needs to be run in a server somewhere: that is the backend. The backend is the "core" of web applications, where all fancy stuff happens. And it needs to happen away from the user (nowadays it runs mostly on the cloud), so the data is stored securely, and the computations are done efficiently, so the user has the desired experience.

## What are the main functionalities that Flask brings?
Now that we know what a backend is, we can talk of what `flask` allows Python to do. Python on its own is a "scripting" language, that means that it can be used to run "series of tasks" in a linear way: the program starts, performs some computations (such as reading a file, computing some results, and writing them on another file), and then it stops.

`Flask` brings a simple but key component that will allow Python to become a server: and that is an "event listener". The event listener is an object that will continuously listen to client requests. Recalling from the [introduction](../../0-basic-concepts/README.md#22-http-protocol), at any point in time, servers should be able to handle any request sent by the client (remember a request is a combination of a **URL**  and an **HTTP method**, amongst other data), and it should formulate a response. The event listener brings those functionalities. Under the covers, it works as an infinite loop continuously checking if any request has arrived. Once a request is heared, it will execute the function that triggers the response. 

Once a request is heared by the event listener, it will execute the function in the code that triggers the response: that functionality (called "routing") is also brought by `flask`. Routing means that according to the type of request, our server should be able to trigger the right function (that we will code), so that our server prepares the correct response.
>For example: if a user wants to see all the available products, he will do a `"GET"` request to the `"/products"` URL of our server. In that case, we want our server to query the right table on the database, retrieve the data, and send to the client a list of the currently available products (which will then be sent to the browser and rendered in a nice way for the user to see it). This latter part will be coded by us (the developers), while flask will enable us to do it with a very simple syntax.

This is what Flask does for us, it allows to tell Python "keep on listening to requests" and "execute this function if this URL is hit with this HTTP method". As easy as that: let's see how the syntax works for Flask.

# 2 - Building web applications with Flask
## 2.1 Installing `flask`
In order to run flask, first we need to install the library. For that, once Python is installed in our machine, we must run (in the terminal if we want it locally, or in the `Vagrantfile` or `Dockerfile`): `pip install flask`. That will download a bunch of files with Classes and functions that we will use in our code.

## 2.2 Creating the flask application
A flask application is simply an "event listener": an object that will tell Python to never stop (unless told so) listening to requests and processing responses.

### 2.2.1 Creating the `app.py` file
We first create the base flask file, in which the `app` object will be created. To do so, we open our favourite text editor and create brand new file called: `my_app.py` (for example).
> Note: naming the file `my_app.py` is arbitrary. The file can be named as we want: in some examples in the course, the `app` object is created in the `__init__.py` file (which is a special file in Python that allows to execute Python files inside sub-folder of the project, otherwise Python ignores those files).
> Note 2: Naming the main app object `app` is a convention: it is an object, so it can be called any name we want. To make our code readable, however, it is good practice to name it simply `app` (so that others understand it).

### 2.2.2 Importing Flask
Flask is a library, which is simply a set of Python files with a bunch of Classes (remember: classes are "blueprints" from which to create objects) and functions already programmed so that we can use them in our code. In order to use those files, we want to specify **which specific file**, and **which specific class or function** we want to use in our current file. For performance, we do not want to import things we are not using. 

To import the main functionality of flask (the creation of a `Flask` object), we use:
```python
from flask import Flask
```
- This code imports the `Flask` class (which creates an event listener), from the `flask` library (which is a file we downloaded when we ran `pip install flask`).

### 2.2.3 Creating the `app` object
The app object, which will listen to all server requests and then trigger responses cane created with this simple code:
```python
app = Flask(__name__)
```
- creates a `Flask` object named `app` that constantly listens to server requests.
> Note: the `__name__` variable is a special variable in Python that always holds the name of the file that executed it. In this example, since the `my_app.py` file is the one that contains `__name__`, then `__name__` will be equal to `"my_app"` (careful: `"my_app"` is a string, and has nothing to do with the `app` object we just created). It allows Flask to store the location where the `app` object is created.

That's it! With these few lines of code, our Python script is now capable of listening to server requests!

## 2.3 Routing requests, sending responses
The `app` object of the flask library allows us to route requests and prepare responses very easily. We do that using a decorator.

### What is a decorator?
A decorator is a special function in python that allows us to define a specific functionality, and adding it into another function. Flask adds the functionality of routing responses using the decorator `@app.route()`. 
It works the following way:
- we define a function in our code, that (for example), returns some nice HTML that renders "Welcome to the home page!" (we can use any arbitrary name, but it is good practice to use a name that describes what the function does; let's choose `home_page()`).
- on top of that function, as a decorator, we add `@app.route("/")`. This decorator is defined by flask and adds the following functionality to the function we just defined: "everytime a user hits the "/" URL (which is the "home" URL), execute that function". 

That's it! Now the function we defined gets executed only when the user triggers some action, with only one additional line of code! That is the magic of Flask. Let's see all the pieces together.

### 2.3.1 Creating the home route
```python
@app.route("/", methods = ["GET"])
def home_page():
    return "<h1>Home Page</h1>"
```
- we define the `home_page` function which returns some basic HTML code (which will be rendered nicely by the browser), and added the decorator provided by flask that tells this function to be executed every time the user hits the home page with a `GET` request (which is the default initially).