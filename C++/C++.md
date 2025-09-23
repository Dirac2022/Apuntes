
# Basics: Functions and Files


A **function** is a reusable sequence of statements designed to do a particular job. Functions you write yourself are called **user-defined** functions.

A **function call** is an expression that tells the CPU to execute a function. The function initiating the function call is the **caller**, and the function being called is the **callee** or **called** function.

The curly braces and statements in a function definition are called the **function body**.

A function that returns a value is called a **value-returning function**. The **return type** of a function indicates the type of value that the function will return. The **return statement** determines the specific **return value** that is returned to the caller. A return value is copied from the function back to the caller -- this process is called **return by value**. Failure to return a value from a non-void function will result in undefined behavior.

The return value from function _main_ is called a **status code**, and it tells the operating system (and any other programs that called yours) whether your program executed successfully or not. By consensus a return value of 0 means success, and a non-zero return value means failure.

## Void functions

Functions are not required to return a value back to the caller. To tell the compiler that a function does not return a value, a return type of **void** is used. For example

```cpp
#include <iostream>

// void means the function does not return a value to the caller
void printHi()
{
    std::cout << "Hi" << '\n';

    // This function does not return a value so no return statement is needed
}

int main()
{
    printHi(); // okay: function printHi() is called, no value is returned

    return 0;
}
```

<h5>Void functions don't need a return statement</h5>
A void function will automatically return to the caller at the end of the function. No return statement is required.

```cpp
#include <iostream>

// void means the function does not return a value to the caller
void printHi()
{
    std::cout << "Hi" << '\n';

    return; // tell compiler to return to the caller -- this is redundant since the return will happen at the end of the function anyway!
} // function will return to caller here

int main()
{
    printHi();

    return 0;
}
```


<h5>Returning a value from a void function is a compile error</h5>
Trying to return a value from a non-value returning function will result in a compilation error:

```cpp
void printHi() // This function is non-value returning
{
    std::cout << "In printHi()" << '\n';

    return 5; // compile error: we're trying to return a value
}
```



## Introduction to function parameters and arguments

A **function parameter** is a variable used in the header of a function. Function parameters work almost identically to variables defined inside the function, but with one difference: they are initialized with a value provided by the caller of the function.

Here are some examples:

```cpp
// This function takes no parameters
// It does not rely on the caller for anything
void doPrint()
{
    std::cout << "In doPrint()\n";
}

// This function takes one integer parameter named x
// The caller will supply the value of x
void printValue(int x)
{
    std::cout << x << '\n';
}

// This function has two integer parameters, one named x, and one named y
// The caller will supply the value of both x and y
int add(int x, int y)
{
    return x + y;
}
```

An **argument** is a value that is passed from the caller to the function when a function call is made.

<h5>How parameters and arguments work together</h5>
When a function is called, all of the parameters of the function are created as variables, and the value of each of the arguments is copied into the matching parameter (using copy initialization). This process is called **pass by value**.

Functions parameters that utilize pass by value are called **value parameters**.

### Unreferenced parameters and unnamed parameters

In certain cases, you will encounter functions that have parameters that are not used in the body of the function. These are called **unreferenced parameters**.

As a trivial example:

```cpp
void doSomething(int count) // warning: unreferenced parameter count
{
    // This function used to do something with count but it is not used any longer
}

int main()
{
    doSomething(4);

    return 0;
}
```

Just like with unused local variables, your compiler will probably warn that variable `count` has been defined but not used.

In a function definition, the name of a function parameter is optional. Therefore, in cases where a function parameter needs to exist but is not used in the body of the function, you can simply omit the name. A parameter without a name is called an **unnamed parameter**:

```cpp
void doSomething(int) // ok: unnamed parameter will not generate warning
{
}
```

The Google C++ style guide recommends using a comment to document what the unnamed parameter was:

```cpp
void doSomething(int /*count*/)
{
}
```


