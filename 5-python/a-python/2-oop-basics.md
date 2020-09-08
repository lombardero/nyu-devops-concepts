# Object Oriented Programming Basics

This file contains the basics of Object Oriented programming: some intuition about it,
and how to define a Class. For more advanced topics check the
[Advanced OOP python]()
section.

This document is organised as follows:

**[1 - Intuitive introduction to Object-Oriented Programming](#1---introduction-to-oop)**

**[2 - Objects and Classes in Python](#2---oop-with-python)**
- [2.1 Defining and instantiating classes](#21---classes-in-python)
- [2.2 Defining class methods](#22---defining-class-methods)
- [2.3 Inheriting from classes](#23---class-inheritance)


# 1 - Introduction to OOP

## What is OOP?

Object-oriented programming (OOP) is a programming paradigm that allows programmers
to encapsulate the business logic of applications in 'objects'. 

As opposed to lower-level programming languages in which programmers have to focus on
the pure logic of the code, OOP works with a higher level of abstraction, and focuses
on the logical interaction of the code components (which are grouped in 'objects'). It
allows us to build much more complex systems in a much simpler and structured way.

## But wait, what is an 'object'?

Objects are abstract entities defined by programmers. Conceptually, an object is a group
of functions and variables packaged together in an entity; the way objects are defined
in the code depends entirely on the programmer: the possibilities are endless.

> Let's illustrate it with an example: Imagine we have to deal with the backend of a
> pet shop. Amongst many things, the Pet shop needs to store the data of Pets. Each
> Pet has a name, a type, a breed, and a date of birth; each pet can also be adopted,
> or brought to the pet store for the first time. 
> In OOP, we can create a `Pet` object, which will have the variables `name`, `type`,
> `breed`, and `date_of_birth` associated to it. More importantly, we can define within
> the `Pet` object the functions `add_to_database` and `adopt`. The first adds the Pet
> to the database while the second removes it from the main database and adds it to an
> 'adopted Pets' database. The idea is to hide the complexity of the code in such a way
> that the statement `Pet.add_to_database()` performs always the desired action no
> matter the changes to the function we make (such as, for example, changing the type
> of database). That is OOP: the complexity is now encapsulated in the object itself,
> which makes the code much easier to maintain.

## Organising files in OOP

Files are typically used with the MVC (or Model-View-Controller) design pattern. In a
nutshell, the model divides the logic of the code in three parts:
- The `Models` file contains all the object definitions of the code; it is the backbone
  of the application. Objects hold all the complexity of the system, such as the way it
  talks to the database.  In this part we also define the logic the application will
  follow, since we will define the actions each object will be capable of doing.
- The `Contoller` defines the events that trigger the use of certain functionalities.
  In a typical server, the controller will define the actions to be taken once it knows
  the **URL** and **HTTP request** of a client's request. The controller should use the
  methods defined in the `Models` file, in such a way that if any of the models changes
  its implementation, the controller should still work.
- The `View` is the code (usually in a renderizable format such as HTML) that the client
  will see and interact with. Both controller and model will be able to update the view
  (based on what the user does such as clicking a button or sending information, for
  example), which will then be rendered to the user by the browser.

# 2 - OOP with Python

## 2.0 - Introduction: everything is an object

You heard well: in Python, everything is an 'object', or rather, using a more pythonic
language: everything is an instance from a Class, even Classes themselves!

In Python, a **Class** is a template that allows to create instances, all of which have
the same types of attributes and functions attached to it. It can be seen as a template
which defines the structure of the data required to create an instance.
- An **Instance of a Class** is a set of data that follows the Class blueprint
  (its structure) to allocate some memory to store an object (also called 'Class
  instance'). These objects will have some functionalities, which will be defined in the
  class.
> Example: Lists, Integers and Dictionnaries are Classes in Python. More specifically,
> a `List` has a method `pop()` attached to it, which will return the object contained
> in the last index.

Classes are key in Python: they are the building blocks of complexity: once we
them, we can do almost anything.

## 2.1 - Classes in Python

### 2.1.1 Defining a Class

Remember: when we define a class, we are defining the inner structure that its
instantiations will have: what types of data it will hold? which functions will be
allowed? Creating an instance is simply using that 'building block' to initiate an
object following that structure.

#### Creating a Class

Classes in Python are defined using the `class` keyword. Classes expect methods,
which will be attached to the class using the right indentation. See the below
example:

```python
class MyClass:
    def my_method(self, attribute):
        self.my_attribute = attribute
```
- The class above contains a method called `my_method`, which accepts two arguments.
  The first is the class instance (always named `self` by convention in instance
  methods), the second is an additional one provided as an example. Then, the method
  sets an instance attribute to the argument added (this is called a "setter method").

Now that this class has been created, we can instantiate it as follows:
```python
# Creating the class.
my_instance = Myclass()

# Using the method defined in the class.
my_instance.my_method("example_attribute")
```
- The code above creates a `MyClass` instance, then uses the method defined within
  it to perform some action. In this case, `self` is the instance itself
  (`my_instance`), then, a second argument is explicitely passed in the method.

> Note: by convention, Class names are in `CamelCase`, and methods and arguments in
> `slug_format`

#### The class constructor: the `__init__` method

`__init__` is a "magic method" in Python: rather than explicitely, it will be called
under certain circumstances. In the case of `__init__`, it will be automatically
executed every time an instance of a Class is created. In other languages
it is known as the "constructor" function, as it will define the actions the Class
should perform at startup (usually, it contains the logic of setting up some useful
attributes that will be used within the class).

Here is an example that illustrate how it works:
```python
class Person:
    def __init__(self, complete_name):
        self.first_name = complete_name.split()[0]
        self.last_name = complete_name.split()[1]
```
- In the code above, we have created a class named `Person`, with a mandatory input
  variable: `complete_name` (needs to be provided when the class is created). The
  class, however, will save in memory the values of `first_name` and `last_name` as
  two separate variables internally.


Let's take a closer look at what each line of code is doing:
- `class Person:` defines the class (creates a pointer to the name). That way, every
  time we run `Person(complete_name)` we will create an instance of that class.
- `def __init__(self, complete_name):` defines the `__init__` function, which, as
  mentioned before, is a 'special' function in python that will be automatically
  executed when the class is instantated. It allows us to bind the variables
  defined within the function with that instance (in this example, it will be
  `first_name` and `last_name`). Note that all arguments entered on `__init__`
  (apart from `self`) are the required arguments for that class to initiate.
- `self.first_name = complete_name.split()[0]` will create a variable associated
  to the instance. From now on, we can run `<instance-name>.first_name` to return
  the value that is saved in it. In this example, it will be the first name of the
  person.

> Note: `self` the name given by convention to the first argument of instance methods,
> which mean 'the instance of the class itself' (which is passed as an argument to the
> method). It is a pretty ubiquitous argument in Python.

### 2.1.2 Defining a class instance

Once a Class is defined, we can use the template of that Class to create instances
with the same structure. Let's create two instances of the `Person` class defined
before:

```python
person1 = Person('Paul McCartney')
person2 = Person('John Lennon')
```
- The code above creates two instances of the class, and saves their variables in
  memory.

The arguments are now accessible:
- `person1.first_name` will return `'Paul'`
- `person2.last_name` will return `'Lennon'`

## 2.2 - Defining instance methods

Apart from `__init__` (which is not mandatory), we can define custom methods for the
class. These methods add functionalities to the Class, and can be called using the
statement `<instance-name>.method()`.

#### Example: `Rectangle`

Let's define a `Rectangle` class adding a method to it that returns the area of the
rectange:

```python
class Rectangle:

    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width
```
- The code above defines an `area` method that simply returns the area of the rectangle

#### Creating instances and calling the method

We can now create an instance of that Class:

```python
rectangle1 = Rectangle(3,4)
```

And then call the `area` method on it to compute its area:

```python
rectangle1.area()
```
- The code above will return `12` (as defined in the method definition), which is the
  area of the rectangle

