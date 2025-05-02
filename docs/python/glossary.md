Title: Python Fundamentals > Glossary
---
--8<-- [start:body]

## Glossary

<dfn id="concurrency"></dfn>
Concurrency

: Concurrency is concerned with managing access to shared state from different threads. Beware concurrency and parallelism are distinct concepts. Parallelism is concerned with utilizing multiple processors/cores to improve the performance of a computation. 


<dfn id="Container Object"></dfn>
Container Object

: Some objects contain references to other objects, these objects are called containers. Some examples of container-objects are a tuple, list, and dictionary. The value of an immutable container that contains a reference to a mutable object can be changed if that mutable object is changed. However, the container is still considered immutable because when we talk about the mutability of a container only the identities of the contained objects are implied.
```python
>>> t = ([1,2], [0])           # a tuple of 2 lists
>>> t[0].append(3)             # the list are mutable containers !
>>> t
([1, 2, 3], [0])
```

: But
```
>>> t[0] = 1                   # ... but the tuple is not a mutable container, so id(t[0]) cannot change !
TypeError: 'tuple' object does not support item assignment
```

: See also [Mutability](#Mutability)


<dfn id="Decorator"></dfn>
Decorator

: A function that takes a function as input and return another function! :warning: decorators wrap a function, modifying its behavior. i.e the return function is assigned to the initial function variable !
```python
my_function = my_decorator(my_function)
```

<dfn id="Global Interpreter Lock"></dfn>
Global Interpreter Lock (GIL)

: The Python threading module uses threads instead of processes. Threads run in the same unique memory heap. Whereas Processes run in separate memory heaps. This, makes sharing information harder with processes and object instances. One problem arises because threads use the same memory heap, multiple threads can write to the same location in the memory heap which is why the default Python interpreter has a thread-safe mechanism, the “GIL” (Global Interpreter Lock). This prevent conflicts between threads, by executing only one statement at a time (serial processing, or single-threading).

: The Global Interpretor Lock (GIL) in CPython prevents parallel threads of execution on multiple cores, thus the threading implementation on python is useful mostly for concurrent thread implementation in web-servers.

: More at https://blog.usejournal.com/multithreading-vs-multiprocessing-in-python-c7dc88b50b5b


<dfn id="Identity"></dfn>
Identity

: ~ pointer to memory area (memory address)??? An object as a type, value, and identity -- type and identity of the object stays constant! In Python, a reference is not directly exposed, but you can work with it using the object's memory address (id()) or weak references.
```python
>>> id([1,2])
4382416128
>>> id([1,2])
4382416128
>>> a = [1,2]               <== variable
>>> id([1,2])
4382422528
>>> id(a)                   <== variable points to the identity of the assigned object, the identity is used by variables and container objects
4382416128
```
```python
>>> s = 'hello'
>>> id(s)
4384848624
>>> sorted(s)
['e', 'h', 'l', 'l', 'o']
>>> id(s)
4384848624
>>> id(sorted(s))
4385528064
```
```python
>>> our_str ='Bonjour Monde'
>>> id(our_str)
4382424112                        <== ok
>>> our_str = 'Hello World'
>>> id(our_str)
4385028914                        <== new string, new id!
```
```python
>>> h = 'hello'
>>> w = 'world'
>>> h + ' ' + w
'hello world'
>>> id(h)
4382424112
>>> h = h + ' ' + w
>>> id(h)
4384848624
>>> h
'hello world'
```

: See also [Type](#Type)


<dfn id="Immutable"></dfn>
Immutable

: Keys in dictionaries have to be immutable (so can be hashed!) meaning only strings, numbers, frozensets, tuples, bool, range can be dictionary keys


<dfn id="Method Resolution Order"></dfn>
Method Resolution Order (MRO)

: A list of classes. The first is the object at hand, the next ones are the parent classES, followed by the grandparent classES...


<dfn id="Mutability"></dfn>
Mutability

: The value of some objects can change (an object as a type, value, and identity -- type and identity of the object stays constant!). Objects whose value can change are said to be mutable (list, dict, set can be changed after their creation); objects whose value is unchangeable once they are created are called immutable (e.g. numbers, tuples, strings, frozensets, bools, ranges)

: See also [Container Object](#Container Object)


<dfn id="Parallelism"></dfn>
Parallelism

: Parallelism is concerned with utilizing multiple processors/cores to improve the performance of a computation. Beware parallelism and concurrency are distinct concepts. [Concurrency](#Concurrency) is concerned with managing access to shared state from different threads.

<dfn id="Reference"></df>
Reference

: In Python, a reference is a name that points to an object in memory. When you assign a variable to a value, you're actually assigning a reference to that object, not copying the data itself. :warning: The variables hold references, not values
```python
a = [1, 2, 3]          # 'a' holds a reference to the list [1, 2, 3]
b = a                  # 'b' is another reference to the same list

# Both a and b reference the same list in memory.
# Modifying one affects the other.

b.append(4)            # Modify the list using the 'b' variable

print(a)               # [1, 2, 3, 4]
print(b)               # [1, 2, 3, 4] (same list)
```
```python
a = [1, 2, 3]
b = a.copy()           # Creates a new list (a shallow copy)
                       # similar to a[:] ?

b.append(4)            # Modify 'b' only

print(a)               # [1, 2, 3] (original remains unchanged)
print(b)               # [1, 2, 3, 4] (new copy)
```
```python
x = [10, 20, 30]
y = x                  # y references the same object

print(id(x) == id(y))  # ✅ True (same object)
```
```python
z = x.copy()
print(id(x) == id(z))  # ❌ False (different objects) <-- different object because different memory space!
```
```python
a = 100
b = 100
print(id(a) == id(b))  # ✅ True (same reference)

x = "hello"
y = "hello"
print(id(x) == id(y))  # ✅ True (Python reuses string literals)
```

<dfn id="Thread"></dfn>
Thread

: Multiple threads live in the same process in the same space, each thread will do a specific task, have its own code, own stack memory, instruction pointer, and share heap/virtual memory. If a thread has a memory leak it can damage the other threads and parent process. 

: See also [Global Interpreter Lock](#Global Interpreter Lock)


<dfn id="Type"></dfn>
Type

: Example
```python
>>> type((1,2))
<class 'tuple'>
>>> type('hello')
<class 'str'>
```

: See also [Identity](#Identity)

<dfn id="Value"></dfn>
Value

: See also [Identity](#Identity) and [Type](#Type)

--8<-- [end:body]
