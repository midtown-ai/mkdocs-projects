title: Python Fundamentals > Strings
---
--8<-- [start:body]

## Strings

### Immutability

/// warning | A string ~= immutable tuple of characters

In Python, immutability refers to the property of an object that cannot be changed after it is created.

```
"hello" ~= ('h', 'e', 'l', 'l', 'o' )
```

Well, not exactly because their types are different, one is 'str' while the other is 'tuple'.
They are also different objects, with different methods!

```python
type('hello')                       # <class 'str'>
type(('h', 'e', 'l', 'l', 'o'))     # <class 'tuple'>

```
///

 *  Strings are immutable in python (see replace) as are number (int, float, decimal), bool,  tuple, and range!
 *  What is immutable is the content of the string, the variable can be reassigned!

 What is unicode and utf-8 @ https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/

Demonstration of immutability

```
>>> text = "Data Science"
>>> print(id(text))
2450343168944                            # also = to id("Data Science") ;-)

>>> text += " with Python"
>>> print(id(text))
2450343426208                            # The variable points to a new identity (~pointer)

```
Source @ https://towardsdatascience.com/https-towardsdatascience-com-python-basics-mutable-vs-immutable-objects-829a0cb1530a

```
our_str ='Bonjour Monde'
our_str = 'Hello World'                         # Override variable <> immutability of pointed content

print(our_str[0])                               # At a given index, you can read, but you cannot write!
# our_str[0] = 'h'                              # Exception: TypeError: 'str' object does not support item assignment
# our_str[0] = our_str[0].lower()               # Exception! Strings are immutable
new_str = our_str.replace('World', 'Jackson')   # HERE we create a new string, the old string is not changed!
```

### Hands-on

```python
# <!> sorted(string) return a sorted list of characters contained in string
# <!> This list needs to be turned into a string using join()!
ordered_chars_LIST = sorted(string_of_unordered_chars)       # returns an ordered LIST or characters , not a string but a LIST!
ordered_chars = ''.join(sorted(unordered_chars))   # Order a string (anagram)


string1 = "this is a string"
string2 = "%s! %s" % ("hello","toto")                             # Print a string in a string!
string3 = "%(h)s! %(n)s" % { "n":"toto", "h":"hello"}             # Using named variable from a dictionary (great for templating!)

string4 = "a number y is {1:.2f} and x is {0:.3f}".format(x, y)   # order from tuple followed by format!

price = 4.55
string5 = f"Price in Swiss Franks: {price * 1.086:5.2f}"          # String literal <!> 'price' variable must exists
                                                                  # Don't forget the 'f' at the beginning of the string!

str(3210)                                  # Convert number to string '3210'
str("hello")                               # Convert a string into a string, i.e. do nothing!

float("3.1415")                            # Turn a string to float
int("3")                                   # Turn a string to a integer
# int("3.1415")                            # <!> This is an error as this is a float
int(float("3.14"))                         # <!> Ok, this works! ;-) and is 3

string3 = string1 + string2                # Concatenation operation
multiline = "This is a \n\
... multiline string"                      # Multiline string
#comment
len(var3)                                  # Length of a string


print(program, "arguments")                # Python3
print(program, "arguments", sep=" ", end="\n")    # Python3 equivalent = Concat 2 strings with a space in between + CR at the end


>>> list("hello world")                    # A string = tuple of chars --> turn a tuple of char into a list!
['h', 'e', ...., 'o', ' ', 'w', ..., 'd']

# <!> Strings are immutable, but here you are just changing where the variable points to, not the string
s = s.lstrip()                             # Remove leading spaces
s = s.rstrip()                             # Remove trailing spaces and CARRIAGE RETURNS
s = s.strip()                              # Remove leading and trailing spaces and CARRIAGE RETURNS

title = title.strip(',.-\n')               # Remove leading and trailing characters
                                           # <!> Will strip any of those characters, not the string ",.-" but individual characters!

number_of_ts = s.count('t')                # Return number of character 't' in the string
number_of_totos = s.count('toto')          # Return number of substrings

pos_of_first_t = s.find('t')
pos_of_second_t = s.find('t', pos_of_first_t)     # Find returns the index of first found 't' (or second t since starting from 1st 't' position)
                                                  # If find reaches the end, then returns -1

s.capitalize()
s.join()
s.split()                    # Split on any-block of spaces/tabs
                             # , e.g. "12    3 4" --> ['12', '3', '4']
# s.split('')                # <!> but this ~~~> ValueError: empty separator!
# s.split("")                # <!> but this ~~~> ValueError: empty separator!
s.split("\t")                # split on tab characters (\t is the tab character, not 2 chars!)
s.split(" ")                 # split on space charactes only, not tabs!
"hello world".split("wo")    # split on a GROUP of characters <!> Not like strip, which assume individual characters
"arn::account::region".split("::")    # returns a list!

# Replace = split and join?
arn = "arn::account::region"
arn = "XX".join(arn.split("::"))
=?= arn.replace("::","XX")            # ?

>>> s.translate(None, ",!.;")          # Remove unwanted characters, here the punctuation

>>> "Python".center(10)
'  Python  '

s.endswith('toto')
s.startswith('toto')

s = "one\ttwo\t\tthree\nfout"      # Tabs and other special characters in a string
print(s)                           # Transform tabs and other special characters

string_content = "line 1\nline 2\nline 3\n"
string_file_content.splitlines()             # ~ s.split('\n') ?
[ 'line 1', 'line 2', 'line 3']

>>> account_number = "43447879"
>>> account_number.zfill(12)             # Zero fill
'000043447879'
>>> account_number.rjust(12,"0")         # Right justification
'000043447879'

                                         # <!> Immutability: can only be read
string[0]                                # first character
string[-1]                               # very last character
string[1:4]                              # a slice
string[10:]                              # a slice to end of string
string[:-1]                              # everything but last character
string[:]                             # copy of string
string[::1]                           # copy of string, step of 1 (default)
string[::2]                           # print every other characters!
string[::-1]                          # reverse string, step of -1

string[::-2]                          # reverse string + take every other characters

s = " a very long string ..... "         # pep8 compliance for long string
s =(
  "a very long"
  "string ... "
)

s = """
    A multi-line string
    With space as well
and carriage returns
"""

s                      # '\n    A multi-line string\n    With space as well\nand carriage returns\n'

print(s)                # 
                        #   A multi-line string
                        #   With space as well
                        # and carriage returns
```

