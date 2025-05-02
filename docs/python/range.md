title: Python Fundamentals > Range
---
--8<-- [start:body]
## Range

/// Warning | Not quite an iterator

Range are iterator-like but not iterator, because they do not keep track of their state

 * range is an iterable (not an iterator) that generates numbers lazily (when asked for it).
 * You need to call iter(range(n)) to get an iterator from it (and get the 'next' method).
///

```
r = range(3)
print(next(r))  # ❌ TypeError: 'range' object is not an iterator
```
```
r = iter(range(3))  # Creates an iterator from range   (call range.__iter__ method)
print(next(r))  # 0
print(next(r))  # 1
print(next(r))  # 2
print(next(r))  # ❌ Error! StopIteration
```

 * Using range is memory-efficient compared to storing a full list.
--8<-- [end:body]
