# Coding convention for Python

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Nov 24th, 2020 |
| **Topic(s)** | General Techniques |
| **Status**       | In Progress |

# Index

## I. Introduction / Proposals / Benefits
We follow Google Python Style Guidle.<br/>
Python is the main dynamic language used at Google. This is a list of __dos__ and __don'ts__ for Python programs.

## II. Python Language Rules
### II.1. Lint
Run `pylint` over your code using this [pylintrc](https://google.github.io/styleguide/pylintrc)
It is a tool for finding bugs and style problems in Python source code. Because of the dynamic nature of Python, some warnings may be incorrect; however, spurious warnings should be fairly infrequent.

### II.2. Imports
Use ```import``` statements for packages and modules only, not for individual classes or functions.

- Use ```import y``` for importing packages and modules.
- Use ```from x import y``` where ```x``` is the package prefix and ```y``` is the module name with no prefix.
- Use ```from x import y as z``` if two modules named ```y``` are to be imported or if ```y``` is an inconveniently long name.
- Use ```import y as z``` only when ```z``` is a standard abbreviation (e.g., ```import numpy as np```)
- Do not use relative names in imports, use the full package name.

### II.3. Packages
Import each module using the full pathname location of the module.

Do should import each module by its full package name.<br/>
Yes:
```
import doctor.who import jodie
```
No:
```
import jodie
```

### II.4. Exception
Exceptions are allowed but must be used carefully.

Must follow certain conditions:
- Make use exceptions when it makes sense. 
- Never use catch-all ```except:``` statements, or catch ```Exception``` or ```StandardedError```
- Minimize the amount of code in a ```try```/```except``` block.
- Use the ```finally``` clause to excute code whether or not an exception is raised in the `try` block.

### II.5. Global variables
Avoid global variables.

Can use module-level constants: `MAX_VOLUME = 100`.<br/>
If needed, shoule use with prefix `_` to the name. 

### II.6. Nested/Local/Inner Classes and Functions
Nested local functions or classes are fine when used to close over a local variable. Inner classes are fine.
`updating`

### II.7. Comprehensions & Generator Expressions
Each portion must fit on one line: mapping expression, `for` clause, filter expression. Use loops instead when things get more complicated.<br/>
Yes:
```
    result = [mapping_expr for value in iterable if filter_expr]

    result = [{'key': value} for value in iterable
              if a_long_filter_expression(value)]

    result = [complicated_transform(x)
              for x in iterable if predicate(x)]
              
    result = []
    for x in range(10):
        for y in range(5):
            if x * y > 10:
                result.append((x, y))
```
No:
```
    result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]
```

### II.8. Default Iterators and Operators
Use default iterators and operators for types that support them, like lists, dictionaries, and files.<br/>
Yes: 
```
    for key in adict: ...
    if key not in adict: ...
    if obj in alist: ...
    for line in afile: ...
    for k, v in adict.items(): ...
    for k, v in six.iteritems(adict): ...
```
No:
```
No:   
    for key in adict.keys(): ...
    if not adict.has_key(key): ...
    for line in afile.readlines(): ...
    for k, v in dict.iteritems(): ...
```

### II.9. Generators
Use generators as needed.<br/>
Fine. Use “Yields:” rather than “Returns:” in the docstring for generator functions.

### II.10. Lambda Functions
Okay to use them for one-liners. If the code inside the lambda function is longer than 60-80 chars, it’s probably better to define it as a regular nested function.<br/>
Use the functions from the `operator` module instead of lambda functions

### II.11. Conditional Expressions
Each portion must fit on one line: true-expression, if-expression, else-expression. Use a complete if statement when things get more complicated.


### II.12. Default Argument Values
Do not use mutable objects as default values in the function or method definition.<br/>
Yes:
```
    def foo(a, b=None):
        if b is None:
            b = []
    def foo(a, b: Squence = ()): # Empty tuple OK since tuples are immutable
        ...
```
No:
```
    def foo(a, b=[]):
        ...
    def foo(a, b: Squence = {}):
        ...
    def foo(a, b=time.time()): 
        ...
```

### II.13. Properties
Use properties in new code to access or set data where you would normally have used simple, lightweight accessor or setter methods
Yes: 
```
     import math
     class Square:
         """A square with two properties: a writable area and a read-only perimeter.

         To use:
         >>> sq = Square(3)
         >>> sq.area
         9
         >>> sq.perimeter
         12
         >>> sq.area = 16
         >>> sq.side
         4
         >>> sq.perimeter
         16
         """

         def __init__(self, side):
             self.side = side

         @property
         def area(self):
             """Area of the square."""
             return self._get_area()

         @area.setter
         def area(self, area):
             return self._set_area(area)

         def _get_area(self):
             """Indirect accessor to calculate the 'area' property."""
             return self.side ** 2

         def _set_area(self, area):
             """Indirect setter to set the 'area' property."""
             self.side = math.sqrt(area)

         @property
         def perimeter(self):
             return self.side * 4
```

### II.14. True/False Evaluations
Use the “implicit” false if at all possible.<br/>
`0, None, [], {}, ''` all evaluate as false in a boolean context.<br/>
Use the “implicit” false if possible. But you should keep in mind:<br/>
- Always use `if foo is None:` or `is not None` to check for a `None` value.
- Never compare a boolean variable to `False` using `==`. Use `if not x:` instead.
- For sequences (strings, lists, tuples), use the fact that empty sequences are false, so `if seq:` and `if not seq:`.

Yes:
```
    if not users:
        print('no users')
    
    if foo == 0:
        self.handle_zero()
    
    if i % 10 == 0:
        self.handle_multiple_of_ten()
    
    def f(x=None):
        if x is None:
            x = []         
```
No:
```
    if len(users) == 0:
        print('no users')
    
    if foo is not None and not foo:
        self.handle_zero()
    
    if not i % 10:
        self.handle_multiple_of_ten()
    
    def f(x=None):
        x = x or []
```

### II.15. Deprecated Language Features
Use string methods instead of the `string` module where possible. Use function call syntax instead of `apply`. Use list comprehensions and `for` loops instead of `filter` and `map` when the function argument would have been an inlined lambda anyway. Use `for` loops instead of `reduce`.
Yes:
```
     words = foo.split(':')

     [x[1] for x in my_list if x[2] == 5]

     map(math.sqrt, data)    # Ok. No inlined lambda expression.

     fn(*args, **kwargs)
```
No: 
```
     words = string.split(foo, ':')

     map(lambda x: x[1], filter(lambda x: x[2] == 5, my_list))

     apply(fn, args, kwargs)
```

### II.16. Lexical Scoping
A nested Python function can refer to variables defined in enclosing functions, but cannot assign to them. Variable bindings are resolved using lexical scoping, that is, based on the static program text. Any assignment to a name in a block will cause Python to treat all references to that name as a local variable, even if the use precedes the assignment. If a global declaration occurs, the name is treated as a global variable.
```
def get_adder(summand1):
    """Returns a function that adds numbers to a given number."""
    def adder(summand2):
        return summand1 + summand2

    return adder
```

### II.17. Function and Method Decorators 
Decorators a.k.a the `@` notation. One common decorator is `@property`, used for converting ordinary methods into dynamically computed attributes. However, the decorator syntax allows for user-defined decorators as well. Specifically, for some function `my_decorator`, this:
```
class C:
    @my_decorator
    def method(self):
        # method body ...
```
is equivalent to:
```
class C:
    def method(self):
        # method body ...
    method = my_decorator(method)
```
Note: 
- Avoid external dependencies in the decorator itself (e.g. don't rely on files, sockets, database connections)
- Never use `staticmethod` unless forced to in order to integrate with an API defined in an existing library. Write a module level function instead.
- Use `classmethod` only when writing a named constructor or a class-specific routine that modifies necessary global state such as a process-wide cache.

### II.18. Threading
Do not rely on the atomicity of built-in types.

While Python’s built-in data types such as dictionaries appear to have atomic operations, there are corner cases where they aren’t atomic (e.g. if `__hash__` or `__eq__` are implemented as Python methods) and their atomicity should not be relied upon. Neither should you rely on atomic variable assignment (since this in turn depends on dictionaries).

Use the Queue module’s `Queue` data type as the preferred way to communicate data between threads. Otherwise, use the threading module and its locking primitives. Prefer condition variables and `threading.Condition` instead of using lower-level locks.

### II.19. Power Features
Avoid these features

### II.20. Modern Python: Python 3 and from __future__ imports
Use of `from __future__ import` statements is encouraged. All new code should contain the following and existing code should be updated to be compatible when possible:
```
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function
```

### II.21. Type Annotated Code
Type annotations (or “type hints”) are for function or method arguments and return values:
```
def func(a: int) -> List[int]:
```
You can also declare the type of a variable using similar PEP-526 syntax:
```
a: SomeType = some_func()
```
Or by using a type comment in code that must support legacy Python versions.
```
a = some_func()  # type: SomeType
```

## III. Python Style Rules
### III.1. Semicolons
Do not terminate your lines with semicolons, and do not use semicolons to put two statements on the same line.
```
    print('semicolons')    #YES
    
    print('semicolons');   #NO
```

### III.2. Line Length
Maximum line length is 80 characters.

Explicit exceptions to the 80 character limit:
- Long import statements.
- URLs, pathnames, or long flags in comments.
- Long string module level constants not containing whitespace that would be inconvenient to split across lines such as URLs or pathnames. 

When a literal string won’t fit on a single line, use parentheses for implicit line joining.
```
x = ('This will build a very long long '
     'long long long long long long string')
```

### III.3. Parentheses
Use parentheses sparingly.

It is fine, though not required, to use parentheses around tuples. Do not use them in return statements or conditional statements unless using parentheses for implied line continuation or to indicate a tuple.
```
Yes: if foo:
         bar()
     while x:
         x = bar()
     if x and y:
         bar()
     if not x:
         bar()
     # For a 1 item tuple the ()s are more visually obvious than the comma.
     onesie = (foo,)
     return foo
     return spam, beans
     return (spam, beans)
     for (x, y) in dict.items(): ...
```
```
No:  if (x):
         bar()
     if not(x):
         bar()
     return (foo)
```

### III.4. Indentation
Indent your code blocks with 4 spaces. Never use tabs or mix tabs and spaces.

### III.5. Blank Lines
Two blank lines between top-level definitions, be they function or class definitions. One blank line between method definitions and between the `class` line and the first method. No blank line following a `def` line. Use single blank lines as you judge appropriate within functions or methods.
```
def function1():
    ...
    

def function2():
    ...
```
```
def class():

    def function1():
    ...
    
    def function2():
    ...
```

### III.6. Whitespace
Follow standard typographic rules for the use of spaces around punctuation.

- No whitespace inside parentheses, brackets or braces.
```
Yes: spam(ham[1], {eggs: 2}, [])
```
```
No:  spam( ham[ 1 ], { eggs: 2 }, [ ] )
```
- No whitespace before a comma, semicolon, or colon. Do use whitespace after a comma, semicolon, or colon, except at the end of the line.
```
Yes: if x == 4:
         print(x, y)
     x, y = y, x
```
```
No:  if x == 4 :
         print(x , y)
     x , y = y , x
```
- No whitespace before the open paren/bracket that starts an argument list, indexing or slicing.
```
Yes: spam(1)
Yes: dict['key'] = list[index]
```
```
No:  spam (1)
No:  dict ['key'] = list [index]
```
- Surround binary operators with a single space on either side for assignment (`=`), comparisons (`==, <, >, !=, <>, <=, >=, in, not in, is, is not`), and Booleans (`and, or, not`). Use your better judgment for the insertion of spaces around arithmetic operators (`+, -, *, /, //, %, **, @`).
```
Yes: x == 1

No:  x<1
```
- Never use spaces around `=` when passing keyword arguments or defining a default parameter value, with one exception: when a type annotation is present, do use spaces around the `=` for the default parameter value.
```
Yes: def complex(real, imag=0.0): return Magic(r=real, i=imag)
Yes: def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
```
```
No:  def complex(real, imag = 0.0): return Magic(r = real, i = imag)
No:  def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
```
- Don’t use spaces to vertically align tokens on consecutive lines, since it becomes a maintenance burden (applies to `:`, `#`, `=`, etc.):
```
Yes:
  foo = 1000  # comment
  long_name = 2  # comment that should not be aligned

  dictionary = {
      'foo': 1,
      'long_name': 2,
  }
```
```
No:
  foo       = 1000  # comment
  long_name = 2     # comment that should not be aligned

  dictionary = {
      'foo'      : 1,
      'long_name': 2,
  }
```

### III.7 Shebang Line
Most `.py` files do not need to start with a `#!` line. Start the main file of a program with `#!/usr/bin/python` with an optional single digit `2` or `3` suffix per PEP-394.

This line is used by the kernel to find the Python interpreter, but is ignored by Python when importing modules. It is only necessary on a file that will be executed directly.

### III.8 Comments and Docstrings
Be sure to use the right style for module, function, method docstrings and inline comments.
#### III.8.1 Docstrings
Python uses docstrings to document code. A docstring is a string that is the first statement in a package, module, class or function.
#### III.8.2 Modules
Every file should contain license boilerplate. Choose the appropriate boilerplate for the license used by the project (for example, Apache 2.0, BSD, LGPL, GPL)

Files should start with a docstring describing the contents and usage of the module.
```
"""A one line summary of the module or program, terminated by a period.

Leave one blank line.  The rest of this docstring should contain an
overall description of the module or program.  Optionally, it may also
contain a brief description of exported classes and functions and/or usage
examples.

  Typical usage example:

  foo = ClassFoo()
  bar = foo.FunctionBar()
"""
```
### III.8.3 Functions and Methods
A function must have a docstring, unless it meets all of the following criteria:
- not externally visible
- very short
- obvious

Certain aspects of a function should be documented in special sections, listed below. Each section begins with a heading line, which ends with a colon. All sections other than the heading should maintain a hanging indent of two or four spaces (be consistent within a file). These sections can be omitted in cases where the function’s name and signature are informative enough that it can be aptly described using a one-line docstring.

- Args:<br/>
    List each parameter by name. A description should follow the name, and be separated by a colon followed by either a space or newline. If the description is too long to fit on a single 80-character line, use a hanging indent of 2 or 4 spaces more than the parameter name (be consistent with the rest of the docstrings in the file). The description should include required type(s) if the code does not contain a corresponding type annotation. If a function accepts `*foo` (variable length argument lists) and/or `**bar` (arbitrary keyword arguments), they should be listed as `*foo` and `**bar`.
    
- Returns: (or Yields: for generators)<br/>
    Describe the type and semantics of the return value. If the function only returns None, this section is not required. It may also be omitted if the docstring starts with Returns or Yields (e.g. `"""Returns row from Bigtable as a tuple of strings."""`) and the opening sentence is sufficient to describe return value.
    
- Raises:<br/>
    List all exceptions that are relevant to the interface followed by a description. Use a similar exception name + colon + space or newline and hanging indent style as described in Args:. You should not document exceptions that get raised if the API specified in the docstring is violated (because this would paradoxically make behavior under violation of the API part of the API). 

```
def fetch_smalltable_rows(table_handle: smalltable.Table,
                          keys: Sequence[Union[bytes, str]],
                          require_all_keys: bool = False,
) -> Mapping[bytes, Tuple[str]]:
    """Fetches rows from a Smalltable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by table_handle.  String keys will be UTF-8 encoded.

    Args:
        table_handle: An open smalltable.Table instance.
        keys: A sequence of strings representing the key of each table
          row to fetch.  String keys will be UTF-8 encoded.
        require_all_keys: Optional; If require_all_keys is True only
          rows with values set for all keys will be returned.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {b'Serak': ('Rigel VII', 'Preparer'),
         b'Zim': ('Irk', 'Invader'),
         b'Lrrr': ('Omicron Persei 8', 'Emperor')}

        Returned keys are always bytes.  If a key from the keys argument is
        missing from the dictionary, then that row was not found in the
        table (and require_all_keys must have been False).

    Raises:
        IOError: An error occurred accessing the smalltable.
    """
```
### III.8.4 Classes
Classes should have a docstring below the class definition describing the class. If your class has public attributes, they should be documented here in an `Attributes` section and follow the same formatting as a function’s `Args` section.
```
class SampleClass:
    """Summary of class here.

    Longer class information....
    Longer class information....

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```

### III.8.5 Block and Inline Comments
The final place to have comments is in tricky parts of the code. If you’re going to have to explain it at the next code review, you should comment it now. Complicated operations get a few lines of comments before the operations commence. Non-obvious ones get comments at the end of the line.
```
# We use a weighted dictionary search to find out where i is in
# the array.  We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:  # True if i is 0 or a power of 2.
```
To improve legibility, these comments should start at least 2 spaces away from the code with the comment character #, followed by at least one space before the text of the comment itself.

On the other hand, never describe the code. Assume the person reading the code knows Python (though not what you’re trying to do) better than you do.
```
# BAD COMMENT: Now go through the b array and make sure whenever i occurs
# the next element is i+1
```
### III.8.6 Punctuation, Spelling, and Grammar

### III.9 Classes
Classes need not explicitly inherit from `object` (unless for compatibility with Python 2).
```
Modern:
     class SampleClass:
         pass


     class OuterClass:

         class InnerClass:
             pass

```
```
Ancient:
    class SampleClass(object):
        pass


    class OuterClass(object):

        class InnerClass(object):
            pass
```
### III.10 Strings
Use the `format` method or the `%` operator for formatting strings, even when the parameters are all strings. Use your best judgment to decide between `+` and `%` (or `format`) though.
```
Yes: x = a + b
     x = '%s, %s!' % (imperative, expletive)
     x = '{}, {}'.format(first, second)
     x = 'name: %s; score: %d' % (name, n)
     x = 'name: {}; score: {}'.format(name, n)
     x = f'name: {name}; score: {n}'  # Python 3.6+
```
```
No: x = '%s%s' % (a, b)  # use + in this case
    x = '{}{}'.format(a, b)  # use + in this case
    x = first + ', ' + second
    x = 'name: ' + name + '; score: ' + str(n)
```
Avoid using the `+` and `+=` operators to accumulate a string within a loop. Since strings are immutable, this creates unnecessary temporary objects and results in quadratic rather than linear running time. Instead, add each substring to a list and `''.join` the list after the loop terminates (or, write each substring to an `io.BytesIO` buffer).
```
Yes: items = ['<table>']
     for last_name, first_name in employee_list:
         items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
     items.append('</table>')
     employee_table = ''.join(items)
```
```
No: employee_table = '<table>'
    for last_name, first_name in employee_list:
        employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
    employee_table += '</table>'
```
Be consistent with your choice of string quote character within a file. Pick `'` or `"` and stick with it. It is okay to use the other quote character on a string to avoid the need to `\\` escape within the string.
```
Yes:
  Python('Why are you hiding your eyes?')
  Gollum("I'm scared of lint errors.")
  Narrator('"Good!" thought a happy Python reviewer.')
```
```
No:
  Python("Why are you hiding your eyes?")
  Gollum('The lint. It burns. It burns us.')
  Gollum("Always the great lint. Watching. Watching.")
```
Prefer `"""` for multi-line strings rather than `'''`. Projects may choose to use `'''` for all non-docstring multi-line strings if and only if they also use `'` for regular strings. Docstrings must use `"""` regardless.
### III.11 Files and Sockets
Explicitly close files and sockets when done with them.

Leaving files, sockets or other file-like objects open unnecessarily has many downsides:
- They may consume limited system resources, such as file descriptors. Code that deals with many such objects may exhaust those resources unnecessarily if they’re not returned to the system promptly after use.
- Holding files open may prevent other actions such as moving or deleting them.
- Files and sockets that are shared throughout a program may inadvertently be read from or written to after logically being closed. If they are actually closed, attempts to read or write from them will throw exceptions, making the problem known sooner.

Furthermore, while files and sockets are automatically closed when the file object is destructed, tying the lifetime of the file object to the state of the file is poor practice:
- There are no guarantees as to when the runtime will actually run the file’s destructor. Different Python implementations use different memory management techniques, such as delayed garbage collection, which may increase the object’s lifetime arbitrarily and indefinitely.
- Unexpected references to the file, e.g. in globals or exception tracebacks, may keep it around longer than intended.

The preferred way to manage files is using the with statement:
```
with open("hello.txt") as hello_file:
    for line in hello_file:
        print(line)
```

### III.12 TODO Comments
Use `TODO` comments for code that is temporary, a short-term solution, or good-enough but not perfect.

A `TODO` comment begins with the string `TODO` in all caps and a parenthesized name, e-mail address, or other identifier of the person or issue with the best context about the problem. This is followed by an explanation of what there is to do.

The purpose is to have a consistent `TODO` format that can be searched to find out how to get more details. A `TODO` is not a commitment that the person referenced will fix the problem. Thus when you create a `TODO`, it is almost always your name that is given.
```
# TODO(kl@gmail.com): Use a "*" here for string repetition.
# TODO(Zeke) Change this to use relations.
```

### III.13 Imports formatting
Imports should be on separate lines; there are exceptions for typing imports.
```
Yes: import os
     import sys
     from typing import Mapping, Sequence
```
```
No:  import os, sys
```

Imports are always put at the top of the file, just after any module comments and docstrings and before module globals and constants. Imports should be grouped from most generic to least generic:
- Python future import statements. For example:
```
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function
```
- Python standard library imports. For example:
```
import sys
```
- third-party module or package imports. For example:
```
import tensorflow as tf
```
- Code repository sub-package imports. For example:
```
from otherproject.ai import mind
```
- Deprecated: application-specific imports that are part of the same top level sub-package as this file. For example:
```
from myproject.backend.hgwells import time_machine
```

Within each grouping, imports should be sorted lexicographically, ignoring case, according to each module’s full package path (the path in from path import ...). Code may optionally place a blank line between import sections.
```
import collections
import queue
import sys

from absl import app
from absl import flags
import bs4
import cryptography
import tensorflow as tf

from book.genres import scifi
from myproject.backend import huxley
from myproject.backend.hgwells import time_machine
from myproject.backend.state_machine import main_loop
from otherproject.ai import body
from otherproject.ai import mind
from otherproject.ai import soul

# Older style code may have these imports down here instead:
#from myproject.backend.hgwells import time_machine
#from myproject.backend.state_machine import main_loop
```

### III.14 Statements
Generally only one statement per line, do not with `try`/`except`

### III.15 Accessors
If an accessor function would be trivial, you should use public variables instead of accessor functions to avoid the extra cost of function calls in Python. When more functionality is added you can use `property` to keep the syntax consistent.

### III.16 Naming
`module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`, `function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`, `function_parameter_name`, `local_var_name`.
Function names, variable names, and filenames should be descriptive; eschew abbreviation. In particular, do not use abbreviations that are ambiguous or unfamiliar to readers outside your project, and do not abbreviate by deleting letters within a word.

Always use a `.py` filename extension. Never use dashes.
#### III.16.1 Names to Avoid
- single character names, except for specifically allowed cases: counters or iterators (e.g. `i`, `j`, `k`, `v`, et al.), `e` as an exception identifier in `try/except` statements, `f` as a file handle in `with` statements
    Please be mindful not to abuse single-character naming. Generally speaking, descriptiveness should be proportional to the name’s scope of visibility. For example, i might be a fine name for 5-line code block but within multiple nested scopes, it is likely too vague.
- dashes (`-`) in any package/module name
- `__double_leading_and_trailing_underscore__` names (reserved by Python)
- offensive terms

#### III.16.2 Naming Conventions
- “Internal” means internal to a module, or protected or private within a class.
- Prepending a single underscore (`_`) has some support for protecting module variables and functions (linters will flag protected member access). While prepending a double underscore (`__` aka “dunder”) to an instance variable or method effectively makes the variable or method private to its class (using name mangling) we discourage its use as it impacts readability and testability and isn’t really private.
- Place related classes and top-level functions together in a module. Unlike Java, there is no need to limit yourself to one class per module.
- Use CapWords for class names, but lower_with_under.py for module names. Although there are some old modules named CapWords.py, this is now discouraged because it’s confusing when the module happens to be named after a class. (“wait – did I write `import StringIO` or `from StringIO import StringIO`?”)
- Underscores may appear in unittest method names starting with test to separate logical components of the name, even if those components use CapWords. One possible pattern is `test<MethodUnderTest>_<state>`; for example `testPop_EmptyStack` is okay. There is no One Correct Way to name test methods.

#### III.16.3 File Naming
Python filenames must have a `.py` extension and must not contain dashes (`-`). This allows them to be imported and unittested. If you want an executable to be accessible without the extension, use a symbolic link or a simple bash wrapper containing `exec "$0.py" "$@"`.

#### III.16.4 Guidelines derived from Guido’s Recommendations
|Type| 	Public| 	Internal|
|--|--|---|
|Packages |	lower_with_under |	|
|Modules |	lower_with_under |	_lower_with_under|
|Classes |	CapWords |	_CapWords|
|Exceptions |	CapWords 	||
|Functions |	lower_with_under()| 	_lower_with_under()|
|Global/Class Constants |	CAPS_WITH_UNDER |	_CAPS_WITH_UNDER|
|Global/Class Variables |	lower_with_under |	_lower_with_under|
|Instance Variables| 	lower_with_under |	_lower_with_under (protected)|
|Method Names |	lower_with_under()| 	_lower_with_under() (protected)|
|Function/Method Parameters |	lower_with_under 	||
|Local Variables |	lower_with_under 	||

### III.17 Main
In Python, `pydoc` as well as unit tests require modules to be importable. If a file is meant to be used as an executable, its main functionality should be in a `main()` function, and your code should always check `if __name__ == '__main__'` before executing your main program, so that it is not executed when the module is imported.

When using __absl__, use `app.run`:
```
from absl import app
...

def main(argv):
    # process non-flag arguments
    ...

if __name__ == '__main__':
    app.run(main)
```
Otherwise, use:
```
def main():
    ...

if __name__ == '__main__':
    main()
```
All code at the top level will be executed when the module is imported. Be careful not to call functions, create objects, or perform other operations that should not be executed when the file is being `pydoced`.

### III.18 Function Length
Prefer small and focused functions.

We recognize that long functions are sometimes appropriate, so no hard limit is placed on function length. If a function exceeds about 40 lines, think about whether it can be broken up without harming the structure of the program.
### III.19 Type Annotations
#### III.19.1 General Rules
Familiarize yourself with [PEP-484](https://www.python.org/dev/peps/pep-0484/).<br/>
In methods, only annotate `self`, or `cls` if it is necessary for proper type information. e.g., `@classmethod def create(cls: Type[T]) -> T: return cls()`<br/>
If any other variable or a returned type should not be expressed, use `Any`.<br/>
Be not required to annotate all the functions in a module. Unless:
- At least annotate your public APIs.
- Use judgment to get to a good balance between safety and clarity on the one hand, and flexibility on the other.
- Annotate code that is prone to type-related errors (previous bugs or complexity).
- Annotate code that is hard to understand.
- Annotate code as it becomes stable from a types perspective. In many cases, you can annotate all the functions in mature code without losing too much flexibility.
#### III.19.2 Line Breaking
Try to follow the existing indentation rules.

After annotating, many function signatures will become “one parameter per line”.
```
def my_method(self,
              first_var: int,
              second_var: Foo,
              third_var: Optional[Bar]) -> int:
  ...
```
#### III.19.3 Forward Declarations
If you need to use a class name from the same module that is not yet defined – for example, if you need the class inside the class declaration, or if you use a class that is defined below – use a string for the class name.
```
class MyClass:

  def __init__(self,
               stack: List["MyClass"]) -> None:
```
#### III.19.4 Default Values
Use spaces around the `=` only for arguments that have both a type annotation and a default value.
```
Yes:
def func(a: int = 0) -> int:
  ...
```
```
No:
def func(a:int=0) -> int:
  ...
```
#### III.19.5 NoneType
In the Python type system, `NoneType` is a “first class” type, and for typing purposes, `None` is an alias for `NoneType`. If an argument can be `None`, it has to be declared! You can use `Union`, but if there is only one other type, use `Optional`.
```
Yes:
def func(a: Optional[Text], b: Optional[Text] = None) -> Text:
  ...
def multiple_nullable_union(a: Union[None, Text, int]) -> Text
  ...
```
```
No:
def nullable_union(a: Union[None, Text]) -> Text:
  ...
def implicit_optional(a: Text = None) -> Text:
  ...
```
#### III.19.6 Type Aliases
You can declare aliases of complex types. The name of an alias should be CapWorded. If the alias is used only in this module, it should be _Private.
#### III.19.7 Ignoring Types
You can disable type checking on a line with the special comment `# type: ignore`.
#### III.19.8 Typing Variables
If an internal variable has a type that is hard or impossible to infer, you can specify its type in a couple ways.

Type Comments:
Use a `# type:` comment on the end of the line
```
a = SomeUndecoratedFunction()  # type: Foo
```
Annotated Assignments
Use a colon and type between the variable name and value, as with function arguments.
```
a: Foo = SomeUndecoratedFunction()
```
#### III.19.9 Tuples vs Lists
Typed lists can only contain objects of a single type. Typed tuples can either have a single repeated type or a set number of elements with different types. The latter is commonly used as the return type from a function.
```
a = [1, 2, 3]  # type: List[int]
b = (1, 2, 3)  # type: Tuple[int, ...]
c = (1, "2", 3.5)  # type: Tuple[int, Text, float]
```
#### III.19.10 TypeVars
#### III.19.11 String types
#### III.19.12 Imports For Typing
For classes from the `typing` module, always import the class itself. You are explicitly allowed to import multiple specific classes on one line from the `typing` module. Ex:
```
from typing import Any, Dict, Optional
```
## IV. Parting Words
Conclusionly, these guideline is to have a common vocabulary of coding, which present global style rules. In paticular, we have more rule with style by the team or firm. If code you add to a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it. Therefore, avoid it.

# References
- [ ] Coding convention for Python. [link](https://google.github.io/styleguide/pyguide.html)
- [ ] PEP 8 Style Guide for Python Code. [link](https://www.python.org/dev/peps/pep-0008/#imports)
