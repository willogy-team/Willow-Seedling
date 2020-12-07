# Introduction to OOP Programming & Design Patterns for Python

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Dec 1st, 2020 |
| **Topic(s)** | General Techniques |
| **Status**       | In Progress |

# Index
- [Object Oriented Programming]()
- [Design Patterns]()
- [OOP Best Practices]()

## Object-Oriented Programming

### Introduction

Different to procedural programming approach, which structures a program like a recipe in that it provides a set of steps, in the form of functions and code blocks, that flow sequentially in order to complete a task. Object-Oriented Programing(OOP) is a programming paradigm that provides a means of structuring programs so that properties and behaviors are bundled into individual objects. Put another way, object-oriented programming is an approach for modeling concrete, real-world things, like cars, as well as relations between things, like companies and employees, students and teachers, and so on.

### Motivation

- Data is safe and secure with data abstraction.
- Arrange code.
- Easy to understand and modify.
- Lend itself more to use, can be reused.

### Objects versus Classes

An object is simply a collection of data (variables) and methods (functions) that act on those data. Similarly, a `class` is a blueprint for that object.

We can think of `class` as a sketch (prototype) of a house. It contains all the details about the floors, doors, windows etc. Based on these descriptions we build the house. House is the object.

An object can be created from a `class`, is also called an instance of a `class` and the process of creating this object is called **instantiation**.

#### Defining a `class` in Python

Like function definitions begin with the `def` keyword in Python, class definitions begin with a `class` keyword.

(e.g.1) Create empty `Thing` class.
```python
class EmptyThing:
    ''' This is a docstring. The empty class'''
    pass
```

(e.g.2) Create `Thing` class with two attributes
```python
class Thing:
    ''' This is a thing class'''

    # constructor declaration
    def __init__(self, name, color):
        self.__name = name
        self.__color = color

    # instance method
    def get_info(self):
        return f"This object is a(n) {self.__color} {self.__name}."
```
#### Creating an object in Python

(e.g.3 on 1/2)
```python
obj1 = EmptyThing()
obj2 = Thing("car", "red")

objs = [obj1, obj2]
for obj in objs:
    print(obj, obj.__doc__)
```
(output.)
```
<__main__.EmptyThing object at 0x7f43fdc0ad30>  This is a docstring. The empty class
<__main__.Thing object at 0x7f43fdc0a400>  This is a thing class
```

#### Constructors in Python

From (e.g.2) the `__init__()` function gets called whenever a new object of that class is instantiated.

Defaultly, this special function is not defined then construct new object with no parameters (e.g.3 `obj1`). But, if you defined `__init__` function, you must create new instance with adequate parameters (e.g.3 `obj2`).


#### Deleting Attributes and Objects

(e.g.4 on 3)
```python
# delete attribute name in obj2
del obj2.name
# delte obj1
del obj
```

#### Destructor in Python

Automatically destroyed.

### Inheritance

Inheritance is a way of creating a new class for using details of an existing class without modifying it. The newly formed class is a derived class (or child class). Similarly, the existing class is a base class (or parent class).

#### Inheritance Syntax
```python
# parent class
class BaseClass:
    ...

# child class
class DerivedClass(BaseClass):
    ...
```
(e.g.5)
```python
class Thing:
    ''' This is a thing, base class'''

    # constructor declaration
    def __init__(self, name, color):
        self.__name = name
        self.__color = color

    # instance method
    def get_info(self):
        return f"This object is a(n) {self.__color} {self.__name}."


class Car(Thing):
    ''' This is a car, child class'''

    def __init__(self, name, color, brand):
        super().__init__(name, color) # call function from superclass
        self.__brand = brand

    def get_brand(self):
        return f"Brand: {self.__brand}"


car = Car("car", "red","Toyota")
print(car.get_info())
print(car.get_brand())
```
(output)
```
This object is a(n) red car.
Brand: Toyota
```
#### Method Overriding in Python
In (e.g.5) `__init__` method was defined in both classes `Thing` and `Car`. When this happens, the method in the derived class overrides that in the base class.

