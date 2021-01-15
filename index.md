# JavaScript Basics

This document introduces the basics of JavaScript syntax, highlighting some ways in which JavaScript differs from other languages like Python, Java, or C#.

## Running JavaScript programs

Two main environments

### Browser (client-side JavaScript)
- All browsers have a built-in JavaScript interpreter
- Programs run in a 'sandox' (certain operations are not allowed or require explicit permission, e.g. access to file system)
- 

Client-side JS usually runs in the context of a web page...
```html
<html>
<head>
    ...
    <script>
        console.log("Hello, world!");
    </script>
    ...
</head>
<body>
    ...
</body>
</html>
```
  
### Node.js (server-side JavaScript)
- Node.js is a JavaScript interpreter that can run JS programs independently of a browser
- Not sandboxed, no restrictions

Server-side JS can run as a stand-alone program...
```js
console.log("Hellow, world!")
```

## JavaScript Syntax Basics

- To avoid common pitfalls of JS syntax, best practice is to include the `"use strict"` directive at the beginning of all JS scripts.
- Case sensitive (foo and Foo are two different terms)
- Instructions end in semi-colons (not always necessary but considered best-practice)
- Indentation is NOT part of the syntax.  Instead, curly braces are used to indicate blocks of code like conditional/loop/function bodies

The following two JS snippets are syntactically equivalent (but which is more readable?):

```js
function foo() { 
    let name = "Ali"; 
    console.log("Hello, " + name + "!"); 
}
```

```js
function foo() { let name = "Ali"; console.log("Hello, " + name + "!"); }
```

### Indentation

While indentation is not syntactically important, using careful indentation *does* make your code more readable, and all programmers should strive for proper code formatting.

Typically:
- All lines of code within a curly brace should be indented one level from the opening brace.
- The closing brace should be 'outdented' back to the same level as that of the opening brace

### Naming Conventions

In JS, convention is to name things using 'camel casing'

```js
let myVariable = 1;   // Prefer this...
let my_variable = 1;  // ...over this
```

## Comments

```js
// This is a one-line comment
// This is another one-line comment
let x = 1;  // Everything after the slash until the end of the line is a comment

/* This is a multi-line comment.
It can span multiple lines.
Everything inside the opening slash-star 
and the closing star-slash is a comment */
```

## Types and Values

