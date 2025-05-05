title: Python Fundamentals > Tuple
---
--8<-- [start:body]
## Tuple

### Immutability

Some objects contain references to other objects, these objects are called containers. Some examples of containers are a tuple, list, and dictionary. The value of an immutable container that contains a reference to a mutable object can be changed if that mutable object is changed. <<Highlight("However, the container is still considered immutable because when we talk about the mutability of a container only the **identities** of the contained objects are implied")>>.

/// Warning | Immutability

 * <!> What is immutable is the content of the tuple, the variable can be reassigned!
 * <!> other immutable types are int, float, decimal, bool, string, tuple, and range.

 More @ https://www.thegeekstuff.com/2019/03/python-tuple-examples/#more-17801

 * <!> TUPLES ARE IMMUTABLE (Value cannot be changed) as are string and numbers
 * <!> TUPLES ARE CONTAINER OBJECT, ex tuple of list

///

Example

```python
t = ([1,2], [0])
id(t[0])                  # identity of t[0] is 4368558656
t[0].append(3)            # Here we are not changing the tuple t[0] reference! We are changing the value of the list t[0] is pointing to!
print(t)                  # ([1, 2, 3], [0])     <== Value of list in t[0] has changed!
id(t[0])                  # identity of t[0] is 4368558656   <== id has NOT changed!
```

But

```
>>> t[0] = 1                 # t[0] can only point to the particular list it was initialized to!
TypeError: 'tuple' object does not support item assignment
```

### Hands-on

```python
tuple = ([0,1,2], 'two', 'three')
tuple = [0,1,2], 'two', 'three'       # Same as above without the parentheses!
tuple                                 # ([0, 1, 2], 'two', 'three')

id(tuple)                       # 4368483584  <-- identity the variable points to

tuple[::-1]                        # reverse a tuple! But immutability?!?!?
                                   # The identities have not changed in the original tuple!
('three', 'two', [0, 1, 2])        # Here we are just printing/displaying a new tuple!

tuple = tuple[::-1]            # Now the variable points to a new immutable tuple
id(tuple)                      # 4364976768 or different from the previous one!

>>> print(tuple[1])

>>> tuple[1] = 'deux'              # BEWARE IMMUTABILITY !
                                   # Value cannot change! (Assignment)
TypeError: 'tuple' object does not support item assignment

>>> tuple = ('three', 'two', [0, 'w', 2])
>>> tuple
('three', 'two', [0, 'w', 2])
>>> tuple[2][1] = 'w'              # Here you change the mutable type (list) in the tuple
                                   # , but the identity (~pointer) as seen by the tuple is still the same!

>>> tuple[1][1] = 'deux'           # Fails because string are immutable, so the id(.) would have to change
>>> tuple[2][1] = 'y'              # Works because the id in the list changes, but the id seen by the tuple, doesn't

>>> for el in tuple:               # This is what cannot change, the ids(~pointer) in the tuple!
    ...:     print(id(el))
    ...:
140640316455304
140640317363736
140640317362392
```
```python
nested_tuple = (1,2), (3, 4)           # A tuple of tuple
nested_tuple[1][1]                     # 4
nested_tuple                           # ((1, 2), (3, 4))



!!! Tuples are seen in function
def myfunc(self, *args, **kwargs) :    # args is a tuple, kwargs is a dict
                                       # args = arguments
                                       # kwargs = keyword_arguments
```

### zip

```python
#!/usr/bin/env python

names = ["Alice", "Bob", "Charlie", "Emmanuel"]
ages = [25, 30, 35]

# Using zip
zipped = zip(names, ages)            # When the iterables passed to zip() are of unequal length, it stops when the shortest iterable is exhausted.

# Converting to a list to see the output
print(list(zipped))

# [('Alice', 25), ('Bob', 30), ('Charlie', 35)]
```
```python
#!/usr/bin/env python 

names = ["Alice", "Bob", "Charlie", "Emmanuel"]
ages = [25, 30, 35]

for name, age in zip(names, ages):
    print(f"{name} is {age} years old.")

# Alice is 25 years old.
# Bob is 30 years old.
# Charlie is 35 years old.

```

```python
# Zip vs map
# Zip is more readable
# map() stops at the shortest iterable, just like ip()
# map() version is slightly slower and more awkward!
a = [1, 2, 3]
b = ['a', 'b', 'c']

z1 = list(zip(a, b))
z2 = list(map(lambda *args: args, a, b))

print(z1)  # [(1, 'a'), (2, 'b'), (3, 'c')]
print(z2)  # [(1, 'a'), (2, 'b'), (3, 'c')]
```

### Introspection

```
>>> t = (1,2)

>>> type(t)
tuple

>>> dir(t)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'count', 'index']

>>> help(t.index)

nestedtuple.index((3,4))            # Where the element can be found <!> only first level element!
1
```

--8<-- [end:body]
