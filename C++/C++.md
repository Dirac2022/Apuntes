
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


# Function Overloading and Function Templates

## Introduction to function overloading


## Function overload differentiation


## Function overload resolution and ambiguous matches


## Deleting function


## Default arguments


## Function templates

In C++, the template system was designed to simplify the process of creating functions (or classes) that are able to work with different data types.

Once a template is defined, the compiler can use the template to generate as many overloaded functions (or classes) as needed, each using different actual types!

The end result is the same -- we end up with a bunch of mostly-identical functions or classes (one for each set of different types). But we only have to create and maintain a single template, and the compiler does all the hard work to create the rest for us.


### Function templates
A **function template** is a function-like definition that is used to generate one or more overloaded functions, each with a different set of actual types. This is what will allow us to create functions that can work with many different types. The initial function template that is used to generate other functions is called the **primary template**, and the functions generated from the primary template are called **instantiated functions**.


> [!tip]
> C++ supports 3 different kinds of template parameters
> - Type template parameters (where the template parameter represents a type)
> - Non-type template parameters (where the template parameter represents a constexpr value)
> - Template template parameters (where the template parameter represents a template).


<h5>Creating a max() function template</h5>

```cpp
int max(int x, int y)
{
	return (x < y) ? y : x;
}
```

To create a function that uses a single template type, all occurrences of actual types like `int` must been replaced with the type template parameter `T`.

Second, we're going to tell the compiler that this is a template, and `T` is a type template parameter that is a placeholder for any type. Both of these are done using a **template parameter declaration**, which defines any template parameters that will be subsequently used. ==The scope of a template parameter declaration is strictly limited to the function template (or class template) that follows==. Therefore, each function template or class template needs its own template parameter declaration.

```cpp
template <typename T> // this is the template parameter declaration defining T as a type template parameter
T max(T x, T y) // this is the function template definition for max<T>
{
    return (x < y) ? y : x;
}
```

For each type template parameter, we use the keyword `typename` (preferred) or `class`, followed by the name of the type template parameter (e.g. `T`).


> [!tip] As an aside...
> There is no difference between the `typename` and `class` keywords in this context. We prefer the newer `typename` keyword, because it makes it clearer that the type template parameter can be replaced by any type (such as a fundamental type), not just class types.


## Function template instantiation


### Using a function template

Function templates are not actually functions -- their code isn’t compiled or executed directly. Instead, function templates have one job: to generate functions (that are compiled and executed).

To use our `max<T>` function template, we can make a function call with the following syntax:

```cpp
max<actual_type>(arg1, arg2); // actual_type is some actual type, like int or double
```

This looks a lot like a normal function call -- the primary difference is the addition of the type in angled brackets (called a **template argument**), which specifies the actual type that will be used in place of template type `T`.


Let’s take a look at this in a simple example:

```cpp
#include <iostream>

template <typename T>
T max(T x, T y)
{
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max<int>(1, 2) << '\n'; // instantiates and calls function max<int>(int, int)

    return 0;
}
```

When the compiler encounters the function call `max<int>(1, 2)`, it will determine that a function definition for `max<int>(int, int)` does not already exist. Consequently, the compiler will implicitly use our `max<T>` function template to create one.

The process of creating functions (with specific types) from function templates (with template types) is called **function template instantiation** (or **instantiation** for short). When a function is instantiated due to a function call, it’s called **implicit instantiation**. A function that is instantiated from a template is technically called a **specialization**, but in common language is often called a **function instance**. The template from which a specialization is produced is called a **primary template**. Function instances are normal functions in all regards.


<h5>Template argument deduction</h5>

In most cases, the actual types we want to use for instantiation will match the type of our function parameters. For example:

```cpp
std::cout << max<int>(1, 2) << '\n'; // specifying we want to call max<int>
```

In this function call, we’ve specified that we want to replace `T` with `int`, but we’re also calling the function with `int` arguments.

In cases where the type of the arguments match the actual type we want, we do not need to specify the actual type -- instead, we can use **template argument deduction** to have the compiler deduce the actual type that should be used from the argument types in the function call.

For example, instead of making a function call like this:

```cpp
std::cout << max<int>(1, 2) << '\n'; // specifying we want to call max<int>
```

We can do one of these instead:

```cpp
std::cout << max<>(1, 2) << '\n';
std::cout << max(1, 2) << '\n';
```

In either case, the compiler will see that we haven’t provided an actual type, so it will attempt to deduce an actual type from the function arguments that will allow it to generate a `max()` function where all template parameters match the type of the provided arguments. In this example, the compiler will deduce that using function template `max<T>` with actual type `int` allows it to instantiate function `max<int>(int, int)`, so that the type of both function parameters (`int`) matches the type of the provided arguments (`int`).

The difference between the two cases has to do with how the compiler resolves the function call from a set of overloaded functions. In the top case (with the empty angled brackets), the compiler will only consider `max<int>` template function overloads when determining which overloaded function to call. In the bottom case (with no angled brackets), the compiler will consider both `max<int>` template function overloads and `max` non-template function overloads. When the bottom case results in both a template function and a non-template function that are equally viable, the non-template function will be preferred.


- **Function templates with non-templates parameters**: It's possible to create functions templates that have both template parameters and non-template parameters.


### Function templates and default arguments for non-template parameters

Just like normal functions, function templates can have default arguments for non-template parameters. Each function instantiated from the template will use the same default argument.

For example:

```cpp
#include <iostream>

template <typename T>
void print(T val, int times=1)
{
    while (times--)
    {
        std::cout << val;
    }
}

int main()
{
    print(5);      // print 5 1 time
    print('a', 3); // print 'a' 3 times

    return 0;
}
```

This prints:

```
Saaa
```


### Beware function templates with modifiable static local variables

When a static local variable is used in a function template, each function instantiated from that template will have a separate version of the static local variable. This is rarely a problem if the static local variable is const. But if the static local variable is one that is modified, the results may not be as expected.

```cpp
#include <iostream>

// Here's a function template with a static local variable that is modified
template <typename T>
void printIDAndValue(T value)
{
    static int id{ 0 };
    std::cout << ++id << ") " << value << '\n';
}

int main()
{
    printIDAndValue(12);
    printIDAndValue(13);

    printIDAndValue(14.5);

    return 0;
}
```


This produces the result:

```
1) 12
2) 13
3) 14.5
```

You may have been expecting the last line to print `3) 14.5`. However, the compiler creates a `printIDAndValue<int>` function and a `printIDAndValue<double>` function, ==each have their own independent static local variable named== `id`, not one that is shared between them



## Function templates with multiple template types


Consider the following program

```cpp
#include <iostream>

template <typename T>
T max(T x, T y)
{
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max(2, 3.5) << '\n';  // compile error

    return 0;
}
```

You may be surprised to find that this program won’t compile. Instead, the compiler will issue a bunch of  error message.

