title: Python Fundamentals > Set
---
--8<-- [start:body]
## Set

Sets are Unordered immutable elements with no duplicate.

Sets are mutable

What is a set:

  * Every element in set is unique (no duplicates)
  *  Sets can be used to perform mathematical set operations like union, intersection, symmetric difference etc.
  * :warning: Every element in set must be immutable (which cannot be changed) like strings, numbers, tuple, or range, however, the set itself is mutable. We can add or remove items from it.

More at @ https://www.thegeekstuff.com/2019/04/python-set-examples/#more-17819

### Hands-on

```
Months={"Jan", "Feb", "Mar", "Feb"}                  # Will remove 1 "Feb" because not unique!
Dates={21,22,17}

>>> type(Dates)
set

Days = set(["Mon","Tue","Wed","Thu","Fri","Sat","Sun"])   # Turn a list in a set

>>> cars = ['honda','ford','dodge', 'honda']            # List
>>> autos = set(cars)                                   # Create a set from a list
>>> autos
set(['dodge',chevy','honda', 'ford'])
>>> motos & autos                                       # intersection of sets
>>> employees = engineers | programmers | managers      # union of sets
>>> engineering_management = engineers & managers       # intersection of sets
>>> managers_only = employeses - engineers - programmers  # difference of sets
```
```python
s.update(t)	                  # s |= t  return set s with elements added from t
s.intersection_update(t)          # s &= t  return set s keeping only elements also found in t
s.difference_update(t)	          # s -= t  return set s after removing elements found in t
s.symmetric_difference_update(t)  # s ^= t  return set s ...
                                  # ... with elements from s or t but not both

s.add(x)	   # add element x to set s (if x is not already there! If already there, tihs is a no-op!)
s.remove(x)        # remove x from set s; raises KeyError if not present
s.discard(x)	   # removes x from set s if present (no exception)
s.clear()          # remove all elements from set s

s.pop()            # remove and return an arbitrary element from set s ...
                   # ... raises KeyError if empty
```

Source @ [[https://docs.python.org/2/library/sets.html||target='_blank']]

### Introspection

```
>>> s = set()
>>> type(s)
set

>>> dir(s)
>>> dir(set)
['__and__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__iand__', '__init__', '__ior__', '__isub__', '__iter__', '__ixor__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__or__', '__rand__', '__reduce__', '__reduce_ex__', '__repr__', '__ror__', '__rsub__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__xor__', 'add', 'clear', 'copy', 'difference', 'difference_update', 'discard', 'intersection', 'intersection_update', 'isdisjoint', 'issubset', 'issuperset', 'pop', 'remove', 'symmetric_difference', 'symmetric_difference_update', 'union', 'update']

>>> help(set.update)
update(...)
    Update a set with the union of itself and others.
```

--8<-- [end:body]