### Operations

```python
print("12" + "34")      # Outputs: "1234"
print("12" * 2)         # Outputs: "1212"
```

Equality/Inequality used for sorting list of strings with sorted!

```python
("a" < "b")   is True   # True
("a" < "aaa") is True   # True
("1" < "a")   is True   # True
("aaa" < "a") is False  # True, it is False ;-)

# Sorting based on ASCII code of characters!
out = sorted(["aaa", "b", "a", "2", "-1", "0"])
print(out)              # Outputs: ["-1", "0", "2", "a", "aaa", "b"]
#
```

### Print, format, and string literal

 :warning: % is an operation on string!

```
print(word)
print(word, end='\n')                # Same as above (default)
print(word, end='')                  # Print without \n

print(pyObject)                      # Use the __str__ method or if missing the __repr__ method
print("%s" % pyObject)               # Use the __str__ method or if missing the __repr__ method as well and ...
                                     # ... the module operator of string class!)
                                     # <!> __repr__ method is used for representation of the object in ipython when '>>> object'

print(word.__repr__())               # Print single quoted string as word.__repr__() is "'hello'"
print(str(pyObject))                 # Convert using the __str__ method
                                     # <-- this is the correct one!

print('a very very '
'very vreey '
'very long ine'
)

```
```
s = 'hello world!'
pi = 3.1415
print(f's is {s} and pi is {pi:.2}')          # String literal
                                              # <!>  do not forget the 'f' before the quote otherwise not expended!
print(f's is {s} and pi is {pi:.2f}')         # <!> also do not forget the f in the formatting of pi to indicate a float
                                              # the first line prints 3.1 and the second 3.14 for the value of pi !!!

```
```
>>> print(q, p, p * q, sep= " ", end="\n")      # (default) sep -> separator     end -> CR
>>> print(q, p, p * q, sep=" :-) ", end="")     # sep -> separator     end -> no carriage return
459 :-) 0.098 :-) 44.982
```

FORMAT

:warning: The pythonic way to print strings, because strings are objects!

