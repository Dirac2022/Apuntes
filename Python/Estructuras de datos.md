
# List
Lists are positionally ordered collections of arbitrarily typed objects, and they have no fixed size.
They are also mutable—unlike strings, lists can be modified in-place by assignment to
offsets as well as a variety of list method calls.

List are sequences, therefore support all the sequence operations discussed for strings
*Common list literals and operations*

| Operation                         | Interpretation                 |
| --------------------------------- | ------------------------------ |
| L = []                            | An empty list                  |
| L = [123, 'abc', 1.23, {}]        | Four items                     |
| L = ['Bob', 40.0, ['dev', 'mgr']] | Nested sublists                |
| L = list('spam')                  | List of an iterable’s items    |
| L = list(range(-4, 4))            | List of successive integers    |
| L[i]                              | Index                          |
| L[i][j]                           | Index of index                 |
| L[i:j]                            | Slice                          |
| len(L)                            | Length                         |
| L1 + L2                           | Concatenate                    |
| L * 3                             | Repeat                         |
| for x in L: print(x)              | Iteration                      |
| 3 in L                            | Membership                     |
| L.append(4)                       | Methods: growing               |
| L.extend([5,6,7])                 |                                |
| L.insert(i, X)                    |                                |
| L.index(X)                        | Methods: searching             |
| L.count(X)                        |                                |
| L.sort()                          | Methods: sorting, reversing    |
| L.reverse()                       | Reversing                      |
| L.copy()                          | Copying                        |
| L.clear()                         | Clearing                       |
| L.pop(i)                          | Methods, statements: shrinking |
| L.remove(X)                       |                                |
| del L[i]                          |                                |
| del L[i:j]                        |                                |
| L[i:j] = []                       |                                |
| L[i] = 3                          | Index assigments               |
| L[i:j] = [4,5,6]                  | Slice assigment                |
| L = [x**2 for x in range(5)]      | List comprehensions            |
| list(map(ord, 'spam'))            | Maps                           |

Set L = [123, 'spam', 1.23] a list

- append(element): Add object at end of list
- pop(index): delete an item in specified index
- del L[index] deletes from a list too
- insert(i, x): inserts *s* into the list at index given by *i*
- More list operations: https://docs.python.org/3.11/library/stdtypes.html#sequence-types-list-tuple-range



# Dictionaries
They are not sequences at all, but are instead known as mappings. Mappings
are also collections of other objects, but they store objects by key instead of by relative
position Dictionaries are also mutable

When written as literals, dictionaries are coded in curly braces and consist of a series
of “key: value”

*Common dictionary literals and operations*

| Operation                                | Interpretation                                 |
| ---------------------------------------- | ---------------------------------------------- |
| D = {}                                   | Empty dictionary                               |
| D = {'name': 'Bob', 'age': 40}           | Two-item dictionary                            |
| E = {'cto': {'name': 'Bob', 'age': 40}}  | Nesting                                        |
|                                          | Alternative construction techniques:           |
| D = dict(name='Bob', age=40)             | keywords                                       |
| D = dict([('name', 'Bob'), ('age', 40)]) | Key/value pairs                                |
| D = dict(zip(keyslist, valueslist))      | Zipped key/value                               |
| D = dict.fromkeys(['name', 'age'])       | Key list                                       |
| D['name']                                | Indexing by key                                |
| E['cto']['age']                          |                                                |
| 'age' in D                               | Membership: key present test                   |
| D.keys()                                 | Methods: all keys,                             |
| D.values()                               | all values,                                    |
| D.items()                                | all key+value tuples,                          |
| D.copy()                                 | copy (top-level)                               |
| D.clear()                                | clear (remove all items),                      |
| D.update(D2)                             | merge by keys,                                 |
| D.get(key, default?)                     | fetch by key, if absent default (or None),     |
| D.pop(key, default?)                     | remove by key, if absent default (or error)    |
| D.setdefault(key, default?)              | fetch by key, if absent set default (or None), |
| D.popitem()                              | remove/return any (key, value) pair; etc.      |
| len(D)                                   | Length: number of stored entries               |
| D[key] = 42                              | Adding/changing keys                           |
| del D[key]                               | Deleting entries by key                        |
| list(D.keys())                           | Dictionary views (Python 3.X)                  |
| D1.keys() & D2.keys()                    |                                                |
| D.viewkeys(), D.viewvalues()             | Dictionary views (Python 2.7)                  |
| D = {x: x*2 for x in range(10)}          | Dictionary comprehensions (Python 3.X, 2.7)    |

# Tuples

Tuples are sequences, like lists, but they are immutable, like strings. Syntactically, they are coded in parentheses and they support arbitrary types, arbitrary nesting, and the usual sequence operations

# Sets

Sets are unordered collections of unique and  inmuutable objects. Sets support the usual mathematical set operations. We can creat sets with the built-in **set** function or using literals:
- X = set('spam')
- Y = {'h', 'a', 'm'}
X and Y are sets