Two built-in functions `isinstance()` and `issubclass()` are used to check inheritances.

(e.g.6)
```python
lists = [Thing, Car, int, object]
print("Instance")
for obj in lists:
    print(isinstance(car, obj))
print("Subclass")
for obj in lists:
    print(issubclass(Car, obj))
```
(output.)
```
Instance
True
True
False
True
Subclass
True
True
False
True
```

### Multiple Inheritance

A `class` can be derived from more than one base class in Python, similar to C++. This is called multiple inheritance.

#### Multiple derived inheritance
```python
# parent classes
class Base1:
    ...
class Base2:
    ...
...

# child class
class MultiDerivedClass(Base1, Base2 [,...]):
    ...
```

#### Multilevel Inheritance
(e.g.7)
```python
class Base:
    pass

class Derived(Base):
    pass

class DouDerived(Derived):
    pass
```
#### Method Resolution Order in Python
(e.g.8 on 7)
```python
print(DouDerived.__mro__)
print(DoutDerived.mro())
```
(output.)
```
(<class '__main__.DouDerived'>, <class '__main__.Derived'>, <class '__main__.Base'>, <class 'object'>)
[<class '__main__.DouDerived'>, <class '__main__.Derived'>, <class '__main__.Base'>, <class 'object'>]
```
### Operator Overloading
Python operators work for built-in classes. These features in Python that allow the same operator to have different meaning according to the context are called operator overloading. Put another way, that is Pythonic.

(e.g.9)
```python
class Point:

    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    # convert Point to str
    def __str__(self) -> str:
        return f"({self.x}, {self.y})"

    # compute self + other
    def __add__(self, other) -> Point:
        x = self.x + other.x
        y = self.x + other.y
        return Point(x, y)


p1, p2 = Point(1, 2), Point(2,-5)
print(p1, " + ", p2, " = ", p1 + p2)
```
(output.)
```
(1, 2)  +  (2, -5)  =  (3, -4)
```
#### The special functions
|Operator|Expression|Internally|
|----|--|----|
|Addition|`p1 + p2`|`p1.__add__(p2)`|
|Subtraction|`p1 - p2`|`p1.__sub__(p2)`|
|Multiplication|`p1 * p2`|`p1.__mul__(p2)`|
|Power|`p1 ** p2`|`p1.__pow__(p2)`|
|Division|`p1 / p2`|`p1.__truediv__(p2)`|
|Floor Division|`p1 // p2`|`p1.__floordiv__(p2)`|
|Remainder (modulo)	|`p1 % p2`|`p1.__mod__(p2)`|
|Bitwise Left Shift	|`p1 << p2`|`p1.__lshift__(p2)`|
|Bitwise Right Shift	|`p1 >> p2`|`p1.__rshift__(p2)`|
|Bitwise AND	|`p1 & p2`|`p1.__and__(p2)`|
|Bitwise OR|`p1 \| p2`|`p1.__or__(p2)`|
|Bitwise XOR	|`p1 ^ p2`|`p1.__xor__(p2)`|
|Bitwise NOT	|`~p1`|`p1.__invert__()`|

#### Encapsulation
We can restrict access to methods and variables. This prevents data from direct modification which is called encapsulation. In Python, we denote private attributes using underscore as the prefix i.e `_`(single) or `__`(double).

(e.g.10)
```python
class Vehicle:

    def __init__(self, name, color):
        self._name = name
        self._color = color

    # use instance method to set/get attributes
    def set_name(self, name):
        self._name = name

    def set_color(self, color):
        self._color = color

    def get_name(self):
        return self._name

    def get_color(self):
        return self._color
```

#### Polymorphism

Polymorphism is an ability (in OOP) to use a common interface for multiple forms (data types).

