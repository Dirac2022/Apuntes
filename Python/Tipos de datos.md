
# Numeric Types

## Numeric Literals
Python provides integers and floating-pint numbers. Python also allows us to write integers using hexadecimal, octal, and binary literals; offers a complex numer type; and allows integers to have unlimited precision.

| Literal                             | Interpretation                 |
| ----------------------------------- | ------------------------------ |
| 1234, -24, 0, 99999999999           | Integers (unlimited size)      |
| 1.23, 1., 3.14e-10, 4E210, 4.0e+210 | Floating-point numbers         |
| 0o177, 0x9ff, 0b101010              | Octal, hex and binary literals |
| 3+4j, 3.0 + 4.0j,  3J               | Complex number literals        |

Table 5-2. _Python expression operators and precedence_

| Operator                                       | Description                                                                   |
| ---------------------------------------------- | ----------------------------------------------------------------------------- |
| yield x                                        | Generator function send protocol                                              |
| lambda args: expression                        | Anonymous function generation                                                 |
| x if y else z                                  | Ternary selection ( x is evaluated only if y is true)                         |
| x or y                                         | Logical OR                                                                    |
| x and y                                        | Logical AND                                                                   |
| not x                                          | Logical negation                                                              |
| x in y, x not in y                             | Membershio(iterables, sets)                                                   |
| x is y, x is not y                             | Object identity test                                                          |
| x < y, x <= y, x > y, x >= y<br>x == y, x != y | Magnitude comparison, set subset and superset;<br>Value equality operators    |
| x \| y                                         | Bitwise OR, set union                                                         |
| x ^ y                                          | Bitwise XOR, set symmetric difference                                         |
| x & y                                          | Bitwise AND, set intersection                                                 |
| x << y, x >> y                                 | Shift x left or right by y bits                                               |
| x + y<br>x – y                                 | Addition, concatenation;<br>Subtraction, set difference                       |
| x * y<br>x % y<br>x / y, x // y                | Multiplication, repetition;<br>Remainder, format;<br>Division: true and floor |
| -x, +x                                         | Negation, identity                                                            |
| ~x                                             | Bitwise NOT (inversion)                                                       |
| x ** y                                         | Exponentiation                                                                |
| x[i]                                           | Indexing(sequence, mapping, others)                                           |
| x[i:j:k]                                       | Slicing                                                                       |
| x(...)                                         | Call (function, method, class, other callable)                                |
| x.attr                                         | Attibute reference                                                            |
| (...)                                          | Tuple, expression, generator expression                                       |
| [...]                                          | List, list comprehension                                                      |
| {...}                                          | Dictionary, set and dictionary comprehensions                                 |

- Operator lower in the table have higher precedence, and so bind more tightky in mixed expressions
- Operator in the same row generally group from left to right when combined (except for exponentiation, which groups right to left, and comparisons, which chain left to right).



### Some methods
- bin(64) = '0b1000000'
- oct(64) = '0100'
- hex(64) = '0x40'
- int('0x40', 16) = 64


## Division
- The / always perfoms *true* division, returning a float resultthat includes any remainder, regardless of operand types.
- The // performs *floor* division, which truncates the remainder and returns an integer for integer operands or a float if any operand is a float.

## Other Numeric Types

### Decimal Type
Decimal are *fixed-precision* floating-point values

### Fraction Type

The fraction type implements a *rational number object*. IT essentially keeps both a numerator and denominator explicitly, so as to avoid some of the inaccuracies and limitations of floating-point math

Fraction resides in a module; import its constructor and pass in a numerator
and a denominator to make one.

	from fractions import Fraction
	x = Fraction(2, 5)

This represent a 2/5 fraction

Also we can create a fraction from a string

		x = franction('0.4')


#### Limiting the maximum denominator value
Converting from floating-point to fraction, in some cases, there is an unavoidable precision loss, but we can simplify such results by limiting the maximum denominator value

If a is a fraction like Fraction(22517998136852479, 13510798882111488) where a is close to 1.6666666667 when can use

	a.limit_denominator(10)

to simplify to Fraction(5,3)


### Sets
Is an unordered collection of unique and ummutable objects that supports operations corresponding to mathematical set theory.
- Sets are iterable
- Sets are neither sequence nor mapping types

Let x = {'e', 'a', 'd', 'c', 'b'} and y = {'z', 'y', 'd', 'x', 'b'}

| Expression   | Description                  |
| ------------ | ---------------------------- |
| 'e' in x     | Membership                   |
| x - y        | Difference                   |
| x \| y       | Union                        |
| x & y        | Intersection                 |
| x ^ y        | Symmetric diffrerence  (XOR) |
| x > y, x < y | Superset, subset             |