`T` can only represent a single type. There is no type for `T` that would allow the compiler to instantiate function template `max<T>(T, T)` into a function with two different parameter types. Put another way, because both parameters in the function template are of type `T`, they must resolve to the same actual type.

We’ll have to find another solution. Fortunately, we can solve this problem in (at least) three ways.


<h5>Use static_cast to convert the arguments to matching types</h5>

The first solution is to put the burden on the caller to convert the arguments into matching types. For example:

```cpp
#include <iostream>

template <typename T>
T max(T x, T y)
{
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max(static_cast<double>(2), 3.5) << '\n'; // convert our int to a double so we can call max(double, double)

    return 0;
}
```

Now that both arguments are of type `double`, the compiler will be able to instantiate `max(double, double)` that will satisfy this function call.

However, this solution is awkward and hard to read.

<h5>Provide an explicit type template argument</h5>
```cpp
#include <iostream>

template <typename T>
T max(T x, T y)
{
    return (x < y) ? y : x;
}

int main()
{
    // we've explicitly specified type double, so the compiler won't use template argument deduction
    std::cout << max<double>(2, 3.5) << '\n';

    return 0;
}
```

In the above example, we call `max<double>(2, 3.5)`. Because we’ve explicitly specified that `T` should be replaced with `double`, the compiler won’t use template argument deduction. Instead, it will just instantiate the function `max<double>(double, double)`, and then type convert any mismatched arguments. Our `int` parameter will be implicitly converted to a `double`.

While this is more readable than using `static_cast`, it would be even nicer if we didn’t even have to think about the types when making a function call to `max` at all.

### Function templates with multiple template type parameters

The root of our problem is that we’ve only defined the single template type (`T`) for our function template, and then specified that both parameters must be of this same type.

The best way to solve this problem is to rewrite our function template in such a way that our parameters can resolve to different types. Rather than using one template type parameter `T`, we’ll now use two (`T` and `U`):

```cpp
#include <iostream>

template <typename T, typename U> // We're using two template type parameters named T and U
T max(T x, U y) // x can resolve to type T, and y can resolve to type U
{
    return (x < y) ? y : x; // uh oh, we have a narrowing conversion problem here
}

int main()
{
    std::cout << max(2, 3.5) << '\n'; // resolves to max<int, double>

    return 0;
}
```

Because we’ve defined `x` with template type `T`, and `y` with template type `U`, `x` and `y` can now resolve their types independently. When we call `max(2, 3.5)`, `T` can be an `int` and `U` can be a `double`. The compiler will happily instantiate `max<int, double>(int, double)` for us.

However, this example doesn’t work right. If you compile and run the program (with “treat warnings as errors” turned off), it will produce the following result:

```
3
```

What’s going on here? How can the max of `2` and `3.5` be `3`?

The conditional operator (?:) requires its (non-condition) operands to be the same common type. For example, the common type of `int` and `double` is `double`, so when the (non-condition) operands of our conditional operator are an `int` and a `double`, the value produced by the conditional operator will be of type `double`. In this case, that’s the value `3.5`, which is correct.

However, the declared return type of our function is `T`. When `T` is an `int` and `U` is a `double`, the return type of the function is `int`. Our value `3.5` is undergoing a narrowing conversion to `int` value `3`, resulting in a loss of data (and possibly a compiler warning).

In such cases, return type deduction (via `auto`) can be useful -- we’ll let the compiler deduce what the return type should be from the return statement:

```cpp
#include <iostream>

template <typename T, typename U>
auto max(T x, U y) // ask compiler can figure out what the relevant return type is
{
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max(2, 3.5) << '\n';

    return 0;
}
```

This version of `max` now works fine with operands of different types. Just note that a function with an `auto` return type needs to be fully defined before it can be used (a forward declaration won’t suffice), since the compiler has to inspect the function implementation to determine the return type.


<h5>Advanced topic</h5>

