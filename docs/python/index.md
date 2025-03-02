---
---
```python {title="Arguments from command line"}
#!/usr/bin/env python3

import sys

def main(argv):
    assert len(argv) >= 3, 'Too few parameters'
    assert len(argv) <= 1, 'No parameter to command line provided'
    print(argv)

    prog_name = argv[0]
    argument_1 = argv[1]


if __name__ == "__main__":
    main(sys.argv)
```

```python {title="The invisible dictionary problem :-)"}
# Given a list of words, group the anagram in a sublist together
# ['abc', 'bar', 'cab'] ---> [ ['cab', 'abc'], ['bar']]

def ana(L):                             # (1)
    anagrams = {}
    for word in L:
        K = ''.join(sorted(word))       # (2) !
        if K not in anagrams.keys():    # (3) !
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


## Strings (immutable)

/// warning | A string ~= immutable tuple of characters

```
"hello" ~= ('h', 'e', 'l', 'l', 'o' )
```

Well, not exactly because their types are different, one is 'str' while the other is 'tuple'.
They are also different objects, with different methods!

```python
type('hello')                       # <class 'str'>
type(('h', 'e', 'l', 'l', 'o'))     # <class 'tuple'>

```
///

### fundamentals

```python
# <!> sorted(string) return a sorted list of characters contained in string
# <!> This list needs to be turned into a string using join()!
ordered_chars_LIST = sorted(string_of_unordered_chars)       # returns an ordered LIST or characters , not a string but a LIST!
ordered_chars = ''.join(sorted(unordered_chars))   # Order a string (anagram)


string1 = "this is a string"
string2 = "%s! %s" % ("hello","toto")                             # Print a string in a string!
string3 = "%(h)s! %(n)s" % { "n":"toto", "h":"hello"}             # Using named variable from a dictionary (great for templating!)

string4 = "a number y is {1:.2f} and x is {0:.3f}".format(x, y)   # order from tuple followed by format!

price = 4.55
string5 = f"Price in Swiss Franks: {price * 1.086:5.2f}"          # String literal <!> 'price' variable must exists
                                                                  # Don't forget the 'f' at the beginning of the string!

str(3210)                                  # Convert number to string '3210'
str("hello")                               # Convert a string into a string, i.e. do nothing!

float("3.1415")                            # Turn a string to float
int("3")                                   # Turn a string to a integer
# int("3.1415")                            # <!> This is an error as this is a float
int(float("3.14"))                         # <!> Ok, this works! ;-) and is 3

string3 = string1 + string2                # Concatenation operation
multiline = "This is a \n\
... multiline string"                      # Multiline string
#comment
len(var3)                                  # Length of a string


print(program, "arguments")                # Python3
print(program, "arguments", sep=" ", end="\n")    # Python3 equivalent = Concat 2 strings with a space in between + CR at the end


>>> list("hello world")                    # A string = tuple of chars --> turn a tuple of char into a list!
['h', 'e', ...., 'o', ' ', 'w', ..., 'd']

# <!> Strings are immutable, but here you are just changing where the variable points to, not the string
s = s.lstrip()                             # Remove leading spaces
s = s.rstrip()                             # Remove trailing spaces and CARRIAGE RETURNS
s = s.strip()                              # Remove leading and trailing spaces and CARRIAGE RETURNS

title = title.strip(',.-\n')               # Remove leading and trailing characters
                                           # <!> Will strip any of those characters, not the string ",.-" but individual characters!

number_of_ts = s.count('t')                # Return number of character 't' in the string
number_of_totos = s.count('toto')          # Return number of substrings

pos_of_first_t = s.find('t')
pos_of_second_t = s.find('t', pos_of_first_t)     # Find returns the index of first found 't' (or second t since starting from 1st 't' position)
                                                  # If find reaches the end, then returns -1

s.capitalize()
s.join()
s.split()                    # Split on any-block of spaces/tabs
                             # , e.g. "12    3 4" --> ['12', '3', '4']
# s.split('')                # <!> but this ~~~> ValueError: empty separator!
# s.split("")                # <!> but this ~~~> ValueError: empty separator!
s.split("\t")                # split on tab characters (\t is the tab character, not 2 chars!)
s.split(" ")                 # split on space charactes only, not tabs!
"hello world".split("wo")    # split on a GROUP of characters <!> Not like strip, which assume individual characters
"arn::account::region".split("::")    # returns a list!

# Replace = split and join?
arn = "arn::account::region"
arn = "XX".join(arn.split("::"))
=?= arn.replace("::","XX")            # ?

>>> s.translate(None, ",!.;")          # Remove unwanted characters, here the punctuation

>>> "Python".center(10)
'  Python  '

s.endswith('toto')
s.startswith('toto')

s = "one\ttwo\t\tthree\nfout"      # Tabs and other special characters in a string
print(s)                           # Transform tabs and other special characters

string_content = "line 1\nline 2\nline 3\n"
string_file_content.splitlines()             # ~ s.split('\n') ?
[ 'line 1', 'line 2', 'line 3']

>>> account_number = "43447879"
>>> account_number.zfill(12)             # Zero fill
'000043447879'
>>> account_number.rjust(12,"0")         # Right justification
'000043447879'

                                         # <!> Immutability: can only be read
string[0]                                # first character
string[-1]                               # very last character
string[1:4]                              # a slice
string[10:]                              # a slice to end of string
string[:-1]                              # everything but last character
string[:]                             # copy of string
string[::1]                           # copy of string, step of 1 (default)
string[::2]                           # print every other characters!
string[::-1]                          # reverse string, step of -1

string[::-2]                          # reverse string + take every other characters

s = " a very long string ..... "         # pep8 compliance for long string
s =(
  "a very long"
  "string ... "
)

s = """
    A multi-line string
    With space as well
and carriage returns
"""

s                      # '\n    A multi-line string\n    With space as well\nand carriage returns\n'

print(s)                # 
                        #   A multi-line string
                        #   With space as well
                        # and carriage returns
```
