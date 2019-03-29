---
layout: page
title: Python Single Asterisk Operator
---

#### Single asterisk (`*`) unpacks iterables

The single asterisk (`*`) operator unpack a list or tuple into positional arguments. Positional argument is an argument that is not a keywork argument. 

A keywork argument is an argument preceded by an identifier (e.g. name=) in **_a function call_**. For example, `3` and `5` are both keyword arguments in the following call to `complex()`:

```
complex(real=3, imag=5)
```

An example of positional arguments (`3` and `5`):

```
add(3, 5)
```

A positional argument can also be passed as elements of an _iterable_ preceded by `*`, which **unpack** the _iterable_ into positional arguments. For example, `3` and `5` are both positional arguments in the following calls:

```
add(*(3, 5)) # unpack a tuple
add(*[3, 5]) # unpack a list
add(*{3: 'x', 5: 'y'}) # unpack a dictionary into a tuple of keys
```

A keywork argument can be passed as a value in a _dictionary_ preceded by `**`. For example, `3` and `5` are both keyword arguments in the following call to `complex()`:

```
complex(**{'real': 3, 'imag': 5}) 
```

Here are some examples that maybe helpful to understand `*` and `**`.

```
def complex(real, imag):
	print('real:', real, 'imag:', imag)

>>> complex(*[3,5])
real 3 , imag 5
>>> complex(*{3:'x', 5:'y'})
real 3 , imag 5
>>> complex(**{'real':3, 'imag':5})
real 3 , imag 5
>>> complex(**{'real':5, 'imag':3})
real 5 , imag 3
```

#### Single asterisk (`*`) helps to define variadic functions

Variadic function accepts a variable number of arguments. For example, `print_names` function takes only positional arguments:

```
def print_names(*names):
	print(type(names)) # the positional arguments are encodes as a tuple
	print(names)

>>> print_names('Alice', 'Bob', 'Cher')
<class 'tuple'>
('Alice', 'Bob', 'Cher')
```

Function `print_personal_info` takes only keyworks arguments:

```
def print_personal_info(**personal_info):
	print(type(personal_info)) # the keyworks arguments are encodes as a dictionary
	for name in personal_info:
		print(name, personal_info[name])

>>> print_personal_info(Alice=10, Bob=5, Cher=6)
<class 'dict'>
Alice 10
Bob 5
Cher 6
```

Here's an exmaple of a function takes both positional arguments and keywork arguments:

```
def print_person(*names, **personal_info):
	print(names)
	for name in personal_info:
		print(name, personal_info[name])

>>> print_person('Alice', 'Bob', 'Cher', Alice=10, Bob=5)
('Alice', 'Bob', 'Cher')
Alice 10
Bob 5

# You have to follow the order of the positional argument
# and the keywork argument, otherwise you get an error
>>> print_person('Alice', Alice=10, 'Bob', 'Cher')
SyntaxError: positional argument follows keyword argument
```