## 1. What Is Pulsar?

Pulsar is a programming language using `.pulsar` source files.

The language provides core programming features including:

* Variables
* Values
* Types
* Strings
* Numbers
* Booleans
* `null`
* Arrays
* Objects
* Operators
* Expressions
* Conditional statements
* `if / else`
* `for` loops
* `for ... in` loops
* `while` loops
* `break`
* `continue`
* Functions
* `return`
* Arrow functions
* Scope and environments
* Builtins
* JSON operations
* File operations
* HTTP operations
* Environment variables
* Asynchronous operations

---

# 2. Basic Pulsar Program

A minimal program:

```pulsar
define name = "Pulsar";

show(name);
```

Another example:

```pulsar
define a = 10;
define b = 20;

define result = a + b;

show(result);
```

Expected output:

```text
30
```

---

# 3. Variables

Variables are declared with `define`.

```pulsar
define name = "Pulsar";
define age = 20;
define active = true;
```

Variables can contain different values:

```pulsar
define text = "hello";
define number = 100;
define flag = true;
define empty = null;
define numbers = [1, 2, 3];
```

The correct Pulsar declaration keyword is:

```pulsar
define
```

Do not replace it with:

```text
let
var
const
```

unless the Pulsar language implementation specifically adds those keywords.

---

# 4. Values

Pulsar values include:

```text
string
number
boolean
null
array
object
function
```

Examples:

```pulsar
define text = "Hello";
define number = 42;
define enabled = true;
define nothing = null;
define items = [1, 2, 3];

define user = {
    name: "Alex",
    age: 20
};
```

---

# 5. Strings

Strings are written using quotes.

```pulsar
define name = "Pulsar";

show(name);
```

String concatenation:

```pulsar
define name = "Alex";

show("Hello " + name);
```

Multiple values can be combined:

```pulsar
define product = "Laptop";
define price = 1200;

show(product + " costs $" + price);
```

---

# 6. String Builtins

String-related functionality includes:

```text
lower()
upper()
trim()
trimStart()
trimEnd()
startsWith()
endsWith()
includes()
repeat()
repeatStr()
replace()
split()
join()
substring()
padStart()
padEnd()
capitalize()
reverseStr()
camelCase()
kebabCase()
```

Example:

```pulsar
define text = "  Hello Pulsar  ";

define cleaned = trim(text);

show(upper(cleaned));
```

Output:

```text
HELLO PULSAR
```

---

# 7. Numbers

Numbers can be integers:

```pulsar
define count = 10;
```

or decimal numbers:

```pulsar
define price = 19.99;
```

Arithmetic:

```pulsar
define a = 10;
define b = 3;

show(a + b);
show(a - b);
show(a * b);
show(a / b);
show(a % b);
```

---

# 8. Math Builtins

Pulsar provides mathematical builtins including:

```text
floor()
ceil()
round()
abs()
pow()
sqrt()
min()
max()
random()
randomInt()
randomFloat()
clamp()
sign()
lerp()
degToRad()
radToDeg()
```

Examples:

```pulsar
show(abs(-10));
show(sqrt(25));
show(round(4.7));
show(floor(4.9));
show(ceil(4.1));
```

---

# 9. Booleans

Boolean values are:

```pulsar
true
false
```

Example:

```pulsar
define loggedIn = true;

if (loggedIn) {
    show("Welcome");
}
```

Boolean expressions:

```pulsar
define age = 20;

if (age >= 18) {
    show("Allowed");
}
```

---

# 10. Null

Pulsar uses:

```pulsar
null
```

Example:

```pulsar
define result = null;

if (result == null) {
    show("No result");
}
```

A function can also return `null`:

```pulsar
func findUser() {
    return null;
}
```

---

# 11. Arrays

Arrays use square brackets:

```pulsar
define numbers = [1, 2, 3, 4, 5];
```

Arrays can contain strings:

```pulsar
define names = [
    "Alex",
    "John",
    "Maya"
];
```

Mixed values:

```pulsar
define data = [
    "Pulsar",
    100,
    true,
    null
];
```

Arrays can contain objects:

```pulsar
define users = [
    {
        name: "Alex",
        age: 20
    },
    {
        name: "Maya",
        age: 21
    }
];
```

---

# 12. Array Access

Array elements can be accessed by index.

```pulsar
define numbers = [10, 20, 30];

show(numbers[0]);
show(numbers[1]);
show(numbers[2]);
```

When generating code, follow the indexing behavior implemented by the actual Pulsar interpreter rather than assuming another language's indexing convention.

---

# 13. Array Builtins

Array-related functionality includes:

```text
push()
pop()
shift()
unshift()
sort()
reverse()
unique()
indexOf()
includesArr()
flatten()
randomChoice()
count()
uniqueBy()
range()
```

Example:

```pulsar
define numbers = [1, 2, 3];

push(numbers, 4);

show(numbers);
```

---

# 14. Objects

Objects use key/value pairs.

```pulsar
define user = {
    name: "Alex",
    age: 20,
    active: true
};
```

Access properties:

```pulsar
show(user.name);
show(user.age);
show(user.active);
```

Nested objects:

```pulsar
define user = {
    profile: {
        name: "Alex",
        age: 20
    }
};

show(user.profile.name);
```

---

# 15. Object Builtins

Object-related functionality includes:

```text
hasOwn()
keys()
values()
entries()
invert()
isEmpty()
deepClone()
getProp()
setProp()
mergeDeep()
```

Example:

```pulsar
define user = {
    name: "Alex",
    age: 20
};

show(keys(user));
show(values(user));
```

---

# 16. Operators

Common operators include:

```text
+
-
*
/
%
==
!=
<
>
<=
>=
&&
||
!
```

Arithmetic:

```pulsar
define result = 10 + 5 * 2;
```

Comparison:

```pulsar
define age = 20;

show(age >= 18);
```

Logical operations:

```pulsar
define active = true;
define verified = true;

if (active && verified) {
    show("Accepted");
}
```

---

# 17. Expressions

An expression produces a value.

Examples:

```pulsar
10 + 20
```

```pulsar
name
```

```pulsar
user.name
```

```pulsar
price * quantity
```

```pulsar
calculateTotal()
```

Expressions can be combined:

```pulsar
define total =
    price * quantity - discount;
```

---

# 18. Conditional Statements

Basic `if`:

```pulsar
if (score >= 50) {
    show("Pass");
}
```

`if / else`:

```pulsar
if (score >= 50) {
    show("Pass");
} else {
    show("Fail");
}
```

Multiple branches:

```pulsar
if (score >= 80) {
    show("A");
} else if (score >= 60) {
    show("B");
} else {
    show("C");
}
```

---

# 19. Functions

Functions use the `func` keyword.

```pulsar
func add(a, b) {
    return a + b;
}
```

Call the function:

```pulsar
define result = add(10, 20);

show(result);
```

Function without parameters:

```pulsar
func greet() {
    show("Hello");
}

greet();
```

---

# 20. Function Parameters

Functions can accept parameters:

```pulsar
func greet(name) {
    show("Hello " + name);
}

greet("Alex");
```

Multiple parameters:

```pulsar
func multiply(a, b) {
    return a * b;
}

show(multiply(5, 4));
```

---

# 21. Return

`return` sends a value back to the caller.

```pulsar
func square(number) {
    return number * number;
}

define result = square(5);

show(result);
```

A function may return early:

```pulsar
func check(value) {
    if (value == null) {
        return "empty";
    }

    return "valid";
}
```

---

# 22. Arrow Functions

Arrow functions provide a compact function syntax.

```pulsar
define double = x => x * 2;

show(double(5));
```

Multiple parameters:

```pulsar
define add = (a, b) => a + b;

show(add(10, 20));
```

Block body:

```pulsar
define greet = name => {
    show("Hello " + name);
};
```

Arrow functions are especially useful as callbacks.

---

# 23. `map`

`map()` transforms array values.

```pulsar
define numbers = [1, 2, 3, 4];

define doubled = map(
    numbers,
    x => x * 2
);

show(doubled);
```

Conceptually:

```text
[1, 2, 3, 4]
       |
       v
multiply each value by 2
       |
       v
[2, 4, 6, 8]
```

---

# 24. `filter`

`filter()` selects values that satisfy a condition.

```pulsar
define numbers = [1, 2, 3, 4, 5];

define even = filter(
    numbers,
    x => x % 2 == 0
);

show(even);
```

Result:

```text
[2, 4]
```

---

# 25. `reduce`

`reduce()` combines values into one result.

```pulsar
define numbers = [1, 2, 3, 4];

define total = reduce(
    numbers,
    (a, b) => a + b,
    0
);

show(total);
```

Result:

```text
10
```

---

# 26. For Loops

A standard `for` loop contains initialization, condition, and update.

```pulsar
for (define i = 0; i < 5; i = i + 1) {
    show(i);
}
```

The loop produces:

```text
0
1
2
3
4
```

A more practical example:

```pulsar
for (
    define i = 0;
    i < 10;
    i = i + 1
) {
    show(i * 2);
}
```

---

