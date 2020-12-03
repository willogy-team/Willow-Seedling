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

- Control program.
- Arrange code
- Easy to understand and modify
- Lend itself more to use.

### Keywords

#### Class

A `class` is a blueprint for the object.

Define an empty class `Vehicle`:
```
class Vehicle:
    
    pass
```

#### Object (Instance)

An object is an instantiation of a `class`. When class is defined, only the description for the object is defined. 
```
obj = Vehicle()
# obj is an object of class Vehicle
```

#### Method

Methods are functions (`def`), defined inside the body of a `class,`that are used to define the behaviors of an object.

(E.g. )
```
class Vehicle:
    
    # instance attributes
    def __init__(self, name, color):
        self.name = name
        self.color = color
    
    # instance method
    def get_info(self):
        return f"The {self.name} is {self.color}";
        
 # instantiate the object
 car = Vehicle("car", "red")
 
 # call the instance method
 print(car.get_info())
    
```
(Output.)
```
The car is red
```

#### Inheritance

Inheritance is a way of creating a new class for using details of an existing class without modifying it. The newly formed class is a derived class (or child class). Similarly, the existing class is a base class (or parent class).
```
# parent class
class Vehicle:
    ...
    
# child class
class Car(Vehicle):
    ...
```

#### Encapsulation
We can restrict access to methods and variables. This prevents data from direct modification which is called encapsulation. In Python, we denote private attributes using underscore as the prefix i.e `_`(single) or `__`(double).

```
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
(E.g.)
```
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
(Output.)
```
The car vehicle is red
The hat thing is black
```

# References
- OOP in Python, [tutorial 1](https://python-textbok.readthedocs.io/en/1.0/Object_Oriented_Programming.html), [tutorial 2](https://realpython.com/python3-object-oriented-programming/)
- [Python Design Patterns: For Sleek And Fashionable Code](https://www.toptal.com/python/python-design-patterns), Andrei Boyanov
- [Advanced Python: 9 Best Practices to Apply When You Define Classes](https://medium.com/better-programming/advanced-python-9-best-practices-to-apply-when-you-define-classes-871a27af658b), Yong Cui.