(e.g.11)
```python
class Vehicle:

    def __init__(self, name, color):
        self._name = name
        self._color = color

    def get_info(self):
        return f"The {self._name} vehicle is {self._color}";
class Thing:
    def __init__(self, name, color):
        self._name = name
        self._color = color

    def get_info(self):
        return f"The {self._name} thing is {self._color}";

# common interface
class Interface:

    def get_info(obj):
        return obj.get_info()
# instantiate objs
car = Vehicle("car", "red")
hat = Thing("hat", "black")
list = [car, hat]
# passing the obj
for obj in list:
    print(Interface.get_info(obj))
```
(output.)
```
The car vehicle is red
The hat thing is black
```

## Design Patterns

### Introduction

In software engineering, a software design pattern is a general, reusable solution to a commonly occurring problem within a given context in software design. Everything starts with the Gang of Four (GOF). The patterns are not only microarchitectural models but also useful as a common design vocabulary among software engineers. The overall architecture of the system and related design decisions can be explained by giving a set of patterns used. While new patterns do emerge the GOF still remains as the definite reference on design patterns. For this reason it is important to introduce these patterns, the notions and the theory behind them and their applicability to Python community.

### Motivation

Design patterns are a common way of solving well known problems. With two principles which they believe would lead to good object-oriented software design:
- Program to an **interface**, not an **implementation**.
- Composition over inheritance: "Favor **object composition** over **class inheritance**".

The authors claim the following as advantages of interfaces over implementation:
- Clients remain unaware of the specific types of objects they use, as long as the object adheres to the interface
- Clients remain unaware of the classes that implement these objects; clients only know about the abstract class(es) defining the interface

To put it briefly Python is a weakly and dynamically typed interpreted language. Python objects is that they are not merely instances of their classes; their structures can change in runtime. It can be very difficult to understand and maintain.

### Patterns by Type

GOF is divided into three parts and each part describes the patterns related to the theme of the part. The themes describe the purpose of the patterns.
- **Creational** patterns address object instantiation issues.
- **Structural** patterns concentrate on object composition and their relations in the runtime object structures.
- Whereas the structural patterns describe the layout of the object system, the **behavioral** patterns focus on the internal dynamics and object interaction in the system.

#### Creational patterns
Creational patterns are ones that create objects, rather than having to instantiate objects directly. This gives the program more flexibility in deciding which objects need to be created for a given case.

| Pattern | Description |
|-------------|-------------|
|Factory Method|Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.|
|Abstract Factory| Lets you produce families of related objects without specifying their concrete classes. |
|Builder | Lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code. |
|Prototype |Lets you copy existing objects without making your code dependent on their classes. |
| Singleton |Lets you ensure that a class has only one instance, while providing a global access point to this instance.|

#### Structural patterns
Using inheritance to compose interfaces and define ways to compose objects to obtain new functionality.

| Pattern | Description |
|-------------|-------------|
|Adapter | Allows objects with incompatible interfaces to collaborate.|
|Bridge | Lets you split a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently of each other.|
| Composite |Lets you compose objects into tree structures and then work with these structures as if they were individual objects.|
|Decorator |Lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.|
|Facade|Provides a simplified interface to a library, a framework, or any other complex set of classes.|
|Flyweight |Lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.|
|Proxy|Lets you provide a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.|
#### Behavioral patterns
Behavioral patterns are concerned with communication between objects.

| Pattern | Description |
|-------------|-------------|
|Chain of Responsibility|Lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.|
|Command|Turns a request into a stand-alone object that contains all information about the request. This transformation lets you parameterize methods with different requests, delay or queue a request's execution, and support undoable operations.|
|Iterator|Lets you traverse elements of a collection without exposing its underlying representation (list, stack, tree, etc.).|
|Mediator|Lets you reduce chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object.|
|Memento|Lets you save and restore the previous state of an object without revealing the details of its implementation.|
|Observer|Lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they're observing.|
|State|Lets an object alter its behavior when its internal state changes. It appears as if the object changed its class.|
|Strategy|Lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.|
|Template Method|Defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.
|Visitor|Lets you separate algorithms from the objects on which they operate.|

## OOP Best Practices

### Good Names
You should give the class a pretty name. Although the only limit of your class name is the rules of a legal Python varible. There are recommended ways to give class names.
- Use nouns that are easy to pronounce.
- Reflect its stored data and intended functionalities.
- Flow naming conventions. Using upper-case camel style for class names, like PrettyClass.