> [!tip] Author's note
> You’re probably wondering why we’d write a function that has a parameter whose value isn’t used. This happens most often in cases similar to the following:
>
>1. Let’s say we have a function with a single parameter. Later, the function is updated in some way, and the value of the parameter is no longer needed. If the now-unused function parameter were simply removed, then every existing call to the function would break (because the function call would be supplying more arguments than the function could accept). This would require us to find every call to the function and remove the unneeded argument. This might be a lot of work (and require a lot of retesting). It also might not even be possible (in cases where we did not control all of the code calling the function). So instead, we might leave the parameter as it is, and just have it do nothing


## Introduction to local scope

### Introduction to temporary objects

A **temporary object** (also sometimes called an **anonymous object**) is an unnamed object that is used to hold a value that is only needed for a short period of time. Temporary objects are generated by the compiler when they are needed.

There are many different ways that temporary values can be created, but here’s a common one:

```cpp
#include <iostream>

int getValueFromUser()
{
 	std::cout << "Enter an integer: ";
	int input{};
	std::cin >> input;

	return input; // return the value of input back to the caller
}

int main()
{
	std::cout << getValueFromUser() << '\n'; // where does the returned value get stored?

	return 0;
}
```


In the above program, the function `getValueFromUser()` returns the value stored in local variable `input` back to the caller. Because `input` will be destroyed at the end of the function, the caller receives a copy of the value so that it has a value it can use even after `input` is destroyed.

But where is the value that is copied back to the caller stored? We haven’t defined any variables in `main()`. The answer is that the return value is stored in a temporary object. This temporary object is then passed to `std::cout` to be printed

Temporary objects have no scope at all (this makes sense, since scope is a property of an identifier, and temporary objects have no identifier).

Temporary objects are destroyed at the end of the full expression in which they are created. This means temporary objects are always destroyed before the next statement executes.

In our example above, the temporary object created to hold the return value of `getValueFromUser()` is destroyed after `std::cout << getValueFromUser() << '\n'` executes.


## Introduction to the preprocessor

Prior to compilation, each code (`.cpp`) file goes through a **preprocessing** phase. In this phase , a program called the **preprocessor** makes various changes to the text of the code file. The preprocessor does not actually modify the original code files in any way -- rather, all changes made by the preprocessor happen either temporarily in-memory or using temporary files.


<h3>Preprocessor directives</h3>
**Preprocessor directives** (often just called directives) are instructions that start with a `#` symbol and end with a newline. The directives tell the preprocessor to perform certain text maniputation task. This directives have their own syntax.

### `#include`

 When you `#include` a file, the preprocessor replaces the `#include` directive with the contents of the included file. The included contents are then preprocessed (which may result in additional `#include` being preprocessed recursively), then the rest of the file is preprocessed.


### Macro defines

The `#define` directive can be used to create a macro. In C++, a **macro** is a rule that defines how input text is converted into replacement output text.

There are two basic types of macros: _object-like macros_, and _function-like macros_.

_Function-like macros_ act like functions, and serve a similar purpose. Their use is generally considered **unsafe**, and almost anything they can do can be done by a normal function.

_Object-like macros_ can be defined in one of two ways:

```cpp
#define IDENTIFIER
#define IDENTIFIER substitution_text
```


<h5>Object-like macros with substitution text</h5>
When the preprocessor encounters this directive, an association is made between the macro identifier and _substitution_text_. All further occurrences of the macro identifier (outside of use in other preprocessor commands) are replaced by the _substitution_text_.

Consider the following program:

```cpp
#include <iostream>

#define MY_NAME "Alex"

int main()
{
    std::cout << "My name is: " << MY_NAME << '\n';

    return 0;
}
```

The preprocessor converts the above into the following:

```cpp
// The contents of iostream are inserted here

int main()
{
    std::cout << "My name is: " << "Alex" << '\n';

    return 0;
}
```


>[!tip] Best practice
>Avoid macros with substitution text unless no viable alternatives exist.

<h5>Object-like macros without substitution text</h5>
```cpp
#define USE_YEN
```