# 27. For-In Loops

Pulsar supports:

```pulsar
for item in items {
    show(item);
}
```

Example:

```pulsar
define numbers = [10, 20, 30];

for number in numbers {
    show(number);
}
```

For arrays, the loop variable represents each array value.

Object iteration follows the evaluator's `ForInStatement` implementation.

Example:

```pulsar
define user = {
    name: "Alex",
    age: 20
};

for key in user {
    show(key);
}
```

The AI should not assume that the loop variable contains an object's value when the evaluator defines it as the key.

---

# 28. While Loops

```pulsar
define i = 0;

while (i < 5) {
    show(i);

    i = i + 1;
}
```

A `while` loop continues while its condition evaluates to a truthy value.

---

# 29. Break

`break` exits the current loop.

```pulsar
for (define i = 0; i < 10; i = i + 1) {
    if (i == 5) {
        break;
    }

    show(i);
}
```

The loop stops when `i` reaches `5`.

---

# 30. Continue

`continue` skips the rest of the current iteration.

```pulsar
for (define i = 0; i < 10; i = i + 1) {
    if (i % 2 == 0) {
        continue;
    }

    show(i);
}
```

This is useful for filtering work inside loops.

---

# 31. Scope

Pulsar uses environments to store and resolve variables.

A function has its own environment.

```pulsar
define name = "Global";

func test() {
    define name = "Local";

    show(name);
}

test();

show(name);
```

The local `name` and outer `name` are separate bindings according to the evaluator's environment model.

---

# 32. Environments

The evaluator uses environments to manage variable bindings.

Conceptually:

```text
Global Environment
        |
        v
Function Environment
        |
        v
Local Variables
```

Functions can evaluate code inside a new environment while still having access to values from their surrounding environment.

When debugging scope-related problems, inspect:

```text
Environment
define()
lookup()
assignment
function environment
parent environment
```

rather than assuming JavaScript lexical behavior.

---

# 33. Builtin `len`

`len()` obtains the length of supported values.

```pulsar
define name = "Pulsar";

show(len(name));
```

Array example:

```pulsar
define numbers = [10, 20, 30];

show(len(numbers));
```

---

# 34. Type Inspection

Pulsar provides:

```pulsar
type()
```

Example:

```pulsar
define value = 100;

show(type(value));
```

Another example:

```pulsar
define value = "hello";

show(type(value));
```

Use the runtime's actual type names when writing documentation or tests.

---

# 35. Conversion

String conversion:

```pulsar
define number = 100;

define text = toStr(number);

show(text);
```

The runtime also provides:

```pulsar
str()
```

and numeric conversion functionality such as:

```pulsar
num()
```

when supported by the evaluator.

---

# 36. Random Values

Random number generation:

```pulsar
define value = random();

show(value);
```

Integer range example:

```pulsar
define number = randomInt(1, 100);

show(number);
```

Random array selection:

```pulsar
define names = [
    "Alex",
    "Maya",
    "John"
];

define selected = randomChoice(names);

show(selected);
```

---

# 37. JSON Parsing

JSON text can be parsed:

```pulsar
define text = "{\"name\":\"Alex\",\"age\":20}";

define user = JSONParse(text);

show(user.name);
```

---

# 38. JSON Serialization

Objects can be converted into JSON:

```pulsar
define user = {
    name: "Alex",
    age: 20
};

define json = JSONStringify(user);

show(json);
```

---

# 39. JSON Files

If supported by the runtime:

```pulsar
define user = readJSON("user.json");

show(user.name);
```

Write JSON:

```pulsar
writeJSON(
    "user.json",
    {
        name: "Alex",
        age: 20
    }
);
```

---

# 40. File Operations

Read a file:

```pulsar
define content = readFile("data.txt");

show(content);
```

Write a file:

```pulsar
writeFile(
    "data.txt",
    "Hello from Pulsar"
);
```

Append:

```pulsar
appendFile(
    "data.txt",
    "\nAnother line"
);
```

Check existence:

```pulsar
if (exists("data.txt")) {
    show("File exists");
}
```

---

# 41. Directories

Directory-related operations can include:

```pulsar
mkdir("data");
```

and:

```pulsar
rmdir("data");
```

Only use operations actually registered by the current Pulsar runtime.

---

# 42. HTTP

Pulsar supports asynchronous HTTP-related functionality through its runtime builtins.

Example:

```pulsar
define response = await fetch(
    "https://example.com"
);

show(response);
```

A GET request may be represented by:

```pulsar
define result = await get(
    "https://example.com/api/data"
);

show(result);
```

POST:

