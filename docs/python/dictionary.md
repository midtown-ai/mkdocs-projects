title: Python Fundamentals > Dictionary
---
--8<-- [start:body]
## Dictionary

/// Warning | Immutable keys

keys must be of an immutable data type such as strings, numbers, or tuples.
///

```python
d = {1: 'hello'}                     # d[1] = 'hello'
d = {(1,2): 'hi'}                    # d[(1,2)] = 'hi'
d = {'a_word': 'bonjour'}
d = {'c':  'hello'}
```

### Hands-on

/// details | How to set default values for the dictionary?
    type: question

Use d.get('c', 'default_value')
///

/// details | How to remove a key from a dictionary?
    type: question

Use "del d['key']"
///


```python
# Width dict comprehension
my_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4}
keys_to_remove = {'b', 'c'}
filtered_dict = {k: v for k, v in my_dict.items() if k not in keys_to_remove}
print(filtered_dict)

# with d.pop('key')
my_dict = {'a': 1, 'b': 2, 'c': 3}
value = my_dict.pop('b')
print(my_dict)  # {'a': 1, 'c': 3}
print(value)  # 2 (popped value)
```

```python
>>> d = dict()
>>> d = {'key': 'value'}              # Dicts uses curly braces for their representation

>>> d = {'a': 1, 'b': 9}

>>> d['key']                          # Key must be unique and MUST EXIST ! Otherwise KeyError Exception
'value'
>>> d.get(key)                        # Key must be unique, if does NOT exist return None
>>> d.get('c') is None
True
>>> d.get(key) == 'value'             # False if key does NOT exist !
False
>>> d.get(key, 'value_if_not_exist')  # A key if doesn't exist <!> Unlike setdefault, does not update the dictionary
>>> d.get('c','toto') == 'toto'
True

>>> d.setdefault('toto', 2)           # Same as g.get('toto', 2) that is returns the dict value, but will update the dictionary in place
>>> d.setdefault('titi')              # Here the default value is None + update dictionary, same as d.setdefault('titi', None)
>>> d.setdefault('tata', {'sub': 1} ) # Can be a complex default value!
>>> d.setdefault('l', []).append(2)   # will creaete the ey/value pair if does not exist and append 2 to it <!> can fail if 'l' is different from a list!

>>> d['l2'] = d['l']                  # <!> not a copy of the list, but a reference to it!
>>> d['l2'].append(3)                 # append 3 to both list !!!!!

d = {'a': 1, 'b': 2}
v = d.setdefault('c', 100)            # Key 'c' doesn't exist, so it adds 'c': 100 and return 100
print(v)                              # 100
print(d)                              # {'a': 1, 'b': 2, 'c': 100}


d['key'] = 'value'             # Add a new key/value pair in the dict
'key' in d.keys()              # Check that the key is in dict (True)
del d['key']                   # remove key/value pair
'key' in d.keys()              # Check that the key is in dict (False)

d.keys()                       # returns all keys
d.values()                     # Returns all the values (same order as d.keys())


del dict['Name'];                     # remove entry with key 'Name'
dict.clear();                         # remove all entries in dict, dict is empty dictionary
del dict ;                            # delete entire dictionary, dict variable does not exist anymore


>>> d.items()                         # Iterator-like, list of tuples, but not an iterator!
dict_items([('a', 1), ('b', 9)])

list(d.items())[1]                    # ('b', 2)
list(d.items())[0]                    # ('a', 1)

>>> for k in d                        # Iterate on the keys (same as d.keys())
...     print(k)

>>> for kv in d.items():              # Get the kv tuples
        print(kv)                     # print the tuple

>>> for key, value in d.items():      # Iterate on key and value pairs (was d.iteritems())
                                      # returns a list of tuples
...     print(key, ' -> ', value)

>>> d = {'a': 1, 'b': 2}
>>> 'a' in d                          # A replacement for d.has_key()
True

>>> d.get('a') != None
True

>>> d.get('X') == None                # <!> When using 'dict.get', None is the default value if the key does not exist
True

```

### map on dictionary (rebuild ALL k-v pairs)

 . <!> Also known as dictionary comprehension

```python
def f(value):
   return value**2

my_dictionary = {k: f(v) for k, v in my_dictionary.items()  if k == 1}       # Dict comprehension with filtering-condition!

# or less readable

my_dictionary = dict(map(lambda kv: (kv[0], f(kv[1]) ), d.items()))    # d.items is a LIST of tuples fed to the lambda function!
                                                                       # notice that the map is a map of tuples ... that is then turned into a dict
                                                                       # similar to what d.items() would return... kv tuples!

```

Source @ https://stackoverflow.com/questions/12229064/mapping-over-values-in-a-python-dictionary

### = vs shallow copy method vs copy.deepcopy function

 . <!> with =, the dictionary points to exactly the same content (= identity ~ pointer) - change to immutable/mutable vars are propagated
    * list or 'list_1 = list_2', this is not a copy but 2 variables pointing to the same memory space
 . <!> with the copy dictionary method, the immutable are 'duplicated', the mutable are the same and change together
 . <!> with copy.deepcopy, the 2 dictionaries are completely independent

```python
>>> d = {'a': 1, 'b': 2}
>>> dd = d                       # d and dd are the same !
                                 # A change in one = a change in the other!
>>> id(d) == id(dd)
True
>>> dd['a'] = 3
>>> print(d['a'])
3
```

```python
import copy           # required for deepcopy, but not for copy!

otherDict = copy.deepcopy(wordsDict)           # Create a deep copy of the dictionary
```

 . <!> With shallow copy, ---> copy the object identities (values in particular, since key are immutables)
   * the dictionary values that are mutable (list,...) when changed in one change in the other
   * immutable (numbers, strings, tuple values) are NOT shared
   * copy mutable (list dict, and set) by reference ==> change a mutable's value == change in all dictionary!

