# Object Oriented Programming with Python

This document is organised as follows:

**[1 - Intuitive introduction to Object-Oriented Programming](#1---introduction-to-oop)**

**[2 - Objects and Classes in Python](#2---oop-with-python)**
- [2.1 Defining and instantiating classes](#21---classes-in-python)
- [2.2 Defining class methods](#22---defining-class-methods)
- [2.3 Inheriting from classes](#23---class-inheritance)

# 1 - Introduction to OOP
## What is OOP?
Object-oriented programming (OOP) is a programming paradigm that allows programmers to encapsulate the business logic of applications in what we call 'objects'. 
As opposed to lower-level programming languages in which programmers have to focus on the pure logic of the code, OOP works with a higher level of abstraction, and focuses on the logical interaction of the code components (which are grouped in 'objects'). It allows us to build much more complex systems in a much simpler and structured way.

## But wait, what is an 'object'?
Objects are abstract entities defined by programmers. Conceptually, an object is a group of functions and variables packaged together in an entity; the way objects are defined in the code depends entirely on the programmer: the possibilities are endless. However, programmers should try to follow the logic of the application.

>Let's illustrate it with an example: Imagine we have to deal with the backend of a pet shop. Amongst many things, the Pet shop needs to store the data of Pets. Each Pet has a name, a type, a breed, and a date of birth; each pet can also be adopted, or brought to the pet store for the first time. 
>In OOP, we can create a `Pet` object, which will have the variables `name`, `type`, `breed`, and `date_of_birth` associated to it. More importantly, we can define within the `Pet` object the functions `add_to_database` and `adopt`. The first adds the Pet to the database while the second removes it from the main database and adds it to an 'adopted Pets' database. The idea is to hide the complexity of the code in such a way that the statement `Pet.add_to_database()` performs always the desired action no matter the changes to the function we make (such as, for example, changing the type of database). That is OOP: the complexity is now encapsulated in the object itself, which makes the code much easier to maintain.

## The 'Models' file
Objects are typically used with the MVC (or Model-View-Controller) design pattern. In a nutshell, the model divides the logic of the code in three parts:
- The `Models` file contains all the object definitions of the code; it is the backbone of the application. Objects hold all the complexity of the system, such as the way it talks to the database.  In this part we also define the logic the application will follow, since we will define the actions each object will be capable of doing.
- The `Contoller` defines the events that trigger the use of certain functionalities. In a typical server, the controller will define the actions to be taken once it knows the **URL** and **HTTP request** of a client's request. The controller should use the methods defined in the `Models` file, in such a way that if any of the models changes its implementation, the controller should still work.
- The `View` is the code (usually in a renderizable format such as HTML) that the client will see and interact with. Both controller and model will be able to update the view (based on what the user does such as clicking a button or sending information, for example), which will then be rendered to the user by the browser.

# 2 - OOP with Python
## 2.0 - Introduction
Understanding what Objects and Classes are in Python:
- A **Class** is a bundle of data of different types and functions; it can be seen as a template which defines the structure of the data required to create an object. 
- An **Object** is an instantiation of a Class; it uses the Class blueprint (its structure) to allocate some memory to store an object (also called 'Class instance'). These objects will have some functionalities, which will be defined in the class.
> Example: a data type `Array` is a Class, and the variable `a = [1,2,3]` is an object; we can call the method `a.pop()` and the last element of the array will be removed.

Classes are very important in Python: they are the building blocks of complexity in Python; once we understand classes, we can do almost anything. All libraries and packages built on top of Python are created by defining their own Classes which add functionalities.

## 2.1 - Classes in Python
### 2.1.1 Defining a Class
Remember: when we define a class, we are defining the inner structure that its instantiations will have: what types of data it will hold? which functions will be allowed? Creating an instance is simply using that 'building block' to initiate an object following that structure.

#### Initializing the Class with the `__init__` function

The only thing required by a Class to create an instance in Python, is for us to define the `__init__` function. `__init__` is a what we call a 'constructor' function, which is used to define the variables that will be attached to the Class. The constructor function takes as arguments all the required parameters that the Class needs to exist.

In Python, we define the Class name using the `class` keyword. Let's illustrate how it works through an example:
```python
class Person:
    def __init__(self, complete_name):
        self.first_name = complete_name.split()[0]
        self.last_name = complete_name.split()[1]
```
- In the code above, we have created a class named `Person`, with a mandatory input variable: `complete_name`. The class, however, will save in memory the values of `first_name` and `last_name` as two separate variables internally.

Let's look in more detail what each line of code is doing:
- `class Person:` defines the class (creates a pointer to the name), that way, every time we run `Person(complete_name)` we will create an instance of that class.
- `def __init__(self, complete_name):` defines the `__init__` function, which, as mentioned before, is a 'special' function in python: it will be automatically executed when the class is instantated. It allows us to bind the variables defined within the function with that instance (in this example, it will be `first_name` and `last_name`). Note that all arguments entered on `__init__` (apart from `self`) are the required arguments for that class to initiate.
- `self.first_name = complete_name.split()[0]` will initiate a variable associated to the class. From now on, we can run `<instance-name>.first_name` to return the value that is saved in it. In this example, it will be the first name of the person (since `complete_name.split()[0]` grabs the first part of a string separated by a space).

> Note: `self` is a keyword that means 'the instance of the class itself'. It is a pretty ubiquitous argument in OOP; `__init__` and other methods use it in order to bind elements such as variables to the instance. All methods used in a class require at least the `self` argument inside of it.

### 2.1.2 Defining a class instance
Once a Class is defined, we can use the template of that Class to create instances with the same structure. Let's create two instances of the `Person` class defined before:
```python
person1 = Person('Paul McCartney')
person2 = Person('John Lennon')
```
- The code above creates two instances of the class, and saves their variables in memory.

The arguments are now accessible:
- `person1.first_name` will return `'Paul'`
- `person2.last_name` will return `'Lennon'`

## 2.2 - Defining class methods
Apart from `__init__` function (which is always required), we can define custom methods for the class. These methods add functionalities to the Class, and can be called using the statement `<instance-name>.method()`.

#### Defining the class
Let's define a `Rectangle` class adding a method to it that returns the area of the rectange:
```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width
```
- The code defines a `area` method (which does not need any additional argument) that returns the area of the rectangle

#### Creating instances and calling the method
We can now create an instance of that Class:
```python
rectangle1 = Rectangle(3,4)
```

And then call the `area` method on it to compute its area:
```python
rectangle1.area()
```
- The code above will return `12` (as defined in the method definition), which is the area of the rectangle

## 2.3 - Class inheritance
Class inheritance is a very useful concept in OOP since it allows to reuse code, making it more readable and mantainable. Inheritance is used when we want to create an object with very similar functionalities as another; instead of re-coding an entire object from scratch, we use inheritance to create a 'copy' of the parent class (the class we inherit from), adding some functionalities to it

### 2.3.1 Defining 'child' classes
In order to create a new class ('child' class) based on another class, we need to use the `super()` function. See `super()`'s documentation [here](https://docs.python.org/2/library/functions.html#super).

Let's come back to our `Rectangle` class example. This will be our parent class:
```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * self.length + 2 * self.width
```
- The `Rectangle()` class is created, which requires two variables to instantiate itself `length`, and `width`, and has two methods.

Now, let's say we want to create a `Square` class with the same functionalities as `Rectangle`, but adding one restriction: `length` needs to be equal to `width`. We can create a `Square` class that inherits all the properties from `Rectangle`.

We can do so with the below syntax:
```python
class Square(Rectangle):
    def __init__(self, length):
        super(Square, self).__init__(self, length, length)
```
- The code above creates the new class `Square`, which requires a single argument as an input. `super()` will copy over the methods from `Rectangle` and make them available to `Square`; that process is called inheritance.

>Notes on the code above:
>- `class Square(Rectangle):`: we must add a pointer to the parent class for the child class to understand what class it is inheriting from
>- `def __init__(self, length):` initiates the `Square` class
>- `super(Square, self).__init__(self, length, length)`, copies the functionalities and executes the constructor of the parent class in the child class. From now on, all methods of the parent class are available to the child one. Note that `super()`(without arguments) would work as well, however it is good practice to include the pointers as we did above.

Now, if we define `a = Square(3)`, we can run `a.area()` and we will get `9`.

### 2.3.2 Checking if a class is parent of another
We can check easily if a class is a parent from another with the `issubclass()` function:
```python
issubclass(Class1, Class2)
```
- Will return `True` if `Class1` is a subclass (a 'child') of `Class2`. 

Example: `issubclass(Square, Rectangle)` will return `True` 