This might seem pretty useless, and it _is useless_ for doing text substitution. However, that’s not what this form of the directive is generally used for.

### Conditional compilation

The _conditional compilation_ preprocessor directives allow you to specify under what conditions something will or won’t compile. There are quite a few different conditional compilation directives, but we’ll only cover a few that are used the most often: `#ifdef`, `ifndef` and `#endif`.

The `#ifdef` preprocessor directive allows the preprocessor to check whether an identifier has been previously defined via `#define` If so, the code between the `#ifdef` and matching `#endif` is compiled. If not, the code is ignored.

```cpp
#include <iostream>

#define PRINT_JOE

int main()
{
#ifdef PRINT_JOE
    std::cout << "Joe\n"; // will be compiled since PRINT_JOE is defined
#endif

#ifdef PRINT_BOB
    std::cout << "Bob\n"; // will be excluded since PRINT_BOB is not defined
#endif

    return 0;
}
```

Because PRINT_JOE has been `#define`, the line `std::cout << "Joe\n"` will be compiled. Because PRINT_BOB has not been `#define`, the line `std::cout << "Bob\n"` will be ignored.

`ifndef` is the opposite of `#ifdef`, in that it allows you to check whether an identifier has _NOT_ been `#define`  yet.

```cpp
#include <iostream>

int main()
{
#ifndef PRINT_BOB
    std::cout << "Bob\n";
#endif

    return 0;
}
```

This program prints “Bob”, because PRINT_BOB was never *#defined*.

>[!tip] Note
>In place of `#ifdef PRINT_BOB` and `#ifndef PRINT_BOB`, you’ll also see `#if defined(PRINT_BOB)` and `#if !defined(PRINT_BOB)`. These do the same, but use a slightly more C++-style syntax.


### `#if 0`

One more common use of conditional compilation involves using _#if 0_ to exclude a block of code from being compiled (as if it were inside a comment block). This provides a convenient way to “comment out” code that contains multi-line comments (which can’t be commented out using another multi-line comment due to multi-line comments being non-nestable)

```cpp
#include <iostream>

int main()
{
    std::cout << "Joe\n";

#if 0 // Don't compile anything starting here
    std::cout << "Bob\n";
    /* Some
     * multi-line
     * comment here
     */
    std::cout << "Steve\n";
#endif // until this point

    return 0;
}
```

To temporarily re-enable code that has been wrapped in an `#if 0`, you can change the `#if 0` to `#if 1`.


### The scope of `#define`

Directives are resolved before compilation, from top to bottom on a file-by-file basis.

```cpp
#include <iostream>

void foo()
{
#define MY_NAME "Alex"
}

int main()
{
	std::cout << "My name is: " << MY_NAME << '\n';

	return 0;
}
```

Even though it looks like `#define MY_NAME “Alex”` is defined inside function _foo_, the preprocessor doesn’t understand C++ concepts like functions. Therefore, this program behaves identically to one where `#define MY_NAME “Alex”` was defined either before or immediately after function _foo_.

>[!tip]
>To avoid confusion, you’ll generally want to `#define` identifiers outside of functions


An `#include` copy directives from the included file into the current file. These directives will then be processed in order.

`Alex.h`

```cpp
#define MY_NAME "Alex"
```

`main.cpp`

```cpp
#include "Alex.h" // copies #define MY_NAME from Alex.h here
#include <iostream>

int main()
{
	std::cout << "My name is: " << MY_NAME << '\n'; // preprocessor replaces MY_NAME with "Alex"

	return 0;
}
```

Directives defined in one file do not have any impact on other files (unless they are `#included` into another file).

`function.cpp`

```cpp
#include <iostream>

void doSomething()
{
#ifdef PRINT
    std::cout << "Printing!\n";
#endif
#ifndef PRINT
    std::cout << "Not printing!\n";
#endif
}
```


`main.cpp`

