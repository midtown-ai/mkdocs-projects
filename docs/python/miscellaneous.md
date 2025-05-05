title= Python Fundamentals > Miscellaneous
---
--8<-- [start:body]
## Miscellaneous

### Hello world!

```python
$ python3 --version
Python 3.9.10

$ python3
>>> print("Hello world!")             # Python 3
>>> 2+1
>>> 2*(3+4)
#!/usr/bin/env python
#!/usr/bin/env python2      # DEPRECATED
#!/usr/bin/env python3
```


### Data structure & algorithm

 Set ::

 List ::

 Map ::

 Trees ::

 Graph ::

 Big0 notiation ::

#### Check this site

 * https://csvistool.com/

 * https://csvistool.com/

 * https://csvistool.com/

### Variables scopes

#### Global variables

```python
globvar = 0

def set_globvar_to_one():
    global globvar    # Needed to modify global copy of globvar
    globvar = 1

def print_globvar():
    print(globvar)     # No need for global declaration to read value of globvar

set_globvar_to_one()
print_globvar()       # Prints 1
```

### __name__

```python
# mymodule.py
print(f"__name__ is: {__name__}")
```

```python
# main.py
import module          # Outputs __name__ is: mymodule
```
--8<-- [end:body]