```
>>> print("average is {f}".format(average, f=1))     # here f is a MIX of variables + named arguments
average is 1                                         # <!> 1 is not the DEFAULT value for f, but the constant value of f !
                                                     # f is a keyword argument (a variable to be called in the formatted string)

>>> print("average is {:f}".format(average, f=1))    # here f is formatting of DEFAULT first element, i.e 0, as a float
                                                     # <!> if {} were to reappear in the string, it would point to the second element (which does not exist here)
                                                     # {} points to the first element only when appear first, then the counter is incremented!
average is 2.300000
>>> print("average is {0:f}".format(average, f=1))    # here f is formatting of element 0 (float) - same as above but more explicit!
average is 2.300000
>>> >>> print("average is {1:f}".format(average, 3.4, f=1.2))    # here 3.4 is element at pos 1
average is 3.400000                                              # Is f=1.2 at pos 2? NO! 'f' = keyword argument (**kwargs), while average and 3.4 are positional args (*args)

# >>> print("average is {1:f}".format(average, f=1))    # IndexError: Replacement index 1 out of range for positional args tuple
                                                        # Tuple *arg vs **kargs dict ? Yes!

>>> f = 1
>>> print("average is {1:f} {0:f}".format(average, f))  # the last f is the value of the variable 'f' and is a positional argument of the format method


>>> x = 3.1415
>>> float("{0:.2f}".format(x))                 # don't forget the 'f' for float!
3.14

>>> print("{:d}".format(7000))
7000
>>> print("{:,d}".format(7000))
7,000
>>> print("{:^15,d}".format(7000))              # 15 is total number of characters, 7,0000 is centered
     7,000
>>> print("{:*^15,d}".format(7000))
*****7,000*****
>>> print("{:*^15.2f}".format(7000))
****7000.00****
>>> print("{:*>15,d}".format(7000))
**********7,000
>>> print("{:*<15,d}".format(7000))             # left alignment
7,000**********
>>> print("{:*>15X}".format(7000))              # right alignment
***********1B58
>>> print("{:*<#15x}".format(7000))             # hexadecimal format
0x1b58*********


if not testbed:
        raise Exception("No such testbed {}".format(testbed_name))

>>> '{0}{1}{0}'.format('abra', 'cad')                  # arguments' indices can be repeated
'abracadabra'                                          # ~ format of a tuple, and index in the tuple

>>> 'Coordinates: {latitude}, {longitude}'.format(latitude='37.24N', longitude='-115.81W')  # With named arguments
'Coordinates: 37.24N, -115.81W'
>>> "Art: {a:5d},  Price: {p:8.2f}".format(a=453, p=59.058)
'Art:   453,  Price:    59.06'

>>> print("I've <{}> years of experience and my salary is <{:,}> USD per annum.".format(10, 75000))  # {} points to first and then {} points to second element
I've <10> years of experience and my salary is <75,000> USD per annum.

>>> data = dict(province="Ontario",capital="Toronto")
>>> data
{'province': 'Ontario', 'capital': 'Toronto'}
>>> print("The capital of {province} is {capital}".format(**data))         # With a dictionary
                                                                           # SWEET **kwargs --> **dictionary !!!

"{0:<20s} {1:6.2f}".format('Spam & Eggs:', 6.99)                           # With anchored strings
'Spam & Eggs:           6.99'


>>> class Point(object):
...     def __init__(self, x, y):
...         self.x, self.y = x, y
...     def __str__(self):
...         return 'Point({self.x}, {self.y})'.format(self=self)          # with objects
...     def __repr__(self):
...             return 'REPR Point({self.x}, {self.y})'.format(self=self)
...
>>> str(Point(4, 2))
'Point(4, 2)'
>>> Point(4,2)
REPR Point(4, 2)
```

Source @ https://www.python-course.eu/python3_formatted_output.php

More @ https://www.techbeamers.com/python-format-string-list-dict/

SHORT FORMAT (aka string literal -- see above)
  * <!> If variable does not exist ---> Exception: !NameError: name 'ss' is not defined

```
def greet(name):
    print(f"Hello {name}")           # aka string literal
```

### Print in a file

```
from __future__ import print_function

s = 'hello world!'
# f = open("file.txt", "a")
with open("file.txt", "a") as f:
    print(s, end="", file=f)            # Python3
```