```
# create a Shallow copy  the original dictionary
d = {'a': 1, 'b': 2, 'c': [1, 2, 3, 45]}
d_copy = d.copy()

d_copy["c"].append(222)

print d                                        # The original dictionary has been changed!
{'a': 1, 'c': [1, 2, 3, 45, 222], 'b': 2}

>>> d_copy['e'] = [3, 5, 4]                    # Add new element
>>> d
{'a': 1, 'c': [1, 2, 3, 45, 222], 'b': 2}.     # new key is not in original dictionary !!!
>>> d_copy
{'a': 1, 'c': [1, 2, 3, 45, 222], 'b': 2, 'e': [3, 5, 4]}
```

Source @ [[https://thispointer.com/python-how-to-copy-a-dictionary-shallow-copy-vs-deep-copy/||target='_blank']]

```python
import copy

# Original dictionary
original = {'a': 1, 'b': [2, 3]}

# Creating a shallow copy
shallow = copy.copy(original)

# Modifying the nested list
shallow['b'].append(4)

print(original)  # {'a': 1, 'b': [2, 3, 4]}
print(shallow)   # {'a': 1, 'b': [2, 3, 4]} (Both changed!)

# other ways to create shallow copies
shallow = original.copy()  # Built-in method
shallow = dict(original)   # Using dict() constructor
shallow = {k: v for k, v in original.items()}  # Dictionary comprehension

```

```python
# DEEP Copy
✅ All nested objects are also copied.
✅ No shared references—each copy is fully independent.

import copy

# Original dictionary with nested structure
original = {'a': 1, 'b': [2, 3]}

# Creating a deep copy
deep = copy.deepcopy(original)

# Modifying the nested list
deep['b'].append(4)

print(original)  # {'a': 1, 'b': [2, 3]} (Original unchanged)
print(deep)      # {'a': 1, 'b': [2, 3, 4]} (Deep copy modified separately)

```

 * Use copy.copy() (shallow copy) when your dictionary contains only immutable values (numbers, strings, tuples).
 * Use copy.deepcopy() (deep copy) when your dictionary has nested mutable objects (lists, sets, other dictionaries) and you want full independence.

### Hidden dictionary

```python
Given a list of words, group the anagram in a sublist together
['abc', 'bar', 'cab'] ---> [ ['cab', 'abc'], ['bar']]

   Def ana(L):                             # L is list of words
	anagrams = {}
	For word in L:
		C = sorted(word)           # Reorder the chars of the word
		If C not in anagrams:      # C is not a key in the dictionary
			anagrams[C] = []
		anagrams[C].append(word)   # = anagram_list
	Return list(anagrams.values())           # return the values of anagrams dict

```

### map on dict = dict comprehension

 . <!> Not quite an iterator but known as dictionary comprehension

```python
def f(value):
   return value**2

my_dictionary = {k: f(v) for k, v in my_dictionary.items()}

# or less readable

my_dict = dict(map(lambda kv: (kv[0], f(kv[1])), my_dict.items()))

my_dict = dict(
    map(lambda kv: (kv[0], f(kv[1]) ) , my_dict.items())           # dict( [ (k, v), ... ] ) ~~> {k:v, ...}
 )

# or

for k, v in d.items():
    d['k'] = f(v)

```

Source @ https://stackoverflow.com/questions/12229064/mapping-over-values-in-a-python-dictionary

###  A dictionary of functions (switch ... case ...)

 . <!> A dictionary of function
 . <!> Key in dictionary are immutable numbers

```python
import math
from math import sqrt

def zero():                        # zero is a variable-reference to the function object!
    print("You typed zero.\n")

type(zero)            # <class 'function'>

def sqr():
    print("n is a perfect square\n")

def even():
    print("n is an even number\n")

def prime():
    print("n is a prime number\n")

# All numbers from 0 to 9 are 'switch' keys, or keys in the option dictionary
options = {
    0 : zero,
    1 : sqr,         # function name/reference!
    2 : even,
    3 : prime,
    4 : sqr,         # beware function need to be defined before reference is used
    5 : prime,
    6 : even,

    7 : math.sqrt,            # import ...
    8 : sqrt,                 # from math ...

    9 : lambda x : x*x,       # yes, you can have 2 colon-chars in the same line ! The comma is the entry separator!
    # * : lambda : None,      # See how to set the default function if not found!
}

options[num]()
```

You gould also handle the missing default case by doing this instead:

```
options.get(num, lambda : None)()        # Default value for the function !

>>> d.get('*', lambda: None)() == None     # Beware: This is different from d.get('*', None)() which generate an exception because None() or None is not callable!
True                                       # A lambda is callable!
```

 Which will return None if num is not in options.


 <<Highlight("Since python3.10")>>
```python
def switch_example(value):
    match value:
        case 1:
            print("One")
        case 2:
            print("Two")
        case 3:
            print("Three")
        case _:
            print("Default case: Not 1, 2, or 3")

switch_example(2)  # Output: Two

```

### json.load vs eval

 * string of a dict to dict
 * source  @ https://stackoverflow.com/questions/988228/convert-a-string-representation-of-a-dictionary-to-a-dictionary
  . Ex API call response

### introspection

```python
>>> d = {}
>>> type(d)
<class 'dict'>

>>> dir(dict)
['__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']

>>> help(dict.keys())
keys(...)
    D.keys() -> a set-like object providing a view on D's keys
```

--8<-- [end:body]