```pulsar
define result = await post(
    "https://example.com/api/data",
    {
        name: "Alex"
    }
);

show(result);
```

The exact response structure depends on the builtin implementation.

---

# 43. Async and Await

Pulsar evaluation supports asynchronous operations.

For an asynchronous builtin:

```pulsar
define response = await fetch(
    "https://example.com"
);
```

For a delay:

```pulsar
await sleep(1000);
```

Do not treat asynchronous functions as ordinary synchronous values when the builtin returns a Promise.

---

# 44. Environment Variables

Environment variables can be read through the runtime.

```pulsar
define port = getEnv("PORT");

show(port);
```

A fallback can be used when supported:

```pulsar
define port = getEnv(
    "PORT",
    "3000"
);

show(port);
```

---

# 45. Common Program Pattern

A typical Pulsar program can combine variables, functions, arrays, objects, conditions, and loops.

```pulsar
define products = [
    {
        id: 1,
        name: "Laptop",
        price: 1200,
        stock: 5
    },
    {
        id: 2,
        name: "Keyboard",
        price: 80,
        stock: 10
    },
    {
        id: 3,
        name: "Mouse",
        price: 40,
        stock: 20
    }
];

func findProduct(id) {
    for product in products {
        if (product.id == id) {
            return product;
        }
    }

    return null;
}

define product = findProduct(1);

if (product != null) {
    show(product.name);
    show(product.price);
}
```

---

# 46. AI Code Generation Rules

When generating Pulsar code:

### Use `define`

```pulsar
define name = "Pulsar";
```

Not:

```text
let name = "Pulsar";
```

### Use `func`

```pulsar
func add(a, b) {
    return a + b;
}
```

### Use Pulsar's `for-in`

```pulsar
for item in items {
    show(item);
}
```

Not automatically:

```text
for (const item of items)
```

### Use Pulsar's syntax

Do not automatically insert:

```text
JavaScript classes
Python indentation
C declarations
JavaScript semicolons in unsupported positions
```

Use the grammar and evaluator as the authority.

---

# 47. AI Debugging Rules

When a Pulsar program fails, determine whether the problem belongs to:

```text
Source
  |
  v
Lexer
  |
  v
Parser
  |
  v
AST
  |
  v
Evaluator
  |
  v
Builtin/runtime
```

For example, an error reported around:

```pulsar
for product in products {
```

may be an evaluator problem involving `ForInStatement`, rather than invalid Pulsar syntax.

Similarly, an error involving:

```pulsar
map(...)
```

may come from builtin invocation or callback evaluation rather than the array itself.

---

# 48. Do Not Invent Language Features

An AI should not assume that Pulsar supports a feature merely because another language does.

Do not automatically introduce:

```text
class
extends
super
interface
generic
switch
try/catch
throw
import
export
```

unless the actual Pulsar parser, evaluator, and documentation establish that feature.

If a feature is not confirmed, state that it is not confirmed.

---

# 49. Do Not Invent Builtins

Only use documented or actually registered builtins.

For example, do not invent:

```pulsar
readDatabase()
sendEmail()
createServer()
```

unless those functions exist in the current runtime.

A function call should normally be one of:

```text
A user-defined Pulsar function
A documented Pulsar builtin
A supported runtime function
```

---

# 50. Translating Other Languages to Pulsar

When translating JavaScript:

```text
let name = "Alex";
```

becomes:

```pulsar
define name = "Alex";
```

JavaScript:

```text
function add(a, b) {
    return a + b;
}
```

becomes:

```pulsar
func add(a, b) {
    return a + b;
}
```

JavaScript:

```text
for (const item of items) {
    console.log(item);
}
```

becomes conceptually:

```pulsar
for item in items {
    show(item);
}
```

The translation should preserve meaning while using Pulsar syntax.

---

# 51. Testing Pulsar Code

Small programs are useful for testing individual language features.

### Variable test

```pulsar
define name = "Pulsar";

show(name);
```

### Function test

```pulsar
func add(a, b) {
    return a + b;
}

show(add(2, 3));
```

### Array test

```pulsar
define numbers = [1, 2, 3];

for number in numbers {
    show(number);
}
```

### Conditional test

```pulsar
define value = 10;

if (value > 5) {
    show("greater");
} else {
    show("smaller");
}
```

### While test

```pulsar
define i = 0;

while (i < 3) {
    show(i);
    i = i + 1;
}
```

---

# 52. AI Test Generation

When asked to create Pulsar tests, isolate one feature at a time.

For example:

