title: Python Fundamentals > List
---
--8<-- [start:body]
## List

/// Warning | Indexed to 0

 * Lists are indexed to 0
 * First element in the list is at index 0 !!!
///

### Hands-on

/// Warning | How do you copy a list?

You do NOT copy a list with 'list_0 = list_1', but with  'list0 = list1[:]' for shallow copies and 

```
import copy

lst = [[1, 2], [3, 4]]       # A list of mutable elements!
deep = copy.deepcopy(lst)    # An entirely different copy
///

```python
list_0 = [0,1]
list_0 = list(range(10))        # Python3: range is an iterator-like, but not an iterator!
id(list_0)                      # ex: 4368873792

list_1 = list_0                 # Here you have 2 variables thet refers to the same list object, not a copy!  <-- variables points to the same identity
id(list_1)                      # ex: 4368873792


list_1[2] = 'X'                 # Changing one will change the other!
list_0                          # [0, 1, 'X', 3, 4, 5, 6, 7, 8, 9]

list_1 = list_0[:]              # This is how to copy a list!     <-- 2 different identities!
list_1[3] = 'Y'                 # Will NOT change what list_0 is pointing to! If you change one, you do NOT change the other!
list_1                          # [0, 1, 'X', 'Y', 4, 5, 6, 7, 8, 9]

list_0                          # [0, 1, 'X', 3, 4, 5, 6, 7, 8, 9]
```
```
a = range(10)                       # range(0,10) or 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
a
b = range(1,11)                     # range(1, 11) or 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
b
c = range(30,20,-1)                 # range(30, 20, -1) or 30, 29, 28, ..., 22, 21
c


>>> square=[i**2 for i in a]            # List comprehension
>>> square=[i**2 for i in range(10)]

["Even" if x % 2 == 0 else "Odd" for x in range(5)]    # ['Even', 'Odd', 'Even', 'Odd', 'Even']


✅ More Readable: Less boilerplate than loops.
✅ Faster: Optimized for performance compared to for loops.
✅ Memory Efficient: Combined with generators, it can reduce memory usage. (generators create values as they are read instead of first and then reading them from memory (as with regular lists)
```

 . <!> <<Highlight("What is the difference between .append and .extend?")>>

```python
>>> l1 = [1, 2]
>>> l2 = [3, 4]
>>> l2 == l2[:] == l2[::]           # Same
True
>>> l1.extend(l2)                   # Concat the 2 lists and modify one of them in-place ! Here, l1 will be modified!
                                    # Same as list_1 += list_2 !!   <-- also list_1 keep the same id !!!
>>> l1
[1, 2, 3, 4]
>>> l1.append(l2)                   # Append 1 element at the end of the list (l1 is modified)
>>> l1
[1, 2, 3, 4, [3, 4]]

>>> l1.insert(0,"Yes")              # In-place insert at the beginning of the list ~ pre-pend!
                                    # The opposite of append!
>>> l1[0]
Yes
>>> l1                              # Note that insert does NOT replace! (unlike l[0] = 'No' would!)
['Yes', 1, 2, 3, 4, [3, 4]]]

>>> a = 5
>>> l3 = [1, 2, 3]
>>> [a] + l3                        # Insert at the beginning with '+'
                                    # Almost same as .extend, except the original list is not changed in place!
[5, 1, 2, 3]
```
```
>>> list = [1, 'deux', {'trois': 3 } ]  # A list doesn't require its elements to be different
>>> list = ['the','holy','grail']   # List ~ array are represented with square brackets
>>> nested_list = [ 'XXX', list]    # One of the elements of the list is a list
>>> 'XXX' in nested_list            # Check list membership
True