Source @ https://stackoverflow.com/questions/9236198/python-3-operator-to-print-to-file

### Conversion

  * :warning: List are indexed at 0
  * :warning: spliting a list gives you a list of string which you need to reformat 

```
abc = "abcde....z"        # A string is an immutable tuple of characters
char_list = list(abc)


s = 'afdadf 5 dfad 5.0 dfdsdf'
# token = s.split(' ')          # Split on space character
token = s.split()               # Split on any space char, including tab and multiple space
sum = sum + int(token[1]) + float(token[3])   # sum = sum + 5 + 5.0
```

### Char in strings (char = string of len 1)

:warning:Char is a string of length 1 !

```
abc = "abcde....z"          # sring = an immutalbe tuple of characters!
char_list = list(abc)

>>> type('a')
<class 'str'>
>>> chr(97)
'a'
>>> ord('a')              # works only on string of length 1
97

type(chr(97))             # <class 'str'>

>>> s = "asjo,fdjk;djaso,oio!kod.kps"
>>> s.translate(None, ",!.;")          # Remove unwanted characters
'asjofdjkdjasooiokodkjodsdkps'

list('cat')                            # Turn a list in list of chars
['c', 'a',''t' ]


>>> for char in "python":              # iterate on the char
...     print(char)

>>> for char in list(string):    # string --> list of chars (same as above)
    print(char)

for pos, char in enumerate(string):         # With index/position!
    print(pos, char)
    print(pos, char, sep=' ', end='\n')     # same as above (with explicit default values!)
```

### Words in string (not regex)

:warning: Instead of regex, use method or operations of strings

```
new_str = our_str.replace('World', 'Jackson')    # Don't change the same string
                                                 # <!> strings are immutable!

if "blah" in "otherstringblahtoto": 
    print('found group of chars')

s = 'tatatititata'
if s.find('toto') == -1:
    print("Not found!")

s.find('ata')                  # return the position of the first occurence


s = "worl"
S = "Hello world!"
>>> S.find(s)
7

s.endswith('toto')
s.startswith('toto')

with open("myfile", r) as file:

    # for line in file.readlines():
    for line in file:                               # readlines from files (.readlines is implied)
        # print(line)
        # print(line, end='\n')                     # Same as line above, but <!> the line also includes a carriage return! ==> 2 carriage returns!
        print(line, end='')                         # Here we remove the extra carriage return added by the print statement!
        print(line.rstrip())                        # Here we remove the \n from the string, but add the one from the print!

for word in string.split():                         # Process words one at a time (split on spaces)
    print(word, end='')                             # (Python3)
```

REGEX overkill!

```
# Using regex module!
import re
words = re.split('\W+', 'Words1, words2, words3.')   # \W+ matches **one or more non-word characters**
print(words)               # Outputs ['Words', 'words', 'words', '']
```

### __Str__ method of Classes/Objects

```
>>> class Point(object):
...     def __init__(self, x, y):
...         self.x, self.y = x, y
...     def __str__(self):
...         """Used for string conversion, i.e. str(point) or print(point) or '%s' % point """
...         return 'Point({self.x}, {self.y})'.format(self=self)
...     def __repr__(self):
...         """Used for repr(point) or in ipython when >>> P
...            but is also used whenever the __str__() method would normally be used and when not defined/present!"""
...         return('toto')
...
>>> str(Point(4, 2))
'Point(4, 2)'
```

More @ https://docs.python.org/2/library/string.html

### variables, slicing

```
2/ STRING, VARIABLES, SLICING

#!/usr/bin/env python

word = input("Enter a word: ")                          # python 3
print(word[1:] + word[0] + 'ay')
```

### user input

```
language = input('Enter language')              # Python3 
if language in ['C++', 'Python', 'Java']:
   print(language, "rocks!")
if language not in [ 'French', 'English']:
   print(language, "sucks!")
```

### Introspection

 *  <!> used a variable 's' or the type 'str', but not the value of the variable i.e. not 'dir('toto'.replace)

```
>>> s = 'toto'

>>> type(s)
str

>>> dir(s)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']

>>> help(s.split)
split(sep=None, maxsplit=-1) method of builtins.str instance
...
```


--8<-- [end:body]
