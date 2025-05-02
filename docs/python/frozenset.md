title: Python Fundamentals > Frozenset
---
--8<-- [start:body]
## Frozenset

A frozenset in Python is an immutable version of a set—once created, you cannot add or remove elements from it.

Key properties:

  * Unordered collection of unique items (like a set)
  * Immutable (unlike a set)
  * Hashable, so it can be used as a key in dictionaries or as an element in other sets

When to use:

  * When you need a set-like collection that must not change
  * When using sets as keys in a [dictionary](index.md#dictionary)

### Hands-on

```python
# Create a frozenset
fs = frozenset([1, 2, 3, 2])  # duplicates are removed

print(fs)  # Output: frozenset({1, 2, 3})

# Attempting to modify it will raise an error
fs.add(4)  # ❌ AttributeError: 'frozenset' object has no attribute 'add'

```
--8<-- [end:body]