If we want to create the set A = {1, 2, 3, 4}

	A = set([1,2,3,4])
	A = {1, 2, 3, 4}
	

Sets can only contain immutable ("hashable") object types. Hence, list and dictionaries cannot be embedded in sets, but tuples can.



# Strings
String are ordered colection o characters used to store and represent text-based information. Strings are inmutable sequences

Sea *str* una cadena de caracteres, por ejemplo *str = 'Spam'*

- **len:** longitud de la cadena
- **str[k]** 
	- si $k \geq 0$ te da el caracter situado en la posición $k$ comenzando desde la izquierda
	- - si $k<0$ te da el caracter situado en la posición *len(str)+k*

- **str[a:b]**: Te da un pedazo de la cadena, empezando desde $a$ hasta $b-1$
	- Si se omite $a$, es decir, **str[:b]** te da un pedazo de cadena desde la posicion $0$ hasta $b-1$
	- Si se omite $b$, **str[a:]** te da un pedazo de cadena, desde la posición $a$ hasta el final de la cadena
	- Si se omiten ambos indices, **str[:]**, nos devuelve toda la cadena. **str[:]** equivale a **str[0:len(str)]
	- Tambien se pueden usar indices negativos, los cuales deben encontrarse dentro del rango $-len(str)$ hasta $-1$. Además **str[a:b]** tiene sentido cuando $a<b$ y cuando $b \neq 0$ si $a<0$. 
	- El operador **[a:b]** te da una parte de la cadena donde se respeta el orden, es decir, siempre empezara por la posición $a$ y se movera hacia la izquierda hasta donde se encuentre la posición $b-1$ y tomara ese pedazo de cadena
- Las cadenas se pueden concatenar mediante el operador **+** para formar una nueva cadena
- El operador '\*' sirve para formar una nueva cadena repitiendo $n$ veces la cadena inicial. por ejemplo $str*n$ te devuelve *'SpamSpam ... Spam'* donde *Spam* se repite $n$ veces

**Cada operación de cadena esta definida para producir una nueva cadena como resultado**

| Operation                   | Interpretation                |
| --------------------------- | ----------------------------- |
| S = ''                      | Empty string                  |
| S = "spam's"                | Double quotes, same as single |
| S = 's\np\ta\x00m'          | Escape sequences              |
| S = """..."""               | Triple-quoted block strings   |
| S = r'\temp\spam'           | Raw strings                   |
| S = b'spam'                 | Byte strings                  |
| S1 + S2                     | Concatenate                   |
| S * 3                       | Repeat                        |
| S[i]                        | Index                         |
| S[i:j]                      | Slice                         |
| len(S)                      | Length                        |
| "a %s parrot" % kind        | String formatting expression  |
| "a {0} parrot".format(kind) | String formatting method      |
| for x in S: print(x)        | Iteration                     |
| 'spam' in S                 | Membership                    |

| Expression            | String method call |
| --------------------- | ------------------ |
| S.find('pa')          | search             |
| S.rstrip()            | Remove whitespace  |
| S.replace('pa', 'xx') | replacement        |
| S.split(',')          | split on delimiter |
| S.isdigit()           | Content test       |
| S.lower()             | Case conversion    |
| S.endswith('spam')    | End test           |
| 'spam'.join(strlist)  | Delimiter join     |
| S.encode('latin-1')   | Unicode conding    |

*String formatting type codes*

| Code | Meaning                               |
| ---- | ------------------------------------- |
| s    | String (or any objects'str(x) string) |
| r    | s, but uses repr, not str             |
| c    | Character                             |
| d    | Decimal (Integer)                     |
| i    | Integer                               |
| u    | Same as d (obsolete)                  |
| o    | Octal integer                         |
| x    | Hex integer                           |
| X    | x, but print uppercase                |
| e    | Floating-point exponent, lowercase    |
| E    | e, but uppercasse                     |
| f    | Floating-point decimal                |
| F    | f                                     |
| g    | Floating-point e or f                 |
| G    | Floating-point E or F                 |
| %    | Literal %                             |

## String Formatting Method Calls

 template = '{0}, {1} and {2}'                                   # By position
 template.format('spam', 'ham', 'eggs')
- 'spam, ham and eggs'
 
 template = '{motto}, {pork} and {food}'                # By keyword
 template.format(motto='spam', pork='ham', food='eggs')
- 'spam, ham and eggs'

template = '{motto}, {0} and {food}'                       # By both
 template.format('ham', motto='spam', food='eggs')
- 'spam, ham and eggs'