```cpp
void doSomething(); // forward declaration for function doSomething()

#define PRINT

int main()
{
    doSomething();

    return 0;
}
```

The above program will print:

```
Not printing!
```

Even though PRINT was defined in _main.cpp_, that doesn’t have any impact on any of the code in _function.cpp_ (PRINT is only `#defined` from the point of definition to the end of main.cpp).

## Header files

C++ code files (with a .cpp extension) are not the only files commonly seen in C++ programs. The other type of file is called a **header file**. Header files usually have a `.h` extension, but you will occasionally see them with a .`hpp` extension or no extension at all.

>[!tip] Key insights
>Header files allow us to put declarations in one place and then import them wherever we need them. This can save a lot of typing in multi-file programs.

<h5>Using header files to propagate forward declarations</h5>
Now let’s go back to the example we were discussing in a previous lesson. When we left off, we had two files, `add.cpp` and `main.cpp`, that looked like this:

`add.cpp`:

```cpp
int add(int x, int y)
{
    return x + y;
}
```

`main.cpp`:
```cpp
#include <iostream>

int add(int x, int y); // forward declaration using function prototype

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
```

Let's write a header file. Header files only consist of two parts:

1. A *header guard*
2. The actual contento fo the header file, which should be the forward declarations for all of the identifiers we want other.

Here's our completed header file:

`add.h`:

```cpp
// We really should have a header guard here, but will omit it for simplicity (we'll cover header guards in the next lesson)

// This is the content of the .h file, which is where the declarations go
int add(int x, int y); // function prototype for add.h -- don't forget the semicolon!
```

In order to use this header file in main.cpp, we have to `#include` it (using quotes, not angle brackets).

`main.cpp`:

```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.
#include <iostream>

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
```

`add.cpp`:

```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.

int add(int x, int y)
{
    return x + y;
}
```

When the preprocessor processes the `#include "add.h"` line, it copies the contents of add.h into the current file at that point. Because our _add.h_ contains a forward declaration for function _add()_, that forward declaration will be copied into _main.cpp_. The end result is a program that is functionally the same as the one where we manually added the forward declaration at the top of _main.cpp_. 

Consequently, our program will compile and link correctly