If we need a function that can be forward declared, we have to be explicit about the return type. Since our return type needs to be the common type of `T` and `U`, we can use `std::common_type_t` (discussed in lesson [10.5 -- Arithmetic conversions](https://www.learncpp.com/cpp-tutorial/arithmetic-conversions/)) to fetch the common type of `T` and `U` to use as our explicit return type:


### Abbreviated function templates

**C++20** introduces a new use of the `auto` keyword: When the `auto` keyword is used as a parameter type in a normal function, the compiler will automatically convert the function into a function template with each auto parameter becoming an independent template type parameter. This method for creating a function template is called an **abbreviated function template**.

For example:

```cpp
auto max(auto x, auto y)
{
    return (x < y) ? y : x;
}
```

is shorthand in C++20 for the following:

```cpp
template <typename T, typename U>
auto max(T x, U y)
{
    return (x < y) ? y : x;
}
```

which is the same as the `max` function template we wrote above.

### Function templates may be overloaded

Just like functions may be overloaded, function templates may also be overloaded. Such overloads can have a different number of template types and/or a different number or type of function parameters:

```cpp
#include <iostream>

// Add two values with matching types
template <typename T>
auto add(T x, T y)
{
    return x + y;
}

// Add two values with non-matching types
// As of C++20 we could also use auto add(auto x, auto y)
template <typename T, typename U>
auto add(T x, U y)
{
    return x + y;
}

// Add three values with any type
// As of C++20 we could also use auto add(auto x, auto y, auto z)
template <typename T, typename U, typename V>
auto add(T x, U y, V z)
{
    return x + y + z;
}

int main()
{
    std::cout << add(1.2, 3.4) << '\n'; // instantiates and calls add<double>()
    std::cout << add(5.6, 7) << '\n';   // instantiates and calls add<double, int>()
    std::cout << add(8, 9, 10) << '\n'; // instantiates and calls add<int, int, int>()

    return 0;
}
```

One interesting note here is that for the call to `add(1.2, 3.4)`, the compiler will prefer `add<T>(T, T)` over `add<T, U>(T, U)` even though both could possibly match.

The rules for determining which of multiple matching function templates should be preferred are called “partial ordering of function templates”. In short, whichever function template is more restrictive/specialized will be preferred. `add<T>(T, T)` is the more restrictive function template in this case (since it only has one template parameter), so it is preferred.

If multiple function templates can match a call and the compiler can’t determine which is more restrictive, the compiler will error with an ambiguous match.



## Non-type template parameters


## Using function templates in multiple files


Templates that are needed in multiple files should be defined in a a header file, and then `#included` wherever needed. This allows the compiler to see the full template definition and instantiate the template when needed.

Here’s an example of a function template being placed in a header file, so it can be included into multiple source files:

max.h:

```cpp
#ifndef MAX_H
#define MAX_H

template <typename T>
T max(T x, T y)
{
    return (x < y) ? y : x;
}

#endif
```

foo.cpp:

```cpp
#include "max.h" // import template definition for max<T>(T, T)
#include <iostream>

void foo()
{
	std::cout << max(3, 2) << '\n';
}
```

main.cpp:

```cpp
#include "max.h" // import template definition for max<T>(T, T)
#include <iostream>

void foo(); // forward declaration for function foo

int main()
{
    std::cout << max(3, 5) << '\n';
    foo();

    return 0;
}
```

In the above example, both main.cpp and foo.cpp `#include "max.h"` so the code in both files can make use of the `max<T>(T, T)` function template.


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

Perhaps surprisingly, references are not objects in C++. A reference is not required to exist or occupy storage.

Because references aren't objects, they can't be used anywhere an object is required (e.g. you can't have a reference to a reference, since an lvalue reference must reference an identifiable object).

Consider the example:

```cpp
int var{5};
int& ref1{ var };  // an lvalue reference bound to var
int& ref2{ ref1 }; // an lvalue reference bound to var
```

Both `ref1` and `ref2` are references to `var`

```cpp
std::cout<< var << ref1 << ref2 << std::endl;
# 555
```
## Lvalue references to const

A lvalue reference cannot bind to a non-modifiable lvalue.
By using the `const` keyword when declaring an lvalue reference, we tell an lvalue reference to treat the object it is referencing as const. Such a reference is calle an **lvalue reference to a const value**, **reference to const** or **const reference**.

```cpp
int main()
{
    const int x { 5 };    // x is a non-modifiable lvalue
    const int& ref { x }; // okay: ref is a an lvalue reference to a const value

    return 0;
}
```

A lvalue reference to const can be used to access but not modify the value being referenced.

<h5>Initializing an lvalue reference to const with a modifiable lvalue</h5>

Lvalue references to const can also bind to modifiable lvalues. In such a case, the object being referenced is treated as const when accessed through the reference (even though the underlying object is non-const):

```cpp
#include <iostream>

int main()
{
    int x { 5 };          // x is a modifiable lvalue
    const int& ref { x }; // okay: we can bind a const reference to a modifiable lvalue

    std::cout << ref << '\n'; // okay: we can access the object through our const reference
    ref = 7;                  // error: we can not modify an object through a const reference

    x = 6;                // okay: x is a modifiable lvalue, we can still modify it through the original identifier

    return 0;
}
```

> [!tip] Best practice
> Favor **lvalue references to const** over **lvalue references to non-const** unless you need to modify the object being referenced.


<h5>Initializing an lvalue reference to const with an rvalue</h5>

lvalues references to const can also bind to rvalues:

```cpp
#include <iostream>

int main()
{
    const int& ref { 5 }; // okay: 5 is an rvalue
    // Doesn't work with:
    // int& ref { 5 };

    std::cout << ref << '\n'; // prints 5

    return 0;
}
```

When this happens, a temporary object is created and initialized with the rvalue, and the reference to const is bound to that temporary object.

<h5>Initializing an lvalue reference to const with a value of a different type</h5>

Lvalue references to const can even bind to values of a different type, so long as those values can be implicitly converted to the reference type:

```cpp
#include <iostream>

int main()
{
    // case 1
    const double& r1 { 5 };  // temporary double initialized with value 5, r1 binds to temporary

    std::cout << r1 << '\n'; // prints 5

    // case 2
    char c { 'a' };
    const int& r2 { c };     // temporary int initialized with value 'a', r2 binds to temporary

    std::cout << r2 << '\n'; // prints 97 (since r2 is a reference to int)

    return 0;
}
```


Const references bound to temporary objects extends the lifetime of temporary object.

> [!tip] Key insight
> Lvalue references can only bind to modifiable lvalues.
> Lvalue references to const can bind to modifiable lvalues, non-modifiable lvalues, and rvalues. This makes them a much more flexible type of reference.

<h5>Constexpr lvalue references</h5>
**Ver constexpr**

## Pass by lvalue reference

In function parameters a **pass by value** an argument passed to a function is copied into the function's parameter.

```cpp
#include <iostream>
#include <string>

void printValue(std::string y)
{
    std::cout << y << '\n';
} // y is destroyed here

int main()
{
    std::string x { "Hello, world!" }; // x is a std::string

    printValue(x); // x is passed by value (copied) into parameter y (expensive)

    return 0;
}
```

A copy of a `std::string` is expensive.

### Pass by reference

When using **pass by reference**, we declare a function parameter as reference type (or const reference type) rather than as a normal type. When the function is called, each reference parameter is bound to the appropriate argument. Because the reference acts as an alias for the argument, no copy of the argument is made.

Here’s the same example as above, using pass by reference instead of pass by value:

```cpp
#include <iostream>
#include <string>

void printValue(std::string& y) // type changed to std::string&
{
    std::cout << y << '\n';
} // y is destroyed here

int main()
{
    std::string x { "Hello, world!" };

    printValue(x); // x is now passed by reference into reference parameter y (inexpensive)

    return 0;
}
```

This program is identical to the prior one, except the type of parameter `y` has been changed from `std::string` to `std::string&` (an lvalue reference). Now, when `printValue(x)` is called, lvalue reference parameter `y` is bound to argument `x`.


<h5>Pass by reference allows us to change the value of an argument</h5>
When using pass by reference, any changes made to the reference parameter will affect the argument.

```cpp
#include <iostream>

void addOne(int& y) // y is bound to the actual object x
{
    ++y; // this modifies the actual object x
}

int main()
{
    int x { 5 };

    std::cout << "value = " << x << '\n';

    addOne(x);

    std::cout << "value = " << x << '\n'; // x has been modified

    return 0;
}
```

```
value = 5
value = 6
```

<h5>Pass by reference can only accept modifiable lvalue arguments</h5>

Because a reference to a non-const value can only bind to a modifiable lvalue (essentially a non-const variable), this means that pass by reference only works with arguments that are modifiable lvalues. In practical terms, this significantly limits the usefulness of pass by reference to non-const, as it means we can not pass const variables or literals. For example:

```cpp
#include <iostream>

void printValue(int& y) // y only accepts modifiable lvalues
{
    std::cout << y << '\n';
}

int main()
{
    int x { 5 };
    printValue(x); // ok: x is a modifiable lvalue

    const int z { 5 };
    printValue(z); // error: z is a non-modifiable lvalue

    printValue(5); // error: 5 is an rvalue

    return 0;
}
```


## Pass by const lvalue reference

  
Unlike a reference to non-const, a reference to const can bind to modifiable lvalues, non-modifiable lvalues, and rvalues. Therefore, if we make a reference parameter const, then it will be able to bind to any type of argument:

```cpp
#include <iostream>

void printRef(const int& y) // y is a const reference
{
    std::cout << y << '\n';
}

int main()
{
    int x { 5 };
    printRef(x);   // ok: x is a modifiable lvalue, y binds to x

    const int z { 5 };
    printRef(z);   // ok: z is a non-modifiable lvalue, y binds to z

    printRef(5);   // ok: 5 is rvalue literal, y binds to temporary int object

    return 0;
}
```

Passing by const reference ensures that the function cannot change the value being referenced.

```cpp
void addOne(const int& ref)
{
    ++ref; // not allowed: ref is const
}
```


> [!tip] Best practice
> Favor passing by const reference over passing by non-const reference unless you have a specific reason to do otherwise (e.g. the function needs to change the value of an argument).


<h5>When to use pass by value vs pass by reference</h5>
- Fundamental types and enumerated types are cheap to copy, so they are typically passed by value.
- Class types can be expensive to copy (sometimes significantly so), so they are typically passed by const reference.

> [!tip]
>
Here’s a partial list of other interesting cases:
>
The following are often passed by value (because it is more efficient):
>
>- Enumerated types (unscoped and scoped enumerations).
>- Views and spans (e.g. `std::string_view`, `std::span`).
>- Types that mimic references or (non-owning) pointers (e.g. iterators, `std::reference_wrapper`).
>- Cheap-to-copy class types that have value semantics (e.g. `std::pair` with elements of fundamental types, `std::optional`, `std::expected`).
>
Pass by reference should be used for the following:
>
>- Arguments that need to be modified by the function.
>- Types that aren’t copyable (such as `std::ostream`).
>- Types where copying has ownership implications that we want to avoid (e.g. `std::unique_ptr`, `std::shared_ptr`).
>- Types that have virtual functions or are likely to be inherited from (due to object slicing concerns, covered in lesson [25.9 -- Object slicing](https://www.learncpp.com/cpp-tutorial/object-slicing/))

	
## Introduction to pointers

### The address-of operator `(&)`

We can access the memory address for a variable. The **address-of operator** `&` returns the memory address of its operand. 

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    std::cout << x << '\n';  // print the value of variable x
    std::cout << &x << '\n'; // print the memory address of variable x

    return 0;
}
```

Output example

```
5
0027FEA0
```

>[!tip]
>The `&` symbol has different meanings depending on the context
>- When following a type name, & denotes an lvalue reference: `int& ref`.
>- When used in a unary context in an expression, & is the address-of operator: `std::cout << &x`.
>- When used in a binary context in an expression, & is the Bitwise AND operator: `std::cout << x & y`.


### The dereference operator (*)

The **dereference operator** (`*`) (also occasionally called the **indirection operator**) returns the value at a given memory address as an lvalue:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    std::cout << x << '\n';  // print the value of variable x
    std::cout << &x << '\n'; // print the memory address of variable x

    std::cout << *(&x) << '\n'; // print the value at the memory address of variable x (parentheses not required, but make it easier to read)

    return 0;
```

Output example

```
5
0027FEA0
5
```


>[!tip]
>The address-of operator (`&`) and dereference operator (`*`) works as opposites: address-of gets the address of an object, and dereference gets the object at an address.


### Pointers

A **pointer** is an object that holds a _memory address_ (typically of another variable) as its value. This allows us to store the address of some other object to use later.

A type that specifies a pointer (e.g. `int*`) is called a **pointer type**. Much like reference types are declared using an ampersand (&) character, pointer types are declared using an asterisk (*):

```cpp
int;  // a normal int
int&; // an lvalue reference to an int value

int*; // a pointer to an int value (holds the address of an integer value)
```

To create a pointer variable, we simply define a variable with a pointer type:

```cpp
#include <iostream>

int main()
{

    int x { 5 };
    int& ref { x };
    int* ptr = &ref;
    
    std::cout << "x: " << x << '\n';
    std::cout << "&x: " << &x << '\n';
    std::cout << "ref: " << ref << '\n';
    std::cout << "&ref: " << &ref << '\n';
    std::cout << "ptr: " << ptr << '\n';
    std::cout << "*ptr: " << *ptr << '\n';
    
    return 0;
}
```

Output example

```
x: 5
&x: 0x7ffe31da0714
ref: 5
&ref: 0x7ffe31da0714
ptr: 0x7ffe31da0714
*ptr: 5
```

### Pointer initialization

Like normal variables, pointers are _not_ initialized by default. A pointer that has not been initialized is sometimes called a **wild pointer**. Wild pointers contain a garbage address, and dereferencing a wild pointer will result in undefined behavior. Because of this, you should always initialize your pointers to a known value.

```cpp
int main()
{
    int x{ 5 };

    int* ptr;        // an uninitialized pointer (holds a garbage address)
    int* ptr2{};     // a null pointer (we'll discuss these in the next lesson)
    int* ptr3{ &x }; // a pointer initialized with the address of variable x

    return 0;
}
```

Once we have a pointer holding the address of another object, we can then use the dereference operator (*) to access the value at that address. For example:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    std::cout << x << '\n'; // print the value of variable x

    int* ptr{ &x }; // ptr holds the address of x
    std::cout << *ptr << '\n'; // use dereference operator to print the value at the address that ptr is holding (which is x's address)

    return 0;
}
```

This prints:

```
5
5
```

Much like the type of a reference has to match the type of object being referred to, the type of the pointer has to match the type of the object being pointed to:

```cpp
int main()
{
    int i{ 5 };
    double d{ 7.0 };

    int* iPtr{ &i };     // ok: a pointer to an int can point to an int object
    int* iPtr2 { &d };   // not okay: a pointer to an int can't point to a double object
    double* dPtr{ &d };  // ok: a pointer to a double can point to a double object
    double* dPtr2{ &i }; // not okay: a pointer to a double can't point to an int object

    return 0;
}
```

With one exception that we’ll discuss next lesson, initializing a pointer with a literal value is disallowed:

```cpp
int* ptr{ 5 }; // not okay
int* ptr{ 0x0012FF7C }; // not okay, 0x0012FF7C is treated as an integer literal
```


### Pointers and assignment

We can use assignment with pointers in two different ways:

1. To change what the pointer is pointing at (by assigning the pointer a new address)
2. To change the value being pointed at (by assigning the dereferenced pointer a new value)

First, let’s look at a case where a pointer is changed to point at a different object:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int* ptr{ &x }; // ptr initialized to point at x

    std::cout << *ptr << '\n'; // print the value at the address being pointed to (x's address)

    int y{ 6 };
    ptr = &y; // // change ptr to point at y

    std::cout << *ptr << '\n'; // print the value at the address being pointed to (y's address)

    return 0;
}
```

```
5
5
```

Now let’s look at how we can also use a pointer to change the value being pointed at:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int* ptr{ &x }; // initialize ptr with address of variable x

    std::cout << x << '\n';    // print x's value
    std::cout << *ptr << '\n'; // print the value at the address that ptr is holding (x's address)

    *ptr = 6; // The object at the address held by ptr (x) assigned value 6 (note that ptr is dereferenced here)

    std::cout << x << '\n';
    std::cout << *ptr << '\n'; // print the value at the address that ptr is holding (x's address)

    return 0;
}
```

```
5
5
6
6
```

With pointers, we need to explicitly get the address to point at, and we have to explicitly dereference the pointer to get the value.

The are some other differences between pointers and references worth mentioning:

- References must be initialized, pointers are not required to be initialized (but should be).
- References are not objects, pointers are.
- References can not be reseated (changed to reference something else), pointers can change what they are pointing at.
- References must always be bound to an object, pointers can point to nothing.
- References are “safe” (outside of dangling references), pointers are inherently dangerous.

<h5>The address-of operator returns a pointer</h5>

It’s worth noting that the address-of operator (&) doesn’t return the address of its operand as a literal (as C++ doesn’t support address literals). Instead, it returns a pointer to the operand (whose value is the address of the operand). In other words, given variable `int x`, `&x` returns an `int*` holding the address of `x`.

We can see this in the following example:

```cpp
#include <iostream>
#include <typeinfo>

int main()
{
	int x{ 4 };
	std::cout << typeid(x).name() << '\n';  // print the type of x
	std::cout << typeid(&x).name() << '\n'; // print the type of &x

	return 0;
}
```

On Visual Studio Code

```
i
Pi
```


### Dangling pointers

A **dangling pointer** is a pointer that is holding the address of an object that is no longer valid (e.g. because it has been destroyed).

Dereferencing a dangling pointer will lead to undefined behavior, as you are trying to access an object that is no longer valid.

Here's an example of creating a dangling pointer:


```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int* ptr{ &x };

    std::cout << *ptr << '\n'; // valid

    {
        int y{ 6 };
        ptr = &y;

        std::cout << *ptr << '\n'; // valid
    } // y goes out of scope, and ptr is now dangling

    std::cout << *ptr << '\n'; // undefined behavior from dereferencing a dangling pointer

    return 0;
}
```


The above program will probably print

```
5
6
6
```



## Null  pointers

A pointer can hold a **null value**. A **null value** is a special value that means something has no value.

```cpp
int main()
{
    int* ptr {}; // ptr is now a null pointer, and is not holding an address

    return 0;
}
```

> [!tip] Best practice
> Value initialize your pointers (to be null pointers) if you are not initializing them with the address of a valid object


### The `nullptr` keyword

The `nullptr` keyword represents a null pointer literal. We can use `nullptr` to explicitly initialize or assign a pointer a null value.

```cpp
int main()
{
    int* ptr { nullptr }; // can use nullptr to initialize a pointer to be a null pointer

    int value { 5 };
    int* ptr2 { &value }; // ptr2 is a valid pointer
    ptr2 = nullptr; // Can assign nullptr to make the pointer a null pointer

    someFunction(nullptr); // we can also pass nullptr to a function that has a pointer parameter

    return 0;
}
```


>[!tip] Best practice
>Use `nullptr` when you need a null pointer literal for initialization, assignment, or passing a null pointer to a function.


>[!warning]
>Dereferencing a null pointer results in undefined behavior


### Checking for null pointers
We can use a conditional to test whether a pointer has value `nullptr` or not:

```cpp
#include <iostream>

int main()
{
    int x { 5 };
    int* ptr { &x };

    if (ptr == nullptr) // explicit test for equivalence
        std::cout << "ptr is null\n";
    else
        std::cout << "ptr is non-null\n";

    int* nullPtr {};
    std::cout << "nullPtr is " << (nullPtr==nullptr ? "null\n" : "non-null\n"); // explicit test for equivalence

    return 0;
}
```

```
ptr is non-null
nullPtr is null
```

A null pointer converts to Boolean value `false` and a non-null pointer converts to Boolean value `true`. This allows us to skip explicitly testing for `nullptr` and just use the implicit conversion to Boolean to test whether a pointer is a null pointer.

```cpp
#include <iostream>

int main()
{
    int x { 5 };
    int* ptr { &x };

    // pointers convert to Boolean false if they are null, and Boolean true if they are non-null
    if (ptr) // implicit conversion to Boolean
        std::cout << "ptr is non-null\n";
    else
        std::cout << "ptr is null\n";

    int* nullPtr {};
    std::cout << "nullPtr is " << (nullPtr ? "non-null\n" : "null\n"); // implicit conversion to Boolean

    return 0;
}
```


> [!warning]
> When an object is destroyed, any pointers to the destroyed object will be left dangling (they will not be automatically set to `nullptr`). It is your responsibility to detect these cases and ensure those pointers are subsequently set to `nullptr`.

> [!tip] Best practice
> Favor references over pointers unless the additional capabilities provided by pointers are needed.


## Pointers and const

### Pointer to const value

A **pointer to a const value** (sometimes called a `pointer to const` for short) is a (non-const) pointer that points to a constant value.

To declare a pointer to a const value, use the `const` keyword before the pointer’s data type:

```cpp
int main()
{
    const int x{ 5 };
    const int* ptr { &x }; // okay: ptr is pointing to a "const int"

    *ptr = 6; // not allowed: we can't change a const value

    return 0;
}
```


However, because a pointer to const is not const itself (it just points to a const value), we can change what the pointer is pointing at by assigning the pointer a new address:

```cpp
int main()
{
    const int x{ 5 };
    const int* ptr { &x }; // ptr points to const int x

    const int y{ 6 };
    ptr = &y; // okay: ptr now points at const int y

    return 0;
}
```

Just like a reference to const, a pointer to const can point to non-const variables too. A pointer to const treats the value being pointed to as constant, regardless of whether the object at that address was initially defined as const or not:

```cpp
int main()
{
    int x{ 5 }; // non-const
    const int* ptr { &x }; // ptr points to a "const int"

    *ptr = 6;  // not allowed: ptr points to a "const int" so we can't change the value through ptr
    x = 6; // allowed: the value is still non-const when accessed through non-const identifier x

    return 0;
}
```


### Const pointers

We can also make a pointer itself constant. A **const pointer** is a pointer whose address can not be changed after initialization.

To declare a const pointer, use the `const` keyword after the asterisk in the pointer declaration

```cpp
int main()
{
    int x{ 5 };
    int* const ptr { &x }; // const after the asterisk means this is a const pointer

    return 0;
}
```


Just like a normal const variable, a const pointer must be initialized upon definition, and this value can’t be changed via assignment:

```cpp
int main()
{
    int x{ 5 };
    int y{ 6 };

    int* const ptr { &x }; // okay: the const pointer is initialized to the address of x
    ptr = &y; // error: once initialized, a const pointer can not be changed.

    return 0;
}
```


However, because the _value_ being pointed to is non-const, it is possible to change the value being pointed to via dereferencing the const pointer:

```cpp
int main()
{
    int x{ 5 };
    int* const ptr { &x }; // ptr will always point to x

    *ptr = 6; // okay: the value being pointed to is non-const

    return 0;
}
```

### Const pointer to a const value

Finally, it is possible to declare a **const pointer to a const value** by using the `const` keyword both before the type and after the asterisk:

```cpp
int main()
{
    int value { 5 };
    const int* const ptr { &value }; // a const pointer to a const value

    return 0;
}
```

A const pointer to a const value can not have its address changed, nor can the value it is pointing to be changed through the pointer. It can only be dereferenced to get the value it is pointing at.

## Pass by address

We've covered two different ways to pass an argument to a function: **[[#Introduction to function parameters and arguments#Unreferenced parameters and unnamed parameters|pass by value]]**
and **[[#Pass by lvalue reference|pass by lvalue reference]]**. C++ provides a third way to pass values to a function, called pass by address. Wtih **pass by address**, instead of providing an object as an argument, the caller provides an object's address (via a pointer). This pointer (holding the address of the object) is copied into a pointer parameter of the called function (which now also holds the address of the object). The function can then dereference that pointer to access the object whose address was passed.

```cpp
#include <iostream>
#include <string>

void printByValue(std::string val) // The function parameter is a copy of str
{
    std::cout << val << '\n'; // print the value via the copy
}

void printByReference(const std::string& ref) // The function parameter is a reference that binds to str
{
    std::cout << ref << '\n'; // print the value via the reference
}

void printByAddress(const std::string* ptr) // The function parameter is a pointer that holds the address of str
{
    std::cout << *ptr << '\n'; // print the value via the dereferenced pointer
}

int main()
{
    std::string str{ "Hello, world!" };

    printByValue(str); // pass str by value, makes a copy of str
    printByReference(str); // pass str by reference, does not make a copy of str
    printByAddress(&str); // pass str by address, does not make a copy of str

    return 0;
}
```


 When the function is called, we can’t just pass in the `str` object -- we need to pass in the address of `str`. The easiest way to do that is to use the address-of operator (&) to get a pointer holding the address of `str`:

```cpp
printByAddress(&str); // use address-of operator (&) to get pointer holding address of str
```

When this call is executed, `&str` will create a pointer holding the address of `str`. This address is then copied into function parameter `ptr` as part of the function call. Because `ptr` now holds the address of `str`, when the function dereferences `ptr`, it will get the value of `str`, which the function prints to the console.

That’s it.

Although we use the address-of operator in the above example to get the address of `str`, if we already had a pointer variable holding the address of `str`, we could use that instead:

```cpp
int main()
{
    std::string str{ "Hello, world!" };

    printByValue(str); // pass str by value, makes a copy of str
    printByReference(str); // pass str by reference, does not make a copy of str
    printByAddress(&str); // pass str by address, does not make a copy of str

    std::string* ptr { &str }; // define a pointer variable holding the address of str
    printByAddress(ptr); // pass str by address, does not make a copy of str

    return 0;
}
```



> [!note]
> Pass by address does not make a copy of the object being pointed to

<h5>Pass by address allows the function to modify the argument's value</h5>
 If the function parameter is a pointer to non-const, the function can modify the argument via the pointer parameter.

If a function is not supposed to modify the object being passed in, the function parameter should be made a pointer-to-const:

```cpp
void changeValue(const int* ptr) // note: ptr is now a pointer to a const
{
    *ptr = 6; // error: can not change const value
}
```

> [!tip] Best practice
> Prefer pointer-to-const function parameters over pointer-to-non-const function parameters, unless the function needs to modify the object passed in.
> Do not make function parameters const pointers unless the is some specific reason to do so.


### Null checking

If we have a function `foo(*ptr)`, if `ptr` is a null pointer, the function parameter `ptr` will also be a null pointer. When this null pointer is dereferenced in the body of the function, undefined behavior results.

When passing a parameter by address, care should be taken to ensure the pointer is not a null pointer before you dereference the value. 

```cpp
#include <iostream>

void print(int* ptr)
{
    if (!ptr) // if ptr is a null pointer, early return back to the caller
        return;

    // if we reached this point, we can assume ptr is valid
    // so no more testing or nesting required

    std::cout << *ptr << '\n';
}

int main()
{
	int x{ 5 };

	print(&x);
	print(nullptr);

	return 0;
}
```


If a null pointer should never be passed to the function, an `assert` can be used instead.

```cpp
#include <iostream>
#include <cassert>

void print(const int* ptr) // now a pointer to a const int
{
	assert(ptr); // fail the program in debug mode if a null pointer is passed (since this should never happen)

	// (optionally) handle this as an error case in production mode so we don't crash if it does happen
	if (!ptr)
		return;

	std::cout << *ptr << '\n';
}

int main()
{
	int x{ 5 };

	print(&x);
	print(nullptr);

	return 0;
}
```


> [!tip] Best practice
> Prefer pass by reference to pass by address unless you have a specific reason to use pass by address.

## Pass by address (part 2)


<h5>Changing what a pointer parameter points at</h5>

When we pass an address to a function, that address is copied from the argument into the pointer parameter (which is fine, because copying an address is fast). Now consider the following program:

```cpp
#include <iostream>

// [[maybe_unused]] gets rid of compiler warnings about ptr2 being set but not used
void nullify([[maybe_unused]] int* ptr2)
{
    ptr2 = nullptr; // Make the function parameter a null pointer
}

int main()
{
    int x{ 5 };
    int* ptr{ &x }; // ptr points to x

    std::cout << "ptr is " << (ptr ? "non-null\n" : "null\n");

    nullify(ptr);

    std::cout << "ptr is " << (ptr ? "non-null\n" : "null\n");
    return 0;
}
```

This program prints:

```
ptr is non-null
ptr is non-nul
```

As you can see, changing the address held by the pointer parameter had no impact on the address held by the argument (`ptr` still points at `x`).

So what if we want to allow a function to change what a pointer argument points to?

<h5>Pass by address... by reference?</h5>

Just like we can pass a normal variable by reference, we can also pass pointers by reference.

```cpp
#include <iostream>

void nullify(int*& refptr) // refptr is now a reference to a pointer
{
    refptr = nullptr; // Make the function parameter a null pointer
}

int main()
{
    int x{ 5 };
    int* ptr{ &x }; // ptr points to x

    std::cout << "ptr is " << (ptr ? "non-null\n" : "null\n");

    nullify(ptr);

    std::cout << "ptr is " << (ptr ? "non-null\n" : "null\n");
    return 0;
}
```


This program prints:

```
ptr is non-null
ptr is null
```

Because `refptr` is now a reference to a pointer, when `ptr` is passed as an argument, `refptr` is bound to `ptr`. This means any changes to `refptr` are made to `ptr`.

> [!warning]
> `int&*` will throw an error by the compiler because you can't have a pointer to a reference (because pointers must hold the address of an object, and references aren't objects).



## Return by reference and return by address

In cases where we’re passing a class type back to the caller, we may (or may not) want to return by reference instead. **Return by reference** returns a reference that is bound to the object being returned, which avoids making a copy of the return value. To return by reference, we simply define the return value of the function to be a reference type:

```cpp
std::string&       returnByReference(); // returns a reference to an existing std::string (cheap)
const std::string& returnByReferenceToConst(); // returns a const reference to an existing std::string (cheap)
```

Here is an academic program to demonstrate the mechanics of return by reference:

```cpp
#include <iostream>
#include <string>

const std::string& getProgramName() // returns a const reference
{
    static const std::string s_programName { "Calculator" }; // has static duration, destroyed at end of program

    return s_programName;
}

int main()
{
    std::cout << "This program is named " << getProgramName();

    return 0;
}
```

This program prints:

```
This program is named Calculator
```


<h5>The object being returned by reference must exist after the function returns</h5>
Using return by reference has one major caveat: the programmer _must_ be sure that the object being referenced outlives the function returning the reference. Otherwise, the reference being returned will be left dangling (referencing an object that has been destroyed), and use of that reference will result in undefined behavior.

In the program above, because `s_programName` has static duration, `s_programName` will exist until the end of the program. When `main()` accesses the returned reference, it is actually accessing `s_programName`, which is fine, because `s_programName` won’t be destroyed until later.

Now let’s modify the above program to show what happens in the case where our function returns a dangling reference:

```cpp
#include <iostream>
#include <string>

const std::string& getProgramName()
{
    const std::string programName { "Calculator" }; // now a non-static local variable, destroyed when function ends

    return programName;
}

int main()
{
    std::cout << "This program is named " << getProgramName(); // undefined behavior

    return 0;
}
```

The result of this program is undefined. When `getProgramName()` returns, a reference bound to local variable `programName` is returned. Then, because `programName` is a local variable with automatic duration, `programName` is destroyed at the end of the function. That means the returned reference is now dangling, and use of `programName` in the `main()` function results in undefined behavior.

> [!warning]
> Objects returned y reference must live beyond the scope of the function returning the reference, or a dangling reference will result. Never return a (non-static) local variable or temporary by reference.


<h5>Lifetime extension doesn't work across function boundaries</h5>

Let’s take a look at an example where we return a temporary by reference:

```cpp
#include <iostream>

const int& returnByConstReference()
{
    return 5; // returns const reference to temporary object
}

int main()
{
    const int& ref { returnByConstReference() };

    std::cout << ref; // undefined behavior

    return 0;
}
```

In the above program, `returnByConstReference()` is returning an integer literal, but the return type of the function is `const int&`. This results in the creation and return of a temporary reference bound to a temporary object holding value 5. This returned reference is copied into a temporary reference in the scope of the caller. The temporary object then goes out of scope, leaving the temporary reference in the scope of the caller dangling.

By the time the temporary reference in the scope of the caller is bound to const reference variable `ref` (in `main()`), it is too late to extend the lifetime of the temporary object -- as it has already been destroyed. Thus `ref` is a dangling reference, and use of the value of `ref` will result in undefined behavior.

Here’s a less obvious example that similarly doesn’t work:

```cpp
#include <iostream>

const int& returnByConstReference(const int& ref)
{
    return ref;
}

int main()
{
    // case 1: direct binding
    const int& ref1 { 5 }; // extends lifetime
    std::cout << ref1 << '\n'; // okay

    // case 2: indirect binding
    const int& ref2 { returnByConstReference(5) }; // binds to dangling reference
    std::cout << ref2 << '\n'; // undefined behavior

    return 0;
}
```

In case 2, a temporary object is created to hold value `5`, which function parameter `ref` binds to. The function just returns this reference back to the caller, which then uses the reference to initialize `ref2`. Because this is not a direct binding to the temporary object (as the refrence was bounced through a function), lifetime extension doesn’t apply. This leaves `ref2` dangling, and its subsequent use is undefined behavior.


<h5>Don't return non-const static local variables by reference</h5>

In the original example above, we returned a const static local variable by reference to illustrate the mechanics of return by reference in a simple way. However, returning non-const static local variables by reference is fairly non-idiomatic, and should generally be avoided. Here’s a simplified example that illustrates one such problem that can occur:

```cpp
#include <iostream>
#include <string>

const int& getNextId()
{
    static int s_x{ 0 }; // note: variable is non-const
    ++s_x; // generate the next id
    return s_x; // and return a reference to it
}

int main()
{
    const int& id1 { getNextId() }; // id1 is a reference
    const int& id2 { getNextId() }; // id2 is a reference

    std::cout << id1 << id2 << '\n';

    return 0;
}
```

This program prints:

```
22
```

This happens because `id1` and `id2` are referencing the same object (the static variable `s_x`), so when anything (e.g. `getNextId()`) modifies that value, all references are now accessing the modified value.

>[!tip] Best practice
>Avoid returning references to non-const local static variables.



<h5>Assigning/initializing a normal variable with a returned reference makes a copy</h5>

If a function returns a reference, and that reference is used to initialize or assign to a non-reference variable, the return value will be copied (as if it had been returned by value).

```cpp
#include <iostream>
#include <string>

const int& getNextId()
{
    static int s_x{ 0 };
    ++s_x;
    return s_x;
}

int main()
{
    const int id1 { getNextId() }; // id1 is a normal variable now and receives a copy of the value returned by reference from getNextId()
    const int id2 { getNextId() }; // id2 is a normal variable now and receives a copy of the value returned by reference from getNextId()

    std::cout << id1 << id2 << '\n';

    return 0;
}
```

In the above example, `getNextId()` is returning a reference, but `id1` and `id2` are non-reference variables. In such a case, the value of the returned reference is copied into the normal variable. Thus, this program prints:

```
12
```


It’s okay to return reference parameters by reference
If a parameter is passed into a function by reference, it’s safe to return that parameter by reference. This makes sense: in order to pass an argument to a function, the argument must exist in the scope of the caller. When the called function returns, that object must still exist in the scope of the caller


## In and out parameters


## Type deduction with pointers, references, and const

## std::optional





# More on Classes

## Friend classes and friend member functions

A **friend class** is a class that can access the private and protected members of another class.

Example:

```cpp
#include <iostream>

class Storage
{
private:
    int m_nValue {};
    double m_dValue {};
public:
    Storage(int nValue, double dValue)
       : m_nValue { nValue }, m_dValue { dValue }
    { }

    // Make the Display class a friend of Storage
    friend class Display;
};

class Display
{
private:
    bool m_displayIntFirst {};

public:
    Display(bool displayIntFirst)
         : m_displayIntFirst { displayIntFirst }
    {
    }

    // Because Display is a friend of Storage, Display members can access the private members of Storage
    void displayStorage(const Storage& storage)
    {
        if (m_displayIntFirst)
            std::cout << storage.m_nValue << ' ' << storage.m_dValue << '\n';
        else // display double first
            std::cout << storage.m_dValue << ' ' << storage.m_nValue << '\n';
    }

    void setDisplayIntFirst(bool b)
    {
         m_displayIntFirst = b;
    }
};

int main()
{
    Storage storage { 5, 6.7 };
    Display display { false };

    display.displayStorage(storage);

    display.setDisplayIntFirst(true);
    display.displayStorage(storage);

    return 0;
}
```

Because the `Display` class is a friend of `Storage`, `Display` members can access the private members of any `Storage` object they have access to.

This program produces the following result:

```
6.7 5
5 6.7
```

A few additional notes on friend classes.

- First, even though `Display` is a friend of `Storage`, `Display` has no access to the `*this` pointer of `Storage` objects (because `*this` is actually a function parameter).
- Second, friendship is not reciprocal. 
- Class friendship is also not transitive. If class A is a friend of B, and B is a friend of C, that does not mean A is a friend of C.


### Friend member functions

Instead of making an entire class a friend, you can make a single member function a friend. This is done similarly to making a non-member function a friend, except the name of the member function is used instead.

However, in actuality, this can be a little trickier than expected. Let’s convert the previous example to make `Display::displayStorage` a friend member function. You might try something like this:

```cpp
#include <iostream>

class Display; // forward declaration for class Display

class Storage
{
private:
	int m_nValue {};
	double m_dValue {};
public:
	Storage(int nValue, double dValue)
		: m_nValue { nValue }, m_dValue { dValue }
	{
	}

	// Make the Display::displayStorage member function a friend of the Storage class
	friend void Display::displayStorage(const Storage& storage); // error: Storage hasn't seen the full definition of class Display
};

class Display
{
private:
	bool m_displayIntFirst {};

public:
	Display(bool displayIntFirst)
		: m_displayIntFirst { displayIntFirst }
	{
	}

	void displayStorage(const Storage& storage)
	{
		if (m_displayIntFirst)
			std::cout << storage.m_nValue << ' ' << storage.m_dValue << '\n';
		else // display double first
			std::cout << storage.m_dValue << ' ' << storage.m_nValue << '\n';
	}
};

int main()
{
    Storage storage { 5, 6.7 };
    Display display { false };
    display.displayStorage(storage);

    return 0;
}
```

However, it turns out this won’t work. ==In order to make a single member function a friend, the compiler has to have seen the full definition for the class of the friend member function== (not just a forward declaration). Since class `Storage` hasn’t seen the full definition for class `Display` yet, the compiler will error at the point where we try to make the member function a friend.

Fortunately, this is easily resolved by moving the definition of class `Display` before the definition of class `Storage` (either in the same file, or by moving the definition of `Display` to a header file and `#including` it before `Storage` is defined).

```cpp
#include <iostream>

class Display
{
private:
	bool m_displayIntFirst {};

public:
	Display(bool displayIntFirst)
		: m_displayIntFirst { displayIntFirst }
	{
	}

	void displayStorage(const Storage& storage) // compile error: compiler doesn't know what a Storage is
	{
		if (m_displayIntFirst)
			std::cout << storage.m_nValue << ' ' << storage.m_dValue << '\n';
		else // display double first
			std::cout << storage.m_dValue << ' ' << storage.m_nValue << '\n';
	}
};

class Storage
{
private:
	int m_nValue {};
	double m_dValue {};
public:
	Storage(int nValue, double dValue)
		: m_nValue { nValue }, m_dValue { dValue }
	{
	}

	// Make the Display::displayStorage member function a friend of the Storage class
	friend void Display::displayStorage(const Storage& storage); // okay now
};

int main()
{
    Storage storage { 5, 6.7 };
    Display display { false };
    display.displayStorage(storage);

    return 0;
}
```


However, we now have another problem. Because member function `Display::displayStorage()` uses `Storage` as a reference parameter, and we just moved the definition of `Storage` below the definition of `Display`, the compiler will complain it doesn’t know what a `Storage` is. We can’t fix this one by rearranging the definition order, because then we’ll undo our previous fix.

Fortunately, this is also fixable. First, we can add `class Storage` as a forward declaration so the compiler will be okay with a reference to `Storage` before it has seen the full definition of the class.

Second, we can move the definition of `Display::displayStorage()` out of the class, after the full definition of `Storage` class.

```cpp
#include <iostream>

class Storage; // forward declaration for class Storage

class Display
{
private:
	bool m_displayIntFirst {};

public:
	Display(bool displayIntFirst)
		: m_displayIntFirst { displayIntFirst }
	{
	}

	void displayStorage(const Storage& storage); // forward declaration for Storage needed for reference here
};

class Storage // full definition of Storage class
{
private:
	int m_nValue {};
	double m_dValue {};
public:
	Storage(int nValue, double dValue)
		: m_nValue { nValue }, m_dValue { dValue }
	{
	}

	// Make the Display::displayStorage member function a friend of the Storage class
	// Requires seeing the full definition of class Display (as displayStorage is a member)
	friend void Display::displayStorage(const Storage& storage);
};

// Now we can define Display::displayStorage
// Requires seeing the full definition of class Storage (as we access Storage members)
void Display::displayStorage(const Storage& storage)
{
	if (m_displayIntFirst)
		std::cout << storage.m_nValue << ' ' << storage.m_dValue << '\n';
	else // display double first
		std::cout << storage.m_dValue << ' ' << storage.m_nValue << '\n';
}

int main()
{
    Storage storage { 5, 6.7 };
    Display display { false };
    display.displayStorage(storage);

    return 0;
}
```

Now everything will compile properly: the forward declaration of `class Storage` is enough to satisfy the declaration of `Display::displayStorage()` inside the `Display` class. The full definition of `Display` satisfies declaring `Display::displayStorage()` as a friend of `Storage`. And the full definition of class `Storage` is enough to satisfy the definition of member function `Display::displayStorage()`.


This dance is only necessary because we’re trying to do everything in a single file. A better solution is to put each class definition in a separate header file, with the member function definitions in corresponding .cpp files. That way, all of the class definitions would be available in the .cpp files, and no rearranging of classes or functions is necessary!


# Dynamic Allocation

## Dynamic memory allocation with new and delete

C++ supports three basic types of memory allocation, of which you’ve already seen two.

- **Static memory allocation** happens for static and global variables. Memory for these types of variables is allocated once when your program is run and persists throughout the life of your program.
- **Automatic memory allocation** happens for function parameters and local variables. Memory for these types of variables is allocated when the relevant block is entered, and freed when the block is exited, as many times as necessary.
- **Dynamic memory allocation** is the topic of this article.

Both static and automatic allocation have two things in common:

- The size of the variable / array must be known at compile time.
- Memory allocation and deallocation happens automatically (when the variable is instantiated / destroyed).


The most normal variables (including fixed arrays) are allocated in a portion of memory called the **stack**. The amount of stack memory for a program is generally quite small. If you exceed this number, stack overflow will result, and the operating system will probably close down the program.

**Dynamic memory allocation** is a way for running programs to request memory from the operating system when needed. This memory does not come from the program's limited stack memory, instead it is allocated from a much larger pool of memory managed by the operating system called the **heap**. The heap can be gigabytes in size.






## Dynamically allocating arrays



## Destructors

## Pointers to pointers and dynamic multidimensional arrays



## Void pointers







# Operator Overloading

## Introduction to operator overloading





# Move Semantics and Smart Pointers

## Introduction to smart pointers and move semantics


## R-value references



## Move constructors and move assignment




## `std::move`



## `std::unique_ptr`




## `std::shared_ptr`





