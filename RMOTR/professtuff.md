class-1
Mention keywords that students should keep digging about.

Loops: break, continue

```python
# Basic implementation using `elif` with operation as a string argument
def calculator(num1, num2, operation):
    if operation == 'sum':
        return num1 + num2
    elif operation == 'substract':
        return num1 - num2

assert calculator(1, 2, 'sum') == 3
assert calculator(5, 3, 'substract') == 2


# Move operations as external functions
def my_sum(num1, num2):
    return num1 + num2


def my_substract(num1, num2):
    return num1 - num2


def calculator(num1, num2, operation):
    if operation == 'sum':
        return my_sum(num1, num2)
    elif operation == 'substract':
        return my_substract(num1, num2)

assert calculator(1, 2, my_sum) == 3
assert calculator(5, 3, my_substract) == 2


# Send operation functions as argument instead of operation string
def calculator(num1, num2, operation):
    return operation(num1, num2)

assert calculator(1, 2, my_sum) == 3
assert calculator(5, 3, my_substract) == 2


# Accept variable length arguments
def my_sum(*args):
    return sum(args)


def my_substract(*args):
    return args[0] - sum(args[1:])


def calculator(operation, *args):
    return operation(*args)

assert calculator(my_sum, 1, 2, 4, 5) == 12
assert calculator(my_substract, 10, 3, 2) == 5
```

Using mutable objects as default argumentsa
```python
# Do not use mutable objects as default arguments
def my_function(a_list=[]):
    a_list.append(1)
    print(a_list)

my_function()
my_function()
my_function()


# How to solve it
def my_function(a_list=None):
    if not a_list:
        a_list = []
    a_list.append(1)
    print(a_list)
```

from __future__ import division

Functions
https://docs.google.com/presentation/d/1AOLC7RC7fkiY2i7EookjY75DkJqwsS2h4h1_TTWXCl8/edit#slide=id.ga856518b0_04
named arguments
variable amount of arguments
(again, calculator example)

Assert as TDD

Functions as first class citizens

Groups, organize meeting out of class.
Raw
 class-2
1) Share opinions about group work. Quick demo of tic-tac-toe solutions.


2) Quick review of collections, and comprehensions
https://docs.google.com/presentation/d/1ZH1OJNJSwcgtDfPsXWnU427gRXu0O-NigYgYT8pV0tI/edit#slide=id.ga856183b3_025


3) Functional programming (immutability, lambdas, map, filter, reduce)
https://docs.google.com/presentation/d/1E_0iKnfRlnMNcybTn7sgjhIMAnsIBEs4Em_zUb_4eQI/edit#slide=id.gb3d17b520_0_64

a_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]
sum([e ** 2 for e in a_list if e < 5])
reduce(lambda accum, value: accum + value, map(lambda x: x ** 2, filter(lambda x: x < 5, a_list)), 0)


4) divisible_numbers assignment. Basic implementation with pseudocode, for loop, comprehensions, nested comprehensions
https://sis.rmotr.com/admin/assignments/assignment/13/

"""
Write a function that receives a list of numbers
and a list of terms and returns only the elements that are divisible
by all of those terms. You must use two nested list comprehensions to solve it.

Example:
    divisible_numbers([12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1], [2, 3])  # [12, 6]

"""

def is_divisible_by(elem, a_list_of_terms):
    # for term in a_list_of_terms:
    #     if elem % term != 0:
    #         return False
    # return True
    return all([elem % term == 0 for term in a_list_of_terms])


def divisible_numbers(a_list, a_list_of_terms):
    # result = []
    # for elem in a_list:
    #     if is_divisible_by(elem, a_list_of_terms):
    #         result.append(elem)
    # return result
    return [elem for elem in a_list if is_divisible_by(elem, a_list_of_terms)]

assert set(divisible_numbers([12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1], [2, 3]))  == set([6, 12])
assert divisible_numbers([16, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1], [2, 3, 4])  == [12]


5) Groups, organize meeting out of class.
Raw
 class-3
