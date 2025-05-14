
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

Other ways to avoid accessing nonexistent keys in dictionaries.

- The `get` method
```python
# get method
value = D.get('x', 0)        # Index but with a default
# value = 0
```

- The `if/else ternary` expression:
```python
# If/else ternary
value = D['x'] if 'x' in D else 0
# value = 0
```


### Sorting Keys: for Loops
**Dictionaries are not sequences**, they don't maintain any dependable left-to-right order.
The `sorted` call returns the result and sorts a variety of objects types, in this case sorting dictionaries keys automatically:
```python
# D = {'a': 1, 'b': 2, 'c': 3}D = {'a'}
for key in sorted(D):
    print(key, '=>', D[key])

# a => 1
# b => 2 
# c => 3
```

### Iteration and Optimization
An object is *iterable* if is either a physically stored sequence in memory or an object that generates one item at a time in the context fo an iteration operation ("virtual sequence"). Both types of objects are considered iterable because they support the *iteration protocol*, they respond to the **iter** call with an object that advances in response to **next** calls and raises an exception when finished producing values.

Every Python tool that scans an object from left to right uses the iteration protocol.

Any list comprehension expression, such as this one, which computes the squares of a list of numbers:
```python
squares = [x ** 2 for x in [1, 2, 3, 4, 5]] 
# squares [1, 4, 9, 16, 25]
```
 
 Can always be coded as an equivalent for loop that builds the result list manually by appending as it goes:
```python
squares = []
for x in [1, 2, 3, 4, 5]: 
	squares.append(x ** 2)
# squares [1, 4, 9, 16, 25]
```

The list comprehension, though, and related functional programming tools like map and filter, will often run faster than a for loop today on some types of code (perhaps even twice as fast)—a property that could matter in your programs for large data sets.

## Tuples
Tuples are sequences, like lists, but they are immutable, like strings. Functionally, they’re used to represent fixed collections of items. Syntactically, they are normally coded in parentheses instead of square brackets, and they support arbitrary types, arbitrary nesting, and the usual sequence operations:

```python
T = (1, 2, 3, 4)
len(T)
# 4

T + (5, 6)            # Concatenation
# (1, 2, 3, 4, 5, 6)

T[0]                  # Indexing, slicing and more
# 1
```

Tuples also have type-specific callable methods.
```python
T.index(4)
# 3

T.count(4)
# 1
```

Like lists and dictionaries, tuples support mixed types and nesting, but they don’t grow and shrink because they are immutable (the parentheses enclosing a tuple’s items can usually be omitted, as done here): 
```python
T = 'spam', 3.0, [11, 22, 33]
T[1] 
# 3.0
T[2][1] 
# 22
T.append(4) 
# AttributeError: 'tuple' object has no attribute 'append'
```

## Files
They can be used to read and write text memos, audio clips, Excel documents, saved email messages, and whatever else you happen to have stored on your machine. The is no specific literal syntax for creating them.  Rather to create a file object, you call the built-in `open` function, passing in an external filename and an optional processing mode as strings.

```python
f = open('data.txt', 'w')    # Make a new file in output mode ('w' is write)
f.write('Hello\n')
# 6                          # Devuelve el numero de items escritos
# 6
f.write('world\n')
f.close()                    # Close to flush output buffers to disk        
```

This creates a file in the current directory and writes texto to it. 
```python
f = open('data.txt')        # 'r' (read) is the default processing mode
text = f.read()
# text = 'Hello\nworld\n'
```


### Binary Bytes Files
Por revisar
### Unicode Text Files
Por revisar
## Other Core Types

**Sets**
Sets are unordered collections of unique and immutable objects.
```python
X = set('spam')        # Make a set out of a sequence with built-in function
Y = {'h', 'a', 'm'}    # Make a set with set literals

X & Y         # Intersection
# {'m', 'a'}

X | Y         # Union
# {'m', 'h', 'a', 'p', 's'}

X - Y         # Difference
# {'p', 's'}

X > Y        # Superset
# False

{n ** 2 for n in [1, 2, 3, 4]} # Set comprehensions
```

Set also support `in` membership test like all others collection types
```python
'p' in set('spam'), 'p' in 'spam', 'ham' in ['eggs', 'spam', 'ham']
# (True, True, True)
```


**Decimal** and **fractions**
Decimal numbers are fixed precision floating-point numbers and *fraction numbers* are rational numbers with a numerator and denominator

```python
1 / 3                           # Floating-point
# 0.333333333

import decimal                  # Decimals: fixed precision
d = decimal.Decimal('3.141')
d + 1
# Decimal('4.141)

decimal.getcontext().prec = 2
decimal.Decimal('1.00') / decimal.Decimal('3.00')
# Decimal('0.33)
```

```python
from fractions import Fraction
f = Fraction(2, 3)
f + 1
# Fraction(5, 3)
f + Fraction(1, 2)
# Fraction(7, 6)
```

**Booleans**
```python
1 > 2, 1 < 2
# (False, True)

bool('spam')
# True
```

**None** commonly used to initialize names and objects
```python
X = None             # None placeholder
print(X)
# None
```


