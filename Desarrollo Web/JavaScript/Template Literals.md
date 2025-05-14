Template literals are modern way to work with strings, introduced in ES6. They allow you to embed expressions, create multi-line strings, and make string manipulation more dynamic and readable. Template literals backticks instead of quotes. ( \` )
# Features
- **String interpolation:** Embed variables or expressions directly using `$(expresiion)`.
- **Multi-line Strings:** Write strings that span multiple lines without concatenation or escape characters.

# String Interpolation

```javascript
const firsName = "John";
const age = 30;
const message = `Hi, my name is ${firsName}, and I am ${age} years old.`;

console.log(message)
// `Hi, my name is John, and I am 30 years old.
```

# Multi-line Strings

```js
const multiline = `This is the first line.
This is the second line.
This is the third line.`;

console.log(multiline);

/*
This is the first line.
This is the second line.
This is the third line.
*/
```

Template literals allow you to write multi-line strings naturally, without needing `\n`.

# Using Expressions

```js
const num1 = 15;
const num2 = 10;
const sum = `The sum of ${num1} and ${num2} is ${num1 + num2}.`;

console.log(sum);

// The sum of 15 and 10 is 25.
```

You can include any valid JavaScript expression, withing the `${}` syntax.

# Embedding Functions Calls

```js
const greet = (name) => `Hello, ${name}!`;
const message = greet("Alex");

console.log(message);

// Hello, Alex!
```

Function calls and their results can be included withing template literals for dynamic string content.

# Advantages of Template Literals
- Simplifies dynamic string creation.
- Readable multi-line strings.
- Supports embedding of any JavaScript expression.