```text
variables
strings
numbers
booleans
null
arrays
objects
operators
expressions
if/else
for
for-in
while
break
continue
functions
return
arrow functions
scope
builtins
JSON
files
HTTP
async
```

Then create progressively more complex tests.

A good test should make the expected behavior obvious:

```pulsar
define numbers = [1, 2, 3];

define result = map(
    numbers,
    x => x * 2
);

show(result);
```

Expected:

```text
[2, 4, 6]
```

---

# 53. AI Explanation Rules

When explaining Pulsar code, explain the actual Pulsar constructs.

For:

```pulsar
define numbers = [1, 2, 3];

for number in numbers {
    show(number);
}
```

explain:

1. `define` creates `numbers`.
2. `[1, 2, 3]` creates an array.
3. `for number in numbers` iterates through the array.
4. `number` receives each array value.
5. `show(number)` outputs the current value.

Do not explain the code as JavaScript or Python.

---

# 54. AI Modification Rules

When modifying an existing Pulsar program:

1. Preserve valid Pulsar syntax.
2. Preserve existing variable names unless there is a reason to change them.
3. Preserve existing function behavior unless requested otherwise.
4. Use existing builtins where possible.
5. Do not introduce unsupported syntax.
6. Keep `.pulsar` code executable by the current interpreter.
7. If an error appears to originate from the evaluator, distinguish runtime fixes from source-code fixes.

---

# 55. AI Runtime Debugging

For evaluator errors, inspect the AST node involved.

Important evaluator categories include:

```text
Variable declarations
Expressions
Functions
Calls
ForStatement
ForInStatement
WhileStatement
BreakSignal
ContinueSignal
ReturnValue
Array operations
Object operations
Builtin calls
NewExpression
```

For the core language covered by this document, the most important loop nodes are:

```text
ForStatement
ForInStatement
WhileStatement
```

---

# 56. `ForInStatement` Runtime Model

The evaluator handles a `ForInStatement` by evaluating its iterable first.

Conceptually:

```text
for item in iterable
        |
        v
evaluate iterable
        |
        v
verify iterable is an object
        |
        +---- Array
        |       |
        |       v
        |   iterate values
        |
        +---- Object
                |
                v
             iterate keys
```

For an array:

```pulsar
define items = ["A", "B", "C"];

for item in items {
    show(item);
}
```

the loop variable receives:

```text
A
B
C
```

For an object:

```pulsar
define user = {
    name: "Alex",
    age: 20
};

for key in user {
    show(key);
}
```

the evaluator's object branch iterates:

```text
name
age
```

according to the implementation.

---

# 57. Error Interpretation

When a Pulsar runtime reports:

```text
Error evaluating for loop
```

do not immediately rewrite the Pulsar loop.

First determine whether:

```text
The parser produced the wrong AST
```

or:

```text
The evaluator failed to execute the AST
```

or:

```text
The iterable has an invalid runtime value
```

This distinction is important when debugging the interpreter itself.

---

# 58. Language Authority

For AI-generated Pulsar code, use this priority:

```text
1. Pulsar parser
2. Pulsar evaluator
3. Registered Pulsar builtins
4. Pulsar language documentation
5. Existing working Pulsar examples
6. General programming-language knowledge
```

General programming knowledge should never silently override confirmed Pulsar behavior.

---

# 59. Minimal AI Prompt Context

An AI can use the following compact description when generating Pulsar:

```text
Pulsar is a programming language using .pulsar files.

Variables use:
define x = value;

Functions use:
func name(args) {
    ...
}

Functions return with:
return value;

Conditions use:
if (condition) {
    ...
} else {
    ...
}

Standard loops use:
for (define i = 0; i < n; i = i + 1) {
    ...
}

For-in loops use:
for item in items {
    ...
}

While loops use:
while (condition) {
    ...
}

Loop control:
break;
continue;

Arrow functions:
x => expression
(a, b) => expression

Core values:
strings, numbers, booleans, null, arrays, objects, functions.

Common functional builtins:
map(), filter(), reduce()

JSON:
JSONParse()
JSONStringify()

Common utility builtins:
len()
str()
toStr()
type()
random()

The AI must use actual Pulsar syntax and must not invent unsupported language features or builtins.
```

---

# 60. Final AI Principle

When generating Pulsar code, the goal is not to make the code *look like* another familiar programming language.

The goal is to produce code that is valid for the actual Pulsar lexer, parser, evaluator, runtime, and registered builtins.

Therefore:

```text
Pulsar syntax first.
Pulsar runtime behavior first.
Pulsar documentation first.
General language assumptions second.
```

If the implementation does not establish a feature, the AI should not present that feature as part of the Pulsar language.