# The returned lists are not the original list (ie different id)
# You cannot do l[1:].remove(3) and update the list l
>>> my_list[:]                      # The whole list
>>> my_list[0:]                     # The whole list (same as above)
>>> my-list[0:len(my_list)]         # The whole list (same as above)
>>> my_list[::1]                    # The whole list (same as above)
>>> my_list[2:]                     # From 3rd element to end
>>> my_list[2:-2]                   # From 3rd element to 2nd before last
>>> my_list[-1:] = [9]              # from the last element to the end
>>> my_list[-2:] = [8, 9]
>>> my_list[:-2:] = [0, 1, 2, 3, 4, 5, 6, 7]

>>> nested_list[1] = 'awesome'      # List are mutable!
>>> my_list.append('for sure')      # append 1 element only
>>> my_list.append(another_list)    # 'another_list' is placed at the end of the list as a single element
>>> my_list.insert(1,'super')       # inserting of an element without deletion
>>> my_list.remove('super')         # remove the FIRST 'super' entry from the list
>>> my_list = [x for x in my_list if x != 'super']  # remove all the 'super' entry

>>> my_list.extend(another_list)    # contact the 2 lists like the + operation, but my_list is changed in place!

>>> my_list.extend(another_list)      # contact the 2 lists like the + operation and change in place my_list !
>>> my_list = my_list + another_list  # same as above
```
```
>>> myList.index("revolves")
3
>>> "revolves" in myList
True
>>> my_list.index("a")
Exception ValueError: 'a' is not in list
```
```
token = string.split('\t')      # Split on tab only
token = string.split()          # Split on any space character
```
```python
# Remove all the elements with a given value between 2 indexes of a list
def remove_between_indexes(lst, start, end, value):
    return lst[:start] + [x for x in lst[start:end] if x != value] + lst[end:]

# Example list
my_list = ["keep", "remove_me", "keep", "remove_me", "keep", "remove_me", "keep"]

# Remove 'remove_me' between index 1 and 5
new_list = remove_between_indexes(my_list, 1, 5, "remove_me")

print(new_list)
```

### function with list parameter

```
len(lst)             - length of the list
sorted(lst)          - <!> lst.sort()  <== sort in place, but sorted(lst) sort the output
sum(lst)             - sum of all the element of the list
                     - <!> add to 0, so must be a number and not char/str/etc. !
lst[::-1]            - <!> l.reverse() <== reverse in place, but lst[::-1] reverse the output only!
 ...
```

### sorting

 . <<Highlight("what is the difference between 'sorted(lst)' ans 'lst.sort()' ? ")>>
 * lst.sort change the list in place, while sorted doesn't!
 * lst.sort can also use a function to sort the element of he list. see below
 <<P>>
 . <!> sort numbers first and then string ! ( = use LSD Radix sort first and then MSD Radix sort?)

#### sorted(lst)

 . <!> Deprecated? Use lst.sort() instead of sorted(l) ? No, lst.sort() = sort in place while sorted(lst) does not change lst!

```
sorted(range(30,20,-1))                                        # Turn range into a list and sort in numerical order

>>> sorted(["a", "b", "ab", "z", "tutu", "aaa", "0", "2"])     # Sort in alphabetical/dictionary order
['a', 'aaa', 'ab', 'b', 'tutu', 'z']

>>> sorted([1, 2.3, 0.99, -23])                                # Sort in numerical/incremental order
[-23, 0.99, 1, 2.3]

>>> sorted([1, 2, 3, 4, 'a', 'b', 2.4, 3])              # Python3 raise an exception
TypeError: unorderable types: str() < int()
```

```
# Sorting list of tuples use the first element of the tuple
>>> l = [ ('a',34), ('z', 23), ('b', 44)]
>>> sorted(l)
[('a', 34), ('b', 44), ('z', 23)]

# Sort based on 2nd field of tuple ~~~> reverse tuple
>>> l = sorted(list(map(lambda el: el[::-1], l)))
>>> sorted(l)
[(23, 'z'), (34, 'a'), (44, 'b')]
```

#### lst.sort

 . <!> Inplace sorting ! Not lie l2 = l1.sort() ... like sorted?

```
lst.sort()         # Like sorted, but change the list in place