The `typeof` operator can be used to determine the type of a value (like Python's `type()` function)
```js
typeof 1            // 'number'
typeof "hi"         // 'string'
typeof true         // 'boolean'
typeof console.log  // 'function'
typeof []           // 'object'
```

There are only a few more built-in types than the ones shown above.  But there are many built-in objects, and the `instanceof` operator can be used to determine the precise kind of object a value is:

```js
[] instanceof Array  // Yields: true
```

### Numbers

```js
1           // An integer
1.23        // A decimal number
1.23e-5     // A decimal number using scientific notation
NaN         // 'not a number', for example 0/0 == NaN
```

#### Arithmetic operators

```js
1 + 2       // Addition
1 - 2       // Subtraction
1 * 2       // Multiplication
1 / 2       // Division
2 ** 3      // Exponentiation (new in ES7)
9 % 7       // Modulus (the remainder when 9 is divided by 7)
```

### Strings

```js
'Strings can be surrounded by single quotes'
"Or by double quotes"
`Or by backticks`
```

Backtick strings are called 'template' strings because you can inject the value of JS expressions into them directly rather than using the string concatenation operator, +.

Both lines of code below do the same thing:

```js
"The sum of the first three integers is " + (1+2+3)
`The sum of the first three integers is ${1+2+3}`
```

#### [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#instance_methods) Operations

```js
"a" + "b"              // Yields "ab"  (concatenation)
"a".repeat(3)          // Yields "aaa" (repetition)
"abcdef".indexOf("d")  // Yields: 3 
"abcdef".indexOf("z")  // Yields: -1
"abcdef".includes("d") // Yields: true
"abc".toUpperCase()    // Yields "ABC"
"ABC".toLowerCase()    // Yields "abc"
"  abc  ".trim()       // Yields: "abc"
"a,b,c".split(",")     // Yields: ['a', 'b', 'c']

// Strings can be sliced:
"Super duper!".slice(2,5)    // Yields "per"
"Super duper!".slice(6)      // Yields "duper!"
"Super duper!".slice(-1)     // Yields "!"
```

#### Escape sequences

You can use the backslash to create 'escape sequences' for certain special symbols in a string...

```js
'I\'ve got a single quote inside a single-quoted string!'
'First line\nSecond line'
```

#### Immutability of Strings

Strings are immutable:

```js
let s = "abcdef";
s[0] = "z";
console.log(s);    // Prints 'abcdef'
```

### Booleans

JS has two boolean literals: `true` and `false`.

#### Comparison operators

```js
2 == "2"        // Equal (if values can be converted to the same type, they will be!)
2 === 2         // Identical (only true when values have the same type)
2 != 1          // Not equal
3 > 2           // Greater than
2 < 3           // Less than
3 >= 2          // Greater than or equal
2 <= 3          // Less than or equal
```

#### Comparison and Type Coersion

When performing equality comparison (`==`) JS will attempt to automatically convert both operands to the same type before making the comparison.  This is called **Type Coersion**.

The identity comparison operator (`===`) behaves more like the `==` operator you may be used from languages like Python, Java, or C#, and **should be preferred** unless there is a specific reason to use `==`.

```js
5 == "5"        // true 
5 === "5"       // false
1 == true       // true
1 === true      // false
"" == false     // true
"" === false    // true
```

#### Comparison with NaN

The value `NaN` is a bit of a strange duck...

```js
NaN == NaN          // Evaluates to false
NaN === NaN          // Evaluates to false

// Use this instead if you need to check if a value is NaN:
Number.isNaN(NaN)   // Evalues to true
```

#### Logical operators

```js
&&          // and
||          // or
!           // not

// Examples
true && true == true
true || false == true
! false == true
```

### Converting (Casting) Between Types

```js
// String to number
let n = Number("1000")      
let n = Number("NaN")       // This works too
let n = Number("1.23e-6")   // And this

// Number to string
let s = "" + 1000           // Type coersion FTW!
```


### Null and Undefined

JS has two values that represent 'no value': `null` and `undefined`.

There are subtle differences between the two, but for now you can think of them as mostly interchangeable.

### Printing Values

The `console.log` function prints values to the console (like Python's `print` or Java's `System.out.println`).

```js
console.log("Hello, world!");
console.log("Any expression will do " + 1 + 2 * 3 / 4);
```

### Obtaining User Input

There are several ways to obtain user input that will be discussed in this course.  Here, we present the simplest way.  (But this way is not often used in real programs.)

Only in browsers, the `prompt` function may be used to prompt the user for a value.  The user's input is returned from the function as a string.

```js
const response = prompt("What is your name? ");
```

The `prompt` function is NOT available in Node.js.  You must use an NPM package that provides this functionality instead (there are several).

## Bindings (Variables)

Initial declaration of a binding must be done using one of the keywords `let`, `const`, or `var`

```js
let x;       // x is currently 'undefined'
x = 1;       // x is now bound to the value 1
x = 2;       // and now to the value 2

let y = 3;   // Declaration and assignment can be done in a single statement
```

Declaring `const` bindings allows the binding to be assigned only once...

```js
const z = 42;
z = 24;           // Causes a run-time error
```

**NOTE:** Avoid using `var` as it works in an unusual way.  (In short: `var` bindings are 'function-scoped' and `let` bindings are 'block-scoped'.  This will be discussed in more detail in the section on functions.)

### Binding Names

Binding names may include alphabetical symbols, numerical symbols, `$` and/or `_` but may not start with a number.

Binding names may not be a JS keyword.

### Built-in Bindings

There are many bindings built-in to both browsers and Node.js.  We will learn more about these throughout the term.

## Conditionals

```js
if ( conditionExpression ) {
    // instructions to execute if conditionExpression is true
} else if ( otherConditionExpression ) {
    // instructions to execute if otherConditionExpression is true
} else {
    // instructions to execute if none of the above condition expressions were true
}
```

### Switch Statements

If all the condition expressions in a conditional statement are discrete **equality** checks, a switch statement can be more readable and more computationally efficient.

The following two code blocks are equivalent:
```js
if ( condition === 0 ) {
    console.log("Poor");
} else if ( condition === 1 ) {
    console.log("Good");
} else if ( condition === 2 ) {
    console.log("Excellent");
} else {
    console.log("Unknown condition!");
}
```

```js
switch(condition) {
    case 0:
        console.log("Poor");
        break;  // IMPORTANT: Don't forget the break after each case!!
    case 1:
        console.log("Good");
        break;
    case 2:
        console.log("Excellent");
        break;
    default:
        console.log("Unknown condition!");
        break;
}
```

## Loops

### While Loops

```js
while ( conditionExpression ) {
    // Instructions to execute repeatedly until conditionExpression is false
    // (May never be executed!)
}
```

```js
do {
    // Instructions to execute repeatedly until conditionExpression is false
    // (Will be executed at least once!)
} while ( conditionExpression );
// NOTE the ending semi-colon
```

### For loops

The basic for loop in JS is nothing more than a while loop in which all the 'book keeping' is done in one spot.  For example, the two loops below are equivalent:

```js
let i = 0;              // Initialization of counter
while ( i < 10 ) {      // Check counter for exit condition
    console.log(i);
    i += 1;             // Increment counter
}
```

```js
for ( let i = 0 ; i < 10 ; i += 1 ) {
    console.log(i);
}
```

In a basic for loop, initialization, check, and increment are all done inside the parentheses, each separated  by a semi-colon.

### For..of / For..in Loops

JS also has `for..of` and `for..in` loops, the *former* of which operates much like python's `for..in` loop (i.e.  JavaScript's `for..of` works like Python's `for..in`).  These will be discussed further in the section on arrays.

### Exiting Loops

The `break` statement immediately exits a loop and resumes execution at the first instruction after the loop.  

The `continue` statement immediately ends the current iteration of the loop.

## Lists (arrays)

JS arrays (like Python's lists) are zero-indexed.

```js
let a = [1, 2, 3];

a[0] == 1;              // Evaluates to true.
```

All arrays have a `length` property that stores the number of items in the array

```js
[1, 2, 3, 4, 5].length;  // Yields the value 5
```

### Array Operations

```js
let a = [1, 2, 3, 4, 5];

typeof a            // Yields 'object'
a instanceof Array  // Yields: true

a.length            // Yields: 5
a.includes(3)       // Yields: true
a.indexOf(3)        // Yields: 2
a.join("-")         // Yields: "1-2-3-4-5"
a.concat([6. 7, 8]) // Yields: [1, 2, 3, 4, 5, 6, 7, 8]
a.sort()            // Sorts elements of a in-place

// Delete element with index 2
delete a[2]

// Slicing arrays
a.slice(2,4);   // Yields [3, 4]
a.slice(2);     // Yields [3, 4, 5]
a.slice(-2);    // Yields [4, 5]

// Copying arrays
Array.from(a)   // This is the most readable...
a.slice()       // ...but you may see this...
[...a]          // ...or this

// Making arrays out of strings
Array.from("abc")   // Yields ['a', 'b', 'c']
```

### Comparing Arrays

Using `==` to compare arrays works like using `is` to compare lists in Python.

```js
let a = [1, 2, 3];
let b = [1, 2, 3];
let c = a;

a == a      // Yields: true
a == c      // Yields: true
a == b      // Yields: false
```

To check if two arrays contain the same set of values you must traverse the arrays.  There are many possible approaches depending on specific needs.  Here is one example that compares two arrays using strict comparison of values (`===` as opposed to `==`).  This function would fail, though, on multi-dimensional arrays:

```js
function isEqual(arr1, arr2) {
    if ( arr1.length != arr2.length ) {
        return false;
    }

    for ( let i = 0; i < arr1.length; i += 1 ) {
        if ( arr1[i] !== arr2[i] ) {
            return false;
        }
    }
    // If we haven't returned false by now, they're equal!
    return true;
}
```

### Traversing Arrays

JS has both `for..of` and `for..in` loops to traverse iterable values.  The `for..of` loop works much like `for..in` loops in languages like Python:

```js
for ( const item of ['a', 'b', 'c'] ) {
    console.log(item);
}

// Output:
a
b
c
```

**NOTE:** `for..of` loops are useful for traversing any iterable object:

```js
for ( const letter of "supercalifragilisticexpialidocious" ) {
    console.log(letter);
}
```

JS's `for..in` loop iterates over the *index* of the value being iterated, *not* the items.

```js
for ( const i in ['a', 'b', 'c'] ) {
    console.log(i);
}

// Output:
0
1
2
```

### Emulating Python's `range`

```js
let r = Array(5).keys();   // Like Python's range(5)

for ( const n of Array(5).keys() ) {
    // n iterates through the values 0 to 4
}
```

### Filter / Map / Reduce with Arrays

```js
const a = [1, 2, 3, 4, 5]

a.filter(n => n % 2 == 0)   // Yields: [2, 4]
a.map(n => n * 2)          // Yields: [2, 4, 6, 8, 10]
a.reduce((a,b) => a + b)   // Yields: 15 i.e. (1+2+3+4+5)
```

With strings:
```js
const s = "abcdef"

// Yields string containing only the vowels of s:
Array.from(s)
    .filter(x => "aeiou".includes(x))
    .join("")
```

### Array destructuring

The values of an array can be **destructured** into a set of bindings, like so:

```js
const myArray = [1, 2, 3];
const [a, b, c] = myArray;
// Now, a == 1, b == 2, c == 3
```

## Functions

In JS, functions can be treated as values.  The syntax for creating a function and binding it to a name is as follows:

```js
const foo = function() {
    // Instructions to execute when the function is called
};
// NOTE the semi-colon at the end of this assignment expression

foo();  // Calling the above function
```

A function with parameters:
```js
const bar = function(a, b) {
    return a + b;
}

const x = bar(1, 2);  // Calling the above function
```

There is also a shorter syntax for function declarations like the ones above:

```js
function foo() {
    // Instructions to execute when foo is called
}

function bar(a, b) {
    return a + b;
}
```

When declared using the syntax above, calls to the functions may occur *before* the function definitions in the code!

### Arrow Functions

There is a third syntax for function declarations.  Instead of the keyword 'function' before the parenthese, an arrow (`=>`) is placed between the parentheses and the opening curly brace, like so:

```js
const foo = () => {
    // Instructions to execute when foo is called
}

const bar = (a, b) => {
    return a + b;
}
```

If the body of an arrow function is a single expression, the value of that expression is returned automatically, and no curly braces are required.  The declaration of `bar` below is equivalent to all the declarations of `bar` above:

```js
const bar = (a, b) => a + b;  
```

If an arrow function requires only one parameter, the parentheses around the parameter may be omitted as well!

```js
const square = x => x*x;
```

### Higher-order functions

Since functions in JS are values, you can pass them as arguments to functions or return them from other functions.

Functions that return functions or have functions as parameters are called higher-order functions. 

```js
// A higher-order function with a function parameter
function repeat(f, n) {
    for ( let i = 0 ; i < n ; i += 1 ) {
        f();  // Call f
    }
}

// A higher-order function that returns a function
function makeMultiplier(factor) {
    // NOTE that we are returning the function as a value here
    // We are NOT calling
    return number => number * factor;
}
let double = makeMultiplier(2);  // Get the function
double(3);                       // Call the returned function
```

### Functions and Scope

When declared with `let` or `const`, bindings are **block-scoped**, meaning that they are only visible from within the nearest enclosing pair of curly braces.

Example:

```js
let x = 1;                  // In scope: x
                            // Not in scope: y, z, a, b

function foo() {
    let y = 2;              // In scope:  x, y
                            // Not in scope: z, a, b
    while ( x < 10 ) {
        let z = 3;          // In scope: x, y, z
                            // Not in scope: a, b

        if ( (x + y) % 2 ) {
            let a = z + 4;      // In scope: x, y, z, a
                                // Not in scope: b
        } else {
            let b = x + y + 5;  // In scope: x, y, z, b
                                // Not in scope: a
        }
    }
}
```

When declared with `var`, bindings are **function-scoped**, meaning that they are visible anywhere within the nearest enclosing function.

```js
var x = 1;                  // In scope: x
                            // Not in scope: y, z, a, b

function foo() {
                            // In scope: x, y, z, a, b
    var y = 2;              
                            
    while ( x < 10 ) {
        var z = 3;          
                            
        if ( (x + y) % 2 ) {
            var a = z + 4;      
        } else {
            var b = x + y + 5;  
        }
    }
}
```

**NOTE:** `var` was originally the only option for variable declarations in JS, so you will encounter it in older JS code, but since the addition of `const` and `let`, `var` should be avoided.

### Closure

Functions can be (and in JS often are) nested within each other.  The nested function may be a 'helper' function used by the outer function, or it may be a value returned from the function.

For example, the function below returns a function that when called multiplies the given argument with the value that was initially given as the factor when `makeMultiplier` was called:

```js
function makeGreeter(greeting, after) {
    return name => `${greeting}, ${name}!  ${after}`;
}

const greet = makeGreeter("Hello", "Pleased to meet you!");
const greetSarcastically = makeGreeter("Oh, hi", "Soooo nice to see you... 🙄")

greet("Ali");  // Yields "Hello, Ali! Pleased to meet you!"
greetSarcastically("Ali");  // Yields "Oh, hi, Ali!  Soooo nice to see you... 🙄"
```

This is possible because the 'environment' of a function is 'remembered' as part of function's definition when it is created.  Here, the function returned by `makeGreeter` 'remembers' what the value of `greeting` and `after` were when the returned function was created.

This 'remembering' or 'storing' of the state of the environment when a function is created is called *closure*.

Another example:  Make a function that uses the `repeat` function defined above to print a given string a given number of times.

This doesn't work because the first argument must be a function:

```js
function repeatStr(s, n) {
    repeat(console.log(s), n);
}
```

But taking advantage of closure we can wrap the call to `console.log` in an anonymous function so that the first parameter to `repeat` is indeed a function value:

```js
function repeatStr(s, n) {
    repeat(() => console.log(s), n);
}
```

And to summarize the function syntax we've encountered so far, both the following are equivalent to the repeatStr function above:

```js
function repeatStr(s, n) {
    // Declare a nested function that prints the string
    function f() {
        console.log(s);
    }
    // Use it in a call to repeat
    repeat(f, n);
}

function repeatStr(s, n) {
    // Declare an anonymous function expession directly in the call to repeat
    repeat(function() { console.log(s); }, n);
}
```

### Function Documentation

There is a special comment format that is used by convention to document functions (akin to Python's docstrings).  

Many programming tools can parse function comments formatted in this way to automatically produce documentation for a program.

```js
/**
 * @returns {number} The sum of the given numbers
 * @param {number} a One number to add
 * @param {number} b The other number to add
 * 
 * More description can be added if necessary here.
 */
function add(a, b) {
    return a + b;
}
```

**NOTE:**
- Comment starts with `/**` (2 stars instead of the usual 1)
- Each line begins with ` * `
- The `@return` 'keyword' can be used to specificy information about what (if anything) the function returns
- The `@param` 'keyword' can be used to provide information about each parameter
  - one `@param` line per parameter
  - The name of the parameter is included before the description of the parameter
- You can provide type information by including the type inside curly braces, after `@returns` or `@param`, as in `{number}`
- You can add arbitrary documentation in addition to the `@returns` and `@param` lines
- There is [much more](https://jsdoc.app/) you can do with this style of comment, but what you see here is enough to get you started

### Gather and Spread Operators

The `...` operator can be used in a function *declaration* to 'gather' any remaining arguments into an array.

```js
foo(1, 2, 3, 4, 5, 6);
function foo(a, b, ...c) {
    // a == 1
    // b == 2
    // c == [3, 4, 5, 6]
}

```

The `...` operator can be used in a function *call* to 'spread' each of an array's elements into a separate argument.

```js
foo(...[1, 2, 3]);
function foo(a, b, c) {
    // a == 1
    // b == 2
    // c == 3
}

## Maps (dictionaries)

## Objects