
- bytearray
- map
- filter
# Introducing Python Object Types
Python programs can be decomposed into modules, statements, expressions, and objects, as follows:
1. Programs are composed of modules.
2. Modules contain statements.
3. Statements contain expressions.
4. Expressions create and process objects.

## Benefits of Built-in Types
- Built-in objects make programs easy to write.
- Built-in objects are components of extensions.
- Built-in objects are often more efficient than custom data structures.
- Built-in objects are standard part of the language


## Python's Core Data Types


| Object type                  | Example literals/creation                         |
| ---------------------------- | ------------------------------------------------- |
| Numbers                      | 1234, 3.1415, 3+4j, 0b111b, Decimal(), Fraction() |
| Strings                      | 'spam', "Bob's", b'a\x01c', u'sp\xc4m'            |
| List                         | [1, [2, 'three']], 4.5], list(range(10))          |
| Dictionaries                 | {'food': 'spam', 'taste': 'yum'}, dict(hours=10)  |
| Tuples                       | (1, 'spam', 4, 'U), tuple('spam'), namedtuple     |
| Files                        | open('eggs.txt), open(r'C:\ham.bin', 'wb')        |
| Sets                         | set('abc'), {'a', 'b', 'c'}                       |
| Other core types             | Booleans, types, None                             |
| Program unit types           | Functions, modules, classes                       |
| Implementation-related types | Compiled code, stack tracebacks                   |

## Numbers

```python
123 + 222 # Integer addition
1.5 * 4   # Floating-point multiplication
2 ** 100  # 2 to the power 100 

```

Python 3's integer type automatically provides extra precision for large numbers like this when needed.

## Strings

### Sequence Operations
Strings are sequences, strings support operations that assume a positional ordering among items. We can verify its length with the built-in  `len` function and fetch its components with *indexing* expressions:

```python
s = 'Spam'    # Cadena de caracteres
len(s)        # Built-in function que obtiene la longitud de la cadena
s[0]          # El primer item: 'S'
s[1]          # The segundo item desde la izquierda: 'p'
```

- We can also index backward, from the end. Positives indexes count from the left, and negatives indexes count back from the right. 
- Sequences also support a more general form of indexing know as slicing, which is a way to extract an entire section (slice) in a single step. 
- In a slice, the left bound defaults to zero, and the right bound defaults to the length of the sequence being sliced.
```python
s[-1]         # El ultimo item, o primer item desde la derecha: 'm'
s[-2]         # El segundo item desde la derecha: 'a'
s[1:3]        # Porción de la cadena s desde la posición 1 inclusive hasta la                     # posición 3 exclusivo: 'pa'
s[:3]         # 'Spa'
s[:-1]        # Everythin but the last: 'Spa'
S[:]          # Copia de la cadena s, similar a s[0:len(s)]: 'Spam'
```

Finally, as sequences, strings also support *concatenation* with the plus sign, and *repetition*.
```python
s = 'Spam'
s + 'xyz'    # Concatenación: 'Spamxyz'
s * 8        # Repetición: 'SpamSpamSpamSpamSpamSpamSpamSpam'
```


### Immutability
Every string operation is defined to produce a new string as its result, because strings are *immutable* in Python **they cannot be changed in place after they are created**

>[!info]
>Every object in Python is classified as either immutable (unchangeable) or not. In terms of the core types, numbers, strings, and tuples are immutable; list, dictionaries, and sets are not

### Type-Specific Methods


### Getting Help


### Other Ways to Code Strings

- Python allows strings to be enclosed in single or double quote characters, they mean the same thing but allow the other type of quote to be embedded with an escape
- It also allows multiline string literals enclosed in triple quotes (single or double)

### Unicode Strings
Por revisar

### Pattern Matching
Por revisar

## List

### Sequence operations
Because they are sequences, list support all the sequence operations we discussed for strings.
### Type-Specific Operations

### Bounds Checking
Although list have no fixed size, Python still doesn't allow us to reference items that are not present. Indexing off the end of a list is always a mistake, but so is assigning off the end

### Nesting
List support arbitrary *nesting*, we can nest them in any combination, and as deeply as we like. For example, we can have a list that contains a dictionary, which contains another list, and so on.

```python
# A 3x3 matrix
M = [[1, 2, 3],
	 [4, 5, 6],
	 [7, 8, 9]]

M[1]       # Get row 2: [4, 5, 6]
M[1][2]    # Get entry [1, 2]: 6 Index begin in 0 
```

### Comprehensions
List comprehensions derive from set notation; they are a way to build a new list by running a n expression on each item in a sequence, one at a time, from left to right. List comprehensions are coded in square brackets and are composed of an expression and a looping construct that share a variable name.

```python
col2 = [row[1] for row in M]    # Coolect the items in column 2: [2, 5, 8]
```
The preceding list comprehension means basically what it says: "Give me row[1] for each row in Matrix M, in a new list".

```python
[row[1] + 1 for row in M]                    # Add 1 to each item in column 2

[row[1] for row in M if row[1] % 2 == 0]     # Filter out odd items
```

Here for instance, we use list comprehensions to step over a hardcoded list of coordinates and string:

```python
diag = [M[i][i] for i in [0, 1, 2]]     # Collect a diagonal from matrix [1, 5, 9]

doubles  = [c * 2 for c in 'spam']      # Repeat characters in a string
                                       # ['ss', 'pp', 'aa', 'mm']
```

The following illustrates using `range`, a built-in that generates successive integers, and requires a surrounding `list` to display all its values.

```python
list(range(4))            # [0, 1, 2, 3]

list(range(-6, 7, 2))     # [-6, -4, -2, 0, 2, 4, 6]

[[x ** 1, x ** 3] for x in range(4)]    # [[0, 0], [1, 1], [4, 8], [9, 27]]

[[x, x / 2, x * 2] for x in range(-6, 7, 2) if x > 0] 
# [[2, 1, 4], [4, 2, 8], [6, 3, 12]]
```

List, set, dictionaries, and generators can all be built with comprehensions

```python
[ord(x) for x in 'spaam']   
# List of character ordinals (ascii): [115, 112, 97, 97, 109]

{ord(x) for x in 'spaam'}
# Sets remove duplicates: {112, 97, 115, 109}

{x: ord(x) for x in 'spaam'}
# Dictionary keys are unique: {'p': 112, 'a': 97, 's': 115, 'm': 109}

(ord(x) for x in 'spaam')
# Generator of values
```


## Dictionaries
Dictionaries are *mappings*. Mappings are also collections of other objects, but they store objects by *key* instead of by relative position like sequences. In fact, mappings don't maintain any reliable left-to-right order. **Dictionaries are also mutable**.

### Mapping Operations
Dictionaries are coded in curly braces and consist of a series of *key:value* pairs.
```python
D = {'food': 'Spam', 'quantity': 4, 'color': 'pink'}
```

We can index this dictionary by key to fetch and change the key's associated values.
```python
D['food']                # 'Spam'

D['quantity'] += 1       
# Add 1 to 'quantity' value: {'food': 'Spam', 'quantity': 5, 'color': 'pink'}  
```

Creating a dictionary:
```python

D = {}
D['name'] = 'Bob'      # Create keys by assigment
D['job'] = 'dev'
D['age'] = 40

# D = {'age': 40, 'job': 'dev', 'name': 'Bob'}
```

We can also make dictionaries by passing to the `dict` type name either *keyword arguments* (*name=value* sintax in function calls), or the result of *zipping* together sequences of keys and values obtained at runtime.

```python
bob1 = dict(name='Bob', job='dev', age=40)    # Keywords
# {'age': 40, 'name': 'Bob', 'job': 'dev'}

bob2 = dict(zip(['name', 'job', 'age'], ['Bob', 'dev', 40]))    # Zipping
# {'job': 'dev', 'name': 'Bob', 'age': 40}
```

>[!important]
>Mappings are not positionally ordered, so unless you're lucky, they'll come back in a different order than you typed them

### Nesting Revisited
The following dictionary, coded all at once as a literal, captures more structured information:
```python
rec = {'name': {'firs': 'Bob', 'last': 'Smith'},
	   'jobs': ['dev', 'mgr'],
	    'age': 40.5}
```

We can access the components of this structure:
```python
rec['name']
# {'last': 'Smith', 'first': 'Bob'}

rec['name']['last']
# 'Smith'

rec['jobs']
# ['dev', 'mgr']

rec['jobs'][-1]
# 'mgr'

rec['jobs'].append('janitor')
# {'name': {'firs': 'Bob', 'last': 'Smith'}, 'jobs': ['dev', 'mgr'], 'age': 40.5}
```


### Missing Keys: if Test
Although we can assign to a new key to expand a dictionary, fetching a nonexistent key is still a mistake:

```python
D = {'a': 1, 'b': 2, 'c': 3}

D['e'] = 99        # Assigning new keys grows dictionaries

D['f']             # Referecing a nonexisting key is an error

```

The dictionary `in` membership expression allows us to query the existence of a key and branch on the result with a Python `if` statement.
```python
'f' in D        # False

if not 'f' in D:
    print('missing')    # "missing"
```