lst.sort(reverse=True)     # Sort in reverse order!

>>> list1=[[3,5,111],[16,23,21],[1,2,3,4],[100,1,31,12]]
>>> list1.sort(key=lambda x:x[1], reverse=True)                         # Sort based on a value extracted from each element/x!
[[16, 23, 21], [3, 5, 111], [1, 2, 3, 4], [100, 1, 31, 12]]


>>> list1=[[100,200,300,400,500],[100,200,300],[100,150,200,400]]
>>> list1.sort(key=len)                                                 # using a FUNCTION REFERENCE to sort the elements, here the length function of the element
print(list1)
[[100, 200, 300], [100, 150, 200, 400], [100, 200, 300, 400, 500]]


list1=[[10,200,300,40,500],[100,200,300],[100,150,200,400]]
list1.sort(key=sum)                                                     # using the key as sum on the element      sum([1,2]) == 3
print(list1)
[[100, 200, 300], [100, 150, 200, 400], [10, 200, 300, 40, 500]]
```

### map : Operation on every element of a list

 * map() is used to execute a function on all the element of a list
 * map() can also be used to work on multiple lists at once (list zip())
 * if map() is using only one list as input, it can be done with a list comprehension!
 * :warning: the output of map(...) is a map and not a list!

```
l = list(range(9))                  # Python3: Turn the iterator-like range into a list
l = list(map(str, range(9))         # Python3: Turn the map object into a list

l = [ ('a',34), ('z', 23), ('b', 44)]
r = list(map(lambda el: el[::-1], l))    # [(34, 'a'), (23, 'z'), (44, 'b')]
print(r)
[(44, 'b'), (23, 'z'), (34, 'a')]

# Map with a function instead of a lambda!
def my_function(value):
    """ Double provided value """
    return value + value

my_values = (1, 2, 3, 4)                # Can be a tuple or a list
res = list(map(my_function, my_values))

res = list(map(lambda v: v + v, my_values))   # Map with a lambda function !

>>> d                                   # beware list of chars, not index --> string multiplication!
['0', '1', '2', '3', '4', '5', '6', '7', '8']
>>> [ x*2 for x in d ]
['00', '11', '22', '33', '44', '55', '66', '77', '88']


# List of strings
list_of_strings = ['sat', 'bat', 'cat', 'mat']

# map() can listify the list of strings individually
test = list(map(list, list_of_strings))
test                                    # returns [['s', 'a', 't'], ['b', 'a', 't'], ['c', 'a', 't'], ['m', 'a', 't']]
```
```
s = 'hello world'
lc = list(s)

>>> [ el.upper() for el in lc]
['H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D']

>>> list(map(lambda el: el.upper(), lc))
['H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D']

```

### Working with 2 lists together (map)

```python
# Add two lists using map and lambda

x_values = [1, 2, 3]
y_values = [4, 5, 6]

result = map(lambda x, y: x + y, x_values, y_values)
```


#### iteration on the elements of a list

```python
help(list.insert)
insert(self, index, object, /)
    Insert object before index.
```
```python
ordered_words = ['aa', 'bb', 'ee', 'hh']
words = 'aaa,ddd'


def insert_word(word, ordered_words):
    """ change ordered_words in place """
    for i, el_word in enumerate(ordered_words):
        if word < el_word:                        # Inequality on strings, sort based on ASCII characters' code! One by one chars
            ordered_words.insert(i, word)         # Equivalent to ordered_words = ordered_words[:i] + [word] + ordered_words[i:]
            break
    return(true)




words = arg_w.split(',')

for w in words:
    insert_word(w, ordered_words)

print ordered_words
```

### Introspection

```python
>>> l
[9, 7, 5, 3, 1]

>>> type(l)
list

>>> dir(l)
>>> dir(list)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']

>>> help(list.extend)
extend(self, iterable, /)
    Extend list by appending elements from the iterable.
```


--8<-- [end:body]
