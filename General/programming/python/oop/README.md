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
```
class EmptyThing:
    ''' This is a docstring. The empty class'''
    pass
```

(e.g.2) Create `Thing` class with two attributes
```
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
```
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
```
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
```
# parent class
class BaseClass:
    ...
    
# child class
class DerivedClass(BaseClass):
    ...
```
(e.g.5)
```
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
```
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
```
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
```
class Base:
    pass

class Derived(Base):
    pass

class DouDerived(Derived):
    pass
```
#### Method Resolution Order in Python
(e.g.8 on 7)
```
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
```
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

(e.g.11)
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
(output.)
```
The car vehicle is red
The hat thing is black
```
# References
- OOP in Python, [tutorial 1](https://python-textbok.readthedocs.io/en/1.0/Object_Oriented_Programming.html), [tutorial 2](https://realpython.com/python3-object-oriented-programming/)
- [Python Design Patterns: For Sleek And Fashionable Code](https://www.toptal.com/python/python-design-patterns), Andrei Boyanov
- [Advanced Python: 9 Best Practices to Apply When You Define Classes](https://medium.com/better-programming/advanced-python-9-best-practices-to-apply-when-you-define-classes-871a27af658b), Yong Cui.