### How to Break Your Code's Flexibility
Leído
### User-Defined Classes
Leído

# Numeric Types

## Numeric Type  Basics

### Numeric Literals


| Literal                             | Interpretation                       |
| ----------------------------------- | ------------------------------------ |
| 1234, -24, 0, 999999999999          | Integers (unlimited size)            |
| 1.23, 1., 3.14e-10, 4E210, 4.0e+210 | Floating-point numbers               |
| 0o177, 0x9ff, 0b101010              | Octal, hex, and binary literals      |
| 3+4j, 3.0+4.0j, 3J                  | Complex numbres literals             |
| set('spam'), {1, 2, 3, 4}           | Sets construction forms              |
| Decimal('1.0'), Fraction(1,3)       | Decimal and fraction extension types |
| bool(X), True, False                | Boolean type and constants           |

**Hexadecimal, octal, and binary literals** 
- Integers may be coded in decimal (base 10), hexadecimal (base 16), octal (base 8), or binary (base 2), the last three of which are common in some programming do mains. Hexadecimals start with a leading ``0x`` or ``0X``, followed by a string of hexadecimal digits (0–9 and A–F). Hex digits may be coded in lower- or uppercase. Octal literals start with a leading ``0o`` or ``0O`` (zero and lower- or uppercase letter o), followed by a string of digits (0–7).
- Note that all of these literals produce integer objects in program code; they are just alternative syntaxes for specifying values. The built-in calls ``hex(I)``, ``oct(I)``, and ``bin(I)`` convert an integer to its representation string in these three bases, and ``int(str, base)`` converts a runtime string to an integer per a given base.

```python
num = 28

hex(a)
# '0x1c'
int('0x1c', 16)
# 28

oct(a)
# '0o34'
int('0o34', 8)
# 28

bin(a)
# '0b11100'
int('0b11100', 2)
# 28
```

**Complex numbers**
Python complex literals are written as *real part+imaginary part*, where the imaginary part is terminated with a j or J. The real part is technically optional, so the imaginary part may appear on its own. Internally, complex numbers are implemented as pairs of floating-point numbers, but all numeric operations perform complex math when applied to complex numbers. Complex numbers may also be created with the ``complex(real, imag``) built-in call

### Built-in Numeric Tools
Leído
### Python Expressions Operator
Examples: `%` computes a division remainder, `<<` performs a bitwise left-shift, `&` computes a bitwise **AND** result, and so on. The `is` operator test object identity (i.e., address in memory, a strict form of equality) and `lambda` creates unnamed functions

| Operador                       | Descripción                                                         |
| ------------------------------ | ------------------------------------------------------------------- |
| `yield x`                      | Generador de función, protocolo send                                |
| `lambda args: expression`      | Generación de función anónima                                       |
| `x if y else z`                | Selección ternaria (x se evalúa solo si y es verdadero)             |
| `x or y`                       | OR lógico (y se evalúa solo si x es falso)                          |
| `x and y`                      | AND lógico (y se evalúa solo si x es verdadero)                     |
| `not x`                        | Negación lógica                                                     |
| `x in y, x not in y`           | Membresía (iterables, conjuntos)                                    |
| `x is y, x is not y`           | Pruebas de identidad de objeto                                      |
| `x < y, x <= y, x > y, x >= y` | Comparación de magnitudes, subconjunto y superconjunto de conjuntos |
| `x == y, x != y`               | Operadores de igualdad de valor                                     |
| `x \| y`                       | OR a nivel de bits, unión de conjuntos                              |
| `x ^ y`                        | XOR a nivel de bits, diferencia simétrica de conjuntos              |
| `x & y`                        | AND a nivel de bits, intersección de conjuntos                      |
| `x << y, x >> y`               | Desplazamiento de x a la izquierda o derecha por y bits             |
| `x + y`                        | Adición, concatenación;                                             |
| `x - y`                        | Sustracción, diferencia de conjuntos                                |
| `x * y`                        | Multiplicación, repetición;                                         |
| `x % y`                        | Resto, formato;                                                     |
| `x / y, x // y`                | División: verdadera y de piso                                       |
| `-x, +x`                       | Negación, identidad                                                 |
| `˜x`                           | NOT a nivel de bits (inversión)                                     |
| `x ** y`                       | Potenciación (exponenciación)                                       |
| `x[i]`                         | Indexación (secuencia, mapeo, otros)                                |
| `x[i:j:k]`                     | Rebanado                                                            |
| `x(...)`                       | Llamada (función, método, clase, otro llamable)                     |
| `x.attr`                       | Referencia de atributo                                              |
| `(...)`                        | Tupla, expresión, expresión generadora                              |
| `[...]`                        | Lista, comprensión de listas                                        |
| `{...}`                        | Diccionario, conjunto, comprensiones de conjunto y diccionario      |

## Numbers in Action

### Variables and Basic Expressions

### Numeric Display Formats

### Comparisons: Normal and Chained

### Division: Classic, Floor and True

### Integer Precision

### Complex Numbers

### Hex, Octal, Binary: Literals and Conversions

### Bitwise Operations

### Other Built-in Numeric Tools

## Other Numeric Types

## Numeric Extensions



