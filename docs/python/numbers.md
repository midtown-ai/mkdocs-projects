Title: Python Fundamentals > Numbers
---
--8<-- [start:body]

## Numbers

/// Warning | Numbers are immutable!

so are strings, tuples, etc.

But beware: it is the content that is immutable, the variable that points to this content can still change!

///


```python
0
1
1.2
34.56
-56.3

>>> a = 1
>>> id(1)
4329177328
>>> id(a)
4329177328

>>> a = 256                               # Variable is pointing to the identity of another immutable number!
>>> id(256)                               # If you take a higher number, the id can change !!!!
4329185488
>>> id(a)
4329185488
```

More About (im)mutability @ https://towardsdatascience.com/https-towardsdatascience-com-python-basics-mutable-vs-immutable-objects-829a0cb1530a

### integer and float ###

```python
5 / 2 == 2.5                        # Python 3 only !
5 // 2 == 2                         # Python 3 only (round) !


import math
>>> _pi = math.pi
>>> print(_pi)
3.141592653589793

>>> g1 = round(_pi,2)                 # Rounding floats
>>> print(g1)
3.14


>>> g2 = float("{1:.2f}".format(0.1234, _pi))   # Same operation with conversion through a formatted string!
                                        # float --> turn string into float
                                        # format string with element 1 in format (which is _pi!)
                                        # and format it with .2f as a float with 2 digits after the comma
>>> g
3.14
```

Source @ http://www.tutorialspoint.com/python/python_basic_operators.htm

### bitwise operation ###

 <!> Spaces added in binary value for clarity but must be removed in real python code<<BR>>
 <!> Prefix 'b' as in b"0001" ==> bytes, prefix '0b' as in 0b0001 ==> integer_coded_in_binary

```python
a = 0b 0011 1100                  # a = 60 !
b = 0b 0000 1101                  # b = 13 !
-----------------

a&b = 0b 0000 1100                 @ a AND B

a|b = 0b 0011 1101                 # a OR B

a^b = 0b 0011 0001                 # a XOR b
                                   # Note that 2^2 is not 2**2 !!

~a  = 0b 1100 0011                 # NOT a
```

Source @ http://www.tutorialspoint.com/python/python_basic_operators.htm

### byte ###

```python
two_bytes = b'\x01\x02'
number = int.from_bytes(two_bytes, byteorder='big')      # Interprets as 258 (1*256 + 2)
print(number)

number = 258
bytes_obj = number.to_bytes(2, 'big')  # Outputs: b'\x01\x02'
print(bytes_obj)
```

```python
byte1 = b'\x05'
byte2 = b'\x03'

# Extract the integer values (5 and 3)
value1 = byte1[0]
value2 = byte2[0]

# Perform arithmetic addition
sum_value = value1 + value2  # 5 + 3 = 8
print(sum_value)  # Outputs: 8

# Optionally, convert the result back to a bytes object (if it fits in one byte)
result_byte = sum_value.to_bytes(1, 'big')
print(result_byte)  # Outputs: b'\x08'
```

### introspection ###

```python
>>> i = 17
>>> type(i)
<class 'int'>

>>> dir(45)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'as_integer_ratio', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']

>>> help(int.to_bytes)
... shows method descriptor ...

>>> i.to_bytes(2,"big")        # 2-byte representation
                               # 'big', the most significant byte is at the beginning of the byte array.
b'\x00\x11'

>>> i.to_bytes(4,"big")
b'\x00\x00\x00\x11'
>>> i.to_bytes(4,"little")
b'\x11\x00\x00\x00'
```

--8<-- [end:body]