1) Battleship demostration

2) quick review of OOP concepts: 
- classes and objects (cookie cutter example)
- attributes
- "self"
- methods
  - instance, static, class methods, property
  - magic method (operator overloading)
  http://www.rafekettler.com/magicmethods.html
  Example:
  https://gist.github.com/martinzugnoni/ecb1196d334699cf174c

3) inheritance (super, __mro__), abstract classes

4) polymorphism
https://gist.github.com/martinzugnoni/d57ed2326dab4247ea1c

5) mixins
https://gist.github.com/martinzugnoni/ce8d2228615f61c412d8

6) iterators and generators
```
# Generator example:
def my_generator(num):
    print("Starting...")
    for i in range(num):
        print("Number {}".format(i))
        yield i
    print("Finished.")
        
        
mg = my_generator(5)
mg.next()
```
Raw
 class-4

1) files
==================
Docs:
https://docs.python.org/2/library/stdtypes.html#file-objects


f = open('text.txt')  # read
f = open('text.txt', 'r')  # read
f = open('text.txt', 'a')  # append (write without erase)
f = open('text.txt', 'w')  # write erasing
f = open('text.txt', 'r+')  # read + write
f = open('text.txt', 'b')  # binary


f.close()


f.read()
f.read(size_in_bytes)


f.readline()
f.readline(size_in_bytes)


f.readlines()
same as: list(f)


f.seek(offset, from_what)
"""
A "from_what" value of 0 measures from the beginning of the file, 1 uses the 
current file position, and 2 uses the end of the file as the reference point. 
"from_what" can be omitted and defaults to 0, using the beginning of the file 
as the reference point.
"""


f.tell()


f.__iter__()
f.next()


f.write(string)
f.writelines([str1, str2, ...])


for line in f:
    pass


StringIO
https://docs.python.org/2/library/stringio.html


Exercise:
"""
Write a function, that receives the path to a text file that contains JUST ONE word
per line, and returns a dictionary with the counter of words starting with each
letter from 'a' to 'z'.

def counter_by_letter(filepath):
    import string
    
    counters = {}
    for s in string.ascii_lowercase:
        counters.setdefault(s, 0)
      
    with open(filepath) as f:
        for line in f.readlines():
            counters[line[0]] += 1
        return counters
"""
==================

2) context managers
    - Count lines in a text file starting with each letter
    - Sort lines in a text file

3) decorators
==================
def safe_execution(original_func):
    def new_func(*args, **kwargs):
        try:
            return original_func(*args, **kwargs)
        except:
            print('Something went wrong!')
    return new_func


@safe_execution
def divide(a1, a2):
    return a1 / a2
==================


4) modules and packages
    __all__
    sys.path
    virtualenvs / virtualenv-wrapper
        -a project_path
        -r requirements_file
        -p PYTHON_EXE, --python=PYTHON_EXE
        
=================
virtualenv env1
virtualenv -p python3.4 env2


source env1/bin/activate


deactivate


pip
pip list
pip freeze
pip install


Virtualenvwrapper
https://virtualenvwrapper.readthedocs.org/en/latest/


mkvirtualenv env1
mkvirtualenv -p $(which python3.4) env1
workon env1
rmvirtualenv env1
=================
        

5) unit testing
Raw
 class-5
1) OOP quiz

2) client-server workflow

3) step by step introduction to Flask
https://github.com/rmotr/flask-introduction

Access to webapp running in C9:
http://b4_pyp_g1-c9-martinzugnoni.c9users.io/
http://<workspace-name>-c9-<user-name>.c9users.io/


SQLite3:
=========
.exit
.tables
.help
.schema <table> (same as describe)


$ sqlite3 library.db < library-schema.sql
$ sqlite3 library.db < initial-data.sql

$ sudo pip install Flask-SQLAlchemy

```
# playing around with SQLAlchemy
edgar = Author.query.all()[0]
edgar.name
edgar.country.name

# inverse relationship
us = Country.query.all()[0]
authors_from_us