### Explicit Instance Attributes
The best pratice is to place an instance' attributes in the `__init__` method, such that your code’s reader has a single place to get to know your class’s data structure, as shown below.

### Use Properties — But Parsimoniously
They’re used to creating getters and setters for attributes of the instances. This pattern can be mimicked with the use of the property decorator in Python.

(e.g.12)
- Property Decorator
```python
class Student:
    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    @property
    def name(self):
        print("Getter for the name")
        return f"{self.first_name} {self.last_name}"

    @name.setter
    def name(self, name):
        print("Setter for the name")
        self.first_name, self.last_name = name.split()
```

- Use Properties
```python
>>> student = Student("John", "Smith")
... print("Student name:", student.name)
... student.name = "Johnny Smith"
... print("After setting:",student.name)
Getter for the name
Student name: John Smith
Setter for the name
Getter for the name
After setting: Johnny Smith
```
### Define Meaningful String Representations
In Python, functions that have double underscores before and after the name are referred to as special or magic methods, and some people call them dunder methods, such as `__init__`, `__repr__` and `__str__`.
(e.g.13)
```python
class Student:

    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    def __repr__(self):
        return f"Student({self.first_name!r}, {self.last_name!r})"

    def __str__(self):
        return f"Student: {self.first_name} {self.last_name}"
```
(output.)
```python
>>> student = Student("David", "Johnson")
... student
Student('David', 'Johnson')
>>> print(student)
Student: David Johnson
```

### Instance, Class, and Static Methods
In a class, we can define three kinds of methods: instance, class, and static methods. You need to consider what methods you should use for the functionalities of concern.
- Instance methods: are concerned with individual instance objects, which have to have `self` argument in first parameter.
- `classmethod`s: are not concerned with individual instance objects, which allow you to access or update attributes related to the class.
- `staticmethod`s: are not concerned with individual instance objects, which are independent of any instance or the class itself.
(e.g.14)
```python
class Student:

    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    def begin_study(self):
        print(f"{self.first_name} {self.last_name} begins studying.")

    @classmethod
    def from_dict(cls, name_info):
        first_name = name_info['first_name']
        last_name = name_info['last_name']
        return cls(first_name, last_name)

    @staticmethod
    def show_duties():
        return "Study, Play, Sleep"
```

### Encapsulation Using Private Attributes
One important way to apply encapsulation is to prefix attributes and functions with an underscore or two underscores, as a convention.
- **protected** with an underscore: `_my_protected_attribute`.
- **private** with two underscrores: `__my_private_attribute`.

### Separate Concerns and Decoupling
You do not make cumbersome mixed functionalities into one class.
You should separate to concerns.

### Consider __slots__ For Optimization
The special attribute `__slots__` allows you to explicitly state which instance attributes you expect your object instances to have, with the expected results:
- faster attribute access.
- space savings in memory: storing value references in slots instead of `__dict`; denying `__dict__` and `__weakref__` creation if parent classes deny them and you declare `__slots__`.

### Documentation
Your class do not use unnecessary comments to compensate for bad code (i.e., meaningless variable names in this case).
You want to write docstrings for classes. Your responsibility as the programmer to make sure that you provide clear instructions on how to use your programs, which another people aren’t familiar with the relevant codebase.

# References
- OOP in Python, [tutorial 1](https://python-textbok.readthedocs.io/en/1.0/Object_Oriented_Programming.html), [tutorial 2](https://realpython.com/python3-object-oriented-programming/)
- [Python Design Patterns: For Sleek And Fashionable Code](https://www.toptal.com/python/python-design-patterns), Andrei Boyanov
- [The Catalog of Design Patterns in Python](https://refactoring.guru/design-patterns/python)
- [Advanced Python: 9 Best Practices to Apply When You Define Classes](https://medium.com/better-programming/advanced-python-9-best-practices-to-apply-when-you-define-classes-871a27af658b), Yong Cui.
