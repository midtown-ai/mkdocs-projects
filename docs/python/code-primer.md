title: Python Fundamentals > Code Primer
---
# --8<-- [start:body]

## Code Primer

```python {title="Arguments from command line"}
#!/usr/bin/env python3

import sys

def main(argv):
    assert len(argv) >= 3, 'Too few parameters'
    assert len(argv) <= 1, 'No parameter to command line provided'
    print(argv)

    prog_name = argv[0]
    argument_1 = argv[1]


if __name__ == "__main__":     # when you run the python file, __name__ is set to "__main__"
                               # Otherwise it is set to the module name
    main(sys.argv)
```

# --8<-- [end:top]

```python {title="The invisible dictionary problem :-)"}
#!/usr/bin/env python3

# Given a list of words, group the anagram in a sublist together
# ['abc', 'bar', 'cab'] ---> [ ['cab', 'abc'], ['bar']]

def ana(L):                             # (1)
    anagrams = {}
    for word in L:
        K = ''.join(sorted(word))       # (2)
        if K not in anagrams.keys():    # (3)
            anagrams[K] = []
        anagrams[K].append(word)        # = anagram_list
    dict_values = anagrams.values()     # <!> type is dict_values([['abc', 'cab'], ['bar']])
    return( list(dict_values) )         # return the values of the anagrams dict in a list format

# ana(['abc', 'bar', 'cab'])[0]
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: 'dict_values' object is not subscriptable
# list(ana(['abc', 'bar', 'cab']))[0]
# ['abc', 'cab']
```

1.  L is list of words
2.  Reorder the chars of the word
    sorted(word) ==> list of ordered characters as if 'word' was a list of char
    sorted('akc') ==> ['a', 'c', 'k']
3.  K is NOT already a key in the dictionary
    ... create key/entry + initialize

```python {title="Add elements in two lists"}

x_values_list = [1, 2, 3] 
y_values_list = [4, 5, 6] 
  
m = map(lambda x, y: x + y, x_values_list, y_values_list)     # m is <map at 0x104a65180>
                                                              # similar to: for x, y in zip(x_values_list, y_values_list) ? Almost!
                                                              # zip returns an iterable on tuples, not a map object!
type(m)                                                       # m is a map
list(m)                                                       # a list ;-)   or [5, 7, 9]

ret_list = list(map(lambda x, y: x + y, x_values_list, y_values_list))   # Add list for Python3
ret_list = list(map(lambda x: x**2, x_values_list))
```

```python {title="Sorting list of tuples uses the first element of the tuple"}
>>> _list = [ ('a',34), ('z', 23), ('b', 44)]
>>> sorted(_list)                                 # sort list items based on the first value in the 
[('a', 34), ('b', 44), ('z', 23)]

# (DEPRECATED) Sort based on 2nd field of tuple ~~~> reverse tuple
>>> _list = sorted(list(map(lambda el: el[::-1], _list)))

# >>> el_values_list = _list                                            # Those 2 lines ... 
# >>> _list = sorted(list(map(lambda el: el[::-1], el_values_list)))    # ... do the same as above! 

>>> sorted(_list)                              # Sort the elements of a list... using the first value in each element! 
[(23, 'z'), (34, 'a'), (44, 'b')]
```

```python {title="Sorting list of tuples using the 2 element of each tuple"}
data = [("apple", 3), ("banana", 1), ("cherry", 2)]

# Sort by second element (index 1)
sorted_data = sorted(data, key=lambda x: x[1])

print(sorted_data)
# Output: [('banana', 1), ('cherry', 2), ('apple', 3)]
```

```python {title="List comprehension"}
>>> [ c*2 for c in "012345678" ]
['00', '11', '22', '33', '44', '55', '66', '77', '88']

# Dictionary comprehension
# build a new dictionary using a function
my_dictionary_comprehension = {k: f(v) for k, v in d.items()  if k == 1}

# Fct
def myfunc(self, *args, **kwargs) :    # args is a tuple, kwargs is a dict
```

```python {title="Getting help"}
import my_module as mm
help(mm)                     # print the docstring of the module + of functions
help(mm.greet)               # print the docstring of the given function in the module
help(WHATEVER)               # <== prints docstrings
help()                       # <== help in interactive mode

help(dir)
dir()                        # List variables/names in the current scope
dir(int)                     # dir (<class>) --> list methods of <class>
help(int.to_bytes)           # help ( <class>.<method> )
dir(WHATEVER)                <== returns a list of variables in scope of methods

assert 3/4 > 1, "not so fast!"  # raise AssertionError with explanation
help(assert)                 # Fails, assert is a statement, not a function, i.e. assert()!
help(assert.__doc__)         # Fails 
help('assert')               # Works! help for the standalone command 'assert'


help(str)                    # return info for method and class for 'str' objects
help(str.__doc__)            # ok, works, but not formatted correctly
print(str.__doc__)           # print the help for the 'str' type conversion function

<!> If module was already loaded, you need to reload it!
import importlib
importlib.reload(my_module)  # or .reload(mm)
```

```python {title="Primer with doctests"}
# To run if testmod block is not present: python -m doctest your_file.py
# Python will automatically scan the file for docstring tests and run them.
def add(a, b):
    """
    Returns the sum of a and b.

    >>> add(2, 3)
    5
    >>> add(-1, 1)
    0
    """
    return a + b

# To run the tests (with testmod() block ): python calculator.py
if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

```python {title="Primer with Python debugger"}
import pdb

def add(a, b):
    pdb.set_trace()                               # Execution will pause here (when run with pdb)
    return a + b

result = add(3, 5)
print(result)



$ python -m pdb my_script.py                      # run the pdb

pdb
# operations
n | next
s | step               - step into a function call
c | continue           - continue exection until next breakbpoint
r | return             - continue execution until function returns
q | quit               - quit debugger

b 10                   - set a breakpoint at line 10
l | list               - list all breakpoints


p variable             - print the value of a variable
pp variable            - pretty print of a variable
```