![IncludeHeader.png (647×377)](https://www.learncpp.com/images/CppTutorial/Section1/IncludeHeader.png)


<h5>Header file best practices</h5>

Here are a few more recommendations for creating and using header files.

- Always include header guards (we’ll cover these next lesson).
- Do not define variables and functions in header files (for now).
- Give a header file the same name as the source file it’s associated with (e.g. `grades.h` is paired with `grades.cpp`).
- Each header file should have a specific job, and be as independent as possible. For example, you might put all your declarations related to functionality A in A.h and all your declarations related to functionality B in B.h. That way if you only care about A later, you can just include A.h and not get any of the stuff related to B.
- Be mindful of which headers you need to explicitly include for the functionality that you are using in your code files, to avoid inadvertent transitive includes.
- A header file should `#include` any other headers containing functionality it needs. Such a header should compile successfully when `#include` into a .cpp file by itself.
- Only `#include` what you need (don’t include everything just because you can).
- Do not `#include` `.cpp` files.
- Prefer putting documentation on what something does or how to use it in the header. It’s more likely to be seen there. Documentation describing how something works should remain in the source files.


## Header guards

>[!warning]
>In upcoming examples, we’ll define some functions inside header files. You generally shouldn’t do this.
> 
> We are doing so here because it is the most effective way to demonstrate some concepts using functionality we’ve already covered.


Consider the following academic example:

square.h:

```cpp
int getSquareSides()
{
    return 4;
}
```

wave.h:

```cpp
#include "square.h"
```

main.cpp:

```cpp
#include "square.h"
#include "wave.h"

int main()
{
    return 0;
}
```

This seemingly innocent looking program won’t compile! Here’s what’s happening. First, _main.cpp_ #includes _square.h_, which copies the definition for function _getSquareSides_ into _main.cpp_. Then _main.cpp_ #includes _wave.h_, which #includes _square.h_ itself. This copies contents of _square.h_ (including the definition for function _getSquareSides_) into _wave.h_, which then gets copied into _main.cpp_

Thus, after resolving all of the #includes, _main.cpp_ ends up looking like this:

```cpp
int getSquareSides()  // from square.h
{
    return 4;
}

int getSquareSides() // from wave.h (via square.h)
{
    return 4;
}

int main()
{
    return 0;
}
```

Duplicate definitions and a compile error. Each file, individually, is fine. However, because _main.cpp_ ends up #including the content of _square.h_ twice, we’ve run into problems. If _wave.h_ needs _getSquareSides()_, and _main.cpp_ needs both _wave.h_ and _square.h_, how would you resolve this issue?

### Header guards

Header guards are conditional compilation directives that take the following form:

```cpp
#ifndef SOME_UNIQUE_NAME_HERE
#define SOME_UNIQUE_NAME_HERE

// declarations

#endif
```

When this header is #included, the preprocessor will check whether _SOME_UNIQUE_NAME_HERE_ has been previously defined in this translation unit. If this is the first time we’re including the header, _SOME_UNIQUE_NAME_HERE_ will not have been defined. Consequently, it #defines _SOME_UNIQUE_NAME_HERE_ and includes the contents of the file. If the header is included again into the same file, _SOME_UNIQUE_NAME_HERE_ will already have been defined from the first time the contents of the header were included, and the contents of the header will be ignored (thanks to the #ifndef).

All of your header files should have header guards on them.

For example, `square.h` would have the header guard:

`square.h`

```cpp
#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides()
{
    return 4;
}

#endif
```


### Avoiding definitions in header files
We’ve generally told you not to include function definitions in your headers. So you may be wondering why you should include header guards if they protect you from something you shouldn’t do.

There are quite a few cases we’ll show you in the future where it’s necessary to put non-function definitions in a header file. For example, C++ will let you create your own types. These custom types are typically defined in header files, so the type definitions can be propagated out to the code files that need to use them. Without a header guard, a code file could end up with multiple (identical) copies of a given type definition, which the compiler will flag as an error.

### `#pragma once`

Modern compilers support a simpler, alternate form of header guards using the `#pragma` preprocessor directive:

```cpp
#pragma once

// your code here
```

`#pragma once` serves the same purpose as header guards: to avoid a header file from being included multiple times. With traditional header guards, the developer is responsible for guarding the header (by using preprocessor directives `#ifndef`, `#define`, and `#endif`). With `#pragma once`, we’re requesting that the compiler guard the header. How exactly it does this is an implementation-specific detail.


# Compound Types: References and Pointers


<h5>Compound data types</h5>
**Compound data types** are types that are defined in terms of other existing data types. Every data type is either a fundamental type or a compound type

C++ supports the following compound types:

- Functions
- C-style Arrays
- Pointer types:
    - Pointer to object
    - Pointer to function
- Pointer to member types:
    - Pointer to data member
    - Pointer to member function
- Reference types:
    - L-value references
    - R-value references
- Enumerated types:
    - Unscoped enumerations
    - Scoped enumerations
- Class types:
    - Structs
    - Classes
    - Unions


## Value categories (lvalues and rvalues)


**The properties of an expression**
To help determine how expressions should evaluate and where they can be used, all expressions in C++ have two properties: a type and a **value category**

### The value category of an expression

```cpp
int main()
{
    int x{};

    x = 5; // valid: we can assign 5 to x
    5 = x; // error: can not assign value of x to literal value 5

    return 0;
}
```

How the compiler know which expression can legally appear on either side of an assignment statement?

The answer lies in the second property of expressions: the `value category`. The **value category** of an expression (or subexpression) indicates whether an expression resolves to a value, a function, or an object of some kind.

### Lvalue and rvalue expressions

An **lvalue** is an expression that evaluates to an identifiable object or function (or bit-field).

The term “identity” is used by the C++ standard, but is not well-defined. An entity (such as an object or function) that has an identity can be differentiated from other similar entities (typically by comparing the addresses of the entity).

Entities with identities can be accessed via an identifier, reference, or pointer, and typically have a lifetime longer than a single expression or statement.

```cpp
int main()
{
    int x { 5 };
    int y { x }; // x is an lvalue expression

    return 0;
}
```


In the above program, the expression `x` is an lvalue expression as it evaluates to variable `x` (which has an identifier).

- A **modifiable lvalue** is an lvalue whose value can be modified.
- A **non-modifiable lvalue** is an lvalue whose can't be modified (because the lvalue is const or constexpr).

```cpp
int main()
{
    int x{};
    const double d{};

    int y { x }; // x is a modifiable lvalue expression
    const double e { d }; // d is a non-modifiable lvalue expression

    return 0;
}
```


An **rvalue** 

is an expression that is not an lvalue. Rvalue expressions evaluate to a value. Commonly seen rvalues include literals (except C-style string literals, which are lvalues) and the return value of functions and operators that return by value. Rvalues aren’t identifiable (meaning they have to be used immediately), and only exist within the scope of the expression in which they are used.

```cpp
int return5()
{
    return 5;
}

int main()
{
    int x{ 5 }; // 5 is an rvalue expression
    const double d{ 1.2 }; // 1.2 is an rvalue expression

    int y { x }; // x is a modifiable lvalue expression
    const double e { d }; // d is a non-modifiable lvalue expression
    int z { return5() }; // return5() is an rvalue expression (since the result is returned by value)

    int w { x + 1 }; // x + 1 is an rvalue expression
    int q { static_cast<int>(d) }; // the result of static casting d to an int is an rvalue expression

    return 0;
}
```

You may be wondering why `return5()`, `x + 1`, and `static_cast<int>(d)` are rvalues: the answer is because these expressions produce temporary values that are not identifiable objects.

>[!tip] Key insight
>- Lvalue expressions evaluate to an identifiable object.
>- Rvalue expressions evaluate to a value.


<h5>Value categories and operators</h5>
Unless otherwise specified, operators expect their operands to be rvalues.

Now we can answer the question about why `x = 5` is valid but `5 = x` is not: an assignment operation requires its left operand to be a modifiable lvalue expression. The latter assignment (`5 = x`) fails because the left operand expression `5` is an rvalue, not a modifiable lvalue.

```cpp
int main()
{
    int x{};

    // Assignment requires the left operand to be a modifiable lvalue expression and the right operand to be an rvalue expression
    x = 5; // valid: x is a modifiable lvalue expression and 5 is an rvalue expression
    5 = x; // error: 5 is an rvalue expression and x is a modifiable lvalue expression

    return 0;
}
```

<h5>Lvalue-to-rvalue conversion</h5>
In cases where an rvalue is expected but an lvalue is provided, **the lvalue will undergo an lvalue-to-rvalue conversion so that it can be used in such contexts**. This basically means the lvalue is evaluated to produce its value, which is an rvalue

>[!tip]
>An lvalue will implicitly convert to an rvalue. This means an lvalue can be used anywhere an rvalue is expected.  
An rvalue, on the other hand, will not implicitly convert to an lvalue.


<h5>How to differentiate lvalues and rvalues</h5>
>[!tip]
> - Lvalue expressions are those that evaluate to functions or identifiable objects (including variables) that persist beyond the end of the expression.
> - Rvalue expressions are those that evaluate to values, including literals and temporary objects that do not persist beyond the end of the expression.


```
5 is an rvalue
getint() is an rvalue
x is an lvalue
std::string {"Hello"} is an rvalue
"Hello" is an lvalue
++x is an lvalue
x++ is an rvalue
```

## Lvalue references

In C++, a **reference** is an alias for an existing object. Once a reference has been defined, any operation on the reference is applied to the object being referenced. This means we can use a reference to read or modify the object being referenced.

>[!tip]
>A reference is essentially identical to the object being referenced.

<h5>Lvalue references types</h5>
An **lvalue reference** acts as an alias for an existing lvalue (such as a variable).

Just like the type of an object determines what kind of value it can hold, the type of a reference determines what type of object it can reference. Lvalue reference types can be identified by use of a single ampersand (&) in the type specifier:


```cpp
// regular types
int        // a normal int type (not an reference)
int&       // an lvalue reference to an int object
double&    // an lvalue reference to a double object
const int& // an lvalue reference to a const int object
```

A type that specifies a reference (e.g. `int&`) is called a **reference type**. The type that can be referenced (e.g. `int`) is called the **referenced type**.

There are two kinds of lvalue references:

- An lvalue reference to a non-const is commonly just called an “lvalue reference”, but may also be referred to as an **lvalue reference to non-const** or a **non-const lvalue reference** (since it isn’t defined using the `const` keyword).
- An lvalue reference to a const is commonly called either an **lvalue reference to const** or a **const lvalue reference**.


<h5>Lvalue reference variable</h5>
An **lvalue reference variable** is a variable that acts as a reference to an lvalue (usually another variable).

```cpp
#include <iostream>

int main()
{
    int x { 5 };    // x is a normal integer variable
    int& ref { x }; // ref is an lvalue reference variable that can now be used as an alias for variable x

    std::cout << x << '\n';  // print the value of x (5)
    std::cout << ref << '\n'; // print the value of x via ref (5)

    return 0;
}
```

`ref` and `x` can be used synonymously. This program thus prints:

```
5
5
```


**Reference initialization**

- All references must be initialized. Reference are initialized using a form of initialization called **reference initialization**
- Non-const lvalue references can obly be bound to a *modifiable* lvalue

```cpp
int main()
{
    int x { 5 };
    int& ref { x };         // okay: non-const lvalue reference bound to a modifiable lvalue

    const int y { 5 };
    int& invalidRef { y };  // invalid: non-const lvalue reference can't bind to a non-modifiable lvalue
    int& invalidRef2 { 0 }; // invalid: non-const lvalue reference can't bind to an rvalue

    return 0;
}
```


- A reference will (usually) only bind to an object matching its referenced type

<h5>References can't be reseated (changed to refer to another object)</h5>

Once initialized, a reference in C++ cannot be **reseated**, meaning it cannot be changed to reference another object.

```cpp
#include <iostream>

int main()
{
    int x { 5 };
    int y { 6 };

    int& ref { x }; // ref is now an alias for x

    ref = y; // assigns 6 (the value of y) to x (the object being referenced by ref)
    // The above line does NOT change ref into a reference to variable y!

    std::cout << x << '\n'; // user is expecting this to print 5

    return 0;
}
```

Perhaps surprisingly, this prints:

```
6
```

When a reference is evaluated in an expression, it resolves to the object it’s referencing. So `ref = y` doesn’t change `ref` to now reference `y`. Rather, because `ref` is an alias for `x`, the expression evaluates as if it was written `x = y` -- and since `y` evaluates to value `6`, `x` is assigned the value `6`.


- References variables follow the same scoping and duration rules that normal variables do
- References and referents have independent lifetimes
	- A reference can be destroyed before the object it is referencing
	- The object being referenced can be destroyed before the reference


**Dangling references**

When an object being referenced is destroyed before a reference to it, the reference is left referencing an object that no longer exists. Such a reference is called a **dangling reference**. Accessing a dangling reference leads to undefined behavior.

**References aren´t objects**

Perhaps surprisingly, references are not objects in C++. A reference is not required to exist or occupy storage




## Lvalue references to const


## Pass by lvalue reference


## Pass by const lvalue reference


## Introduction to pointers


## Null  pointers


## Pointers and const



## Pass by address


## Pass by address (part 2)


## Return by reference and return by address


## In and out parameters


## Type deduction with pointers, references, and const

## std::optional



