## 1. Overview

Pulsar source files use the `.pulsar` extension.

A Pulsar program is composed of statements and expressions. The parser recognizes declarations, expressions, blocks, functions, entities, control-flow statements, imports, and other language constructs.

A minimal program is:

```pulsar
show("Hello, Pulsar!");
```

Pulsar uses braces `{ }` for blocks and semicolons `;` to terminate statements where applicable. The parser also accepts omitted semicolons in several statement positions. 

---

## 2. Identifiers

Identifiers are names used for variables, functions, entities, parameters, and other user-defined values.

Examples:

```pulsar
name
age
totalPrice
findProduct
User
```

Variable declaration:

```pulsar
define name = "Pulsar";
```

Function declaration:

```pulsar
func greet(name) {
    return "Hello " + name;
}
```

Entity declaration:

```pulsar
entity User {
}
```

The parser requires an identifier after `define`. 

---

## 3. Variable Declaration

Pulsar uses `define`.

```pulsar
define name = "Pulsar";
define age = 20;
define active = true;
```

The general form is:

```text
define identifier = expression;
```

Example:

```pulsar
define total = 100 + 50;
```

The parser produces a `VarDeclaration` node containing the variable identifier and initializer expression. 

A declaration may also omit the initializer according to the parser grammar:

```pulsar
define value;
```

However, an assignment operator must not be confused with equality.

Correct:

```pulsar
define value = 10;
```

Incorrect:

```pulsar
define value == 10;
```

The parser explicitly rejects `==` in a variable declaration. 

---

## 4. Assignment

After a variable has been declared, it can be assigned a new value.

```pulsar
define score = 10;

score = 20;
```

Assignment uses:

```text
=
```

Equality comparison uses:

```text
==
```

Therefore:

```pulsar
score = 20;
```

means assignment, while:

```pulsar
score == 20
```

means comparison.

---

## 5. Statements

A Pulsar program contains statements such as:

```pulsar
define name = "Pulsar";

show(name);

if (name == "Pulsar") {
    show("Matched");
}
```

Common statement forms include:

```text
Variable declaration
Function declaration
Entity declaration
Assignment
Expression statement
If statement
While statement
For statement
For-in statement
Return statement
Break statement
Continue statement
Import statement
Deploy statement
Block statement
```

---

## 6. Semicolons

Statements commonly end with `;`.

```pulsar
define name = "Pulsar";
show(name);
```

The parser consumes an optional semicolon after several statement types.

For example, variable declarations explicitly accept a semicolon after the initializer. 

Use semicolons consistently in normal source code:

```pulsar
define x = 10;
define y = 20;

show(x + y);
```

---

## 7. Blocks

Blocks are enclosed by `{` and `}`.

```pulsar
{
    define x = 10;
    show(x);
}
```

Blocks are used by control-flow statements:

```pulsar
if (condition) {
    show("true");
}
```

and functions:

```pulsar
func greet() {
    show("Hello");
}
```

---

## 8. Expressions

Expressions produce values.

Examples:

```pulsar
10
"Hello"
true
null
10 + 20
name
user.name
numbers[0]
add(10, 20)
```

Expressions can be combined:

```pulsar
define total = price * quantity + shipping;
```

Parentheses can group expressions:

```pulsar
define total = (price + shipping) * quantity;
```

---

## 9. Literals

Pulsar supports literal values such as:

```pulsar
100
12.5
"Hello"
true
false
null
```

Arrays:

```pulsar
[1, 2, 3]
```

Objects:

```pulsar
{
    name: "Pulsar",
    version: 1
}
```

---

## 10. Strings

Strings are written using quotation marks.

```pulsar
define name = "Pulsar";
```

Strings can participate in expressions:

```pulsar
define message = "Hello " + name;

show(message);
```

---

## 11. Numbers

Numeric literals can be used directly:

```pulsar
define integer = 100;
define decimal = 12.5;
```

Arithmetic expressions:

```pulsar
define result = 10 + 20;
define difference = 20 - 5;
define product = 5 * 4;
define quotient = 20 / 4;
define remainder = 17 % 5;
```

---

## 12. Boolean Values

Boolean literals are:

```pulsar
true
false
```

Example:

```pulsar
define active = true;

if (active) {
    show("Active");
}
```

---

## 13. Null

The null literal is:

```pulsar
null
```

Example:

```pulsar
define result = null;
```

It is commonly used when a value does not exist:

```pulsar
func findUser(id) {
    return null;
}
```

---

## 14. Arrays

Arrays use square brackets.

```pulsar
define numbers = [1, 2, 3, 4];
```

Array elements can be expressions:

```pulsar
define x = 10;

define values = [
    x,
    x + 10,
    x + 20
];
```

Arrays can contain objects:

```pulsar
define products = [
    {
        id: 1,
        name: "Laptop"
    },
    {
        id: 2,
        name: "Keyboard"
    }
];
```

Array indexing:

```pulsar
show(numbers[0]);
```

---

## 15. Objects

Objects use curly braces containing property definitions.

```pulsar
define user = {
    name: "Alex",
    age: 20,
    active: true
};
```

Properties can contain expressions:

```pulsar
define price = 100;

define product = {
    name: "Keyboard",
    price: price,
    total: price * 2
};
```

---

## 16. Object Property Access

Dot notation accesses object properties.

```pulsar
define user = {
    name: "Alex",
    age: 20
};

show(user.name);
show(user.age);
```

Nested access is also used:

```pulsar
define user = {
    profile: {
        name: "Alex"
    }
};

show(user.profile.name);
```

The same nested-property style is used by the server's HTML template renderer. 

---

## 17. Property Assignment

Object properties can be assigned new values.

```pulsar
define user = {
    name: "Alex",
    age: 20
};

user.age = 21;
```

Nested properties can also be targeted:

```pulsar
user.profile.name = "Pulsar";
```

---

## 18. Operators

Arithmetic operators include:

```text
+
-
*
/
%
```

Comparison operators include:

```text
==
!=
<
<=
>
>=
```

Logical operators include:

```text
&&
||
!
```

Assignment uses:

```text
=
```

Examples:

```pulsar
define total = price * quantity;

if (total >= 100) {
    show("Large order");
}

if (active && verified) {
    show("Allowed");
}
```

---

## 19. Operator Precedence

Expressions can contain multiple operators.

```pulsar
define result = 2 + 3 * 4;
```

Parentheses can explicitly control grouping:

```pulsar
define result = (2 + 3) * 4;
```

The supplied examples use normal arithmetic precedence in this manner. 

---

## 20. If Statements

Basic syntax:

```pulsar
if (condition) {
    statements
}
```

Example:

```pulsar
if (age >= 18) {
    show("Allowed");
}
```

---

## 21. If / Else

```pulsar
if (condition) {
    statements
} else {
    statements
}
```

Example:

```pulsar
if (score >= 50) {
    show("Pass");
} else {
    show("Fail");
}
```

---

## 22. Else If

Multiple conditions can be chained:

```pulsar
if (score >= 90) {
    show("Excellent");
} else if (score >= 70) {
    show("Good");
} else if (score >= 50) {
    show("Pass");
} else {
    show("Fail");
}
```

---

## 23. While Loops

The basic form is:

```pulsar
while (condition) {
    statements
}
```

Example:

```pulsar
define i = 0;

while (i < 5) {
    show(i);
    i++;
}
```

---

## 24. Standard For Loops

The standard form is:

```pulsar
for (initialization; condition; update) {
    statements
}
```

Example:

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

The three components represent:

```text
initialization
condition
update
```

---

## 25. For-In Loops

Pulsar supports:

```pulsar
for item in collection {
    statements
}
```

Example:

```pulsar
define numbers = [10, 20, 30];

for number in numbers {
    show(number);
}
```

For arrays, the loop variable receives each array value.

For objects:

```pulsar
define user = {
    name: "Alex",
    age: 20
};

for key in user {
    show(key);
}
```

the loop iterates over object keys.

---

## 26. Break

`break` terminates the current loop.

```pulsar
for (define i = 0; i < 10; i++) {
    if (i == 5) {
        break;
    }

    show(i);
}
```

---

## 27. Continue

`continue` skips the remainder of the current iteration.

```pulsar
for (define i = 0; i < 10; i++) {
    if (i == 5) {
        continue;
    }

    show(i);
}
```

---

## 28. Functions

Functions use `func`.

```pulsar
func greet() {
    show("Hello");
}
```

Call the function:

```pulsar
greet();
```

---

## 29. Function Parameters

Parameters are declared inside parentheses.

```pulsar
func greet(name) {
    show("Hello " + name);
}
```

Multiple parameters:

```pulsar
func add(a, b) {
    return a + b;
}
```

Call:

```pulsar
show(add(10, 20));
```

---

## 30. Return

A function can return a value:

```pulsar
func add(a, b) {
    return a + b;
}
```

A return statement can occur inside nested control flow:

```pulsar
func findProduct(id) {
    for product in products {
        if (product.id == id) {
            return product;
        }
    }

    return null;
}
```

---

## 31. Arrow Functions

Arrow functions use `=>`.

Block form:

```pulsar
define add = (a, b) => {
    return a + b;
};
```

Single-parameter form:

```pulsar
define double = value => value * 2;
```

Arrow functions are also used extensively by the built-in server:

```pulsar
app.get("/", (req, res) => {
    return "Hello from Pulsar";
});
```

The supplied server examples use this syntax for route handlers. 

---

## 32. Function Calls

A function call consists of a function expression followed by arguments in parentheses.

```pulsar
greet();
```

With arguments:

```pulsar
add(10, 20);
```

Nested calls:

```pulsar
show(str(num("123")));
```

---

## 33. Nested Function Calls

Function calls can be used inside expressions:

```pulsar
define result = add(
    multiply(2, 3),
    10
);
```

They can also be passed as arguments where the corresponding function accepts callable values.

---

## 34. Entity Declarations

Entity syntax is:

```pulsar
entity EntityName {
    method() {
        statements
    }
}
```

Example:

```pulsar
entity User {
    init(name) {
        self.name = name;
    }

    getName() {
        return self.name;
    }
}
```

The parser expects an entity name followed by an optional inheritance clause and a body of method definitions. 

---

## 35. Entity Methods

Methods are declared without the `func` keyword:

```pulsar
entity User {
    greet() {
        return "Hello";
    }
}
```

Methods can have parameters:

```pulsar
entity Calculator {
    add(a, b) {
        return a + b;
    }
}
```

The parser represents these as `MethodDefinition` nodes. 

---

## 36. Entity Initialization

The special method `init` is used for initialization:

```pulsar
entity User {
    init(name) {
        self.name = name;
    }
}
```

The parser treats `init` as the entity's initialization method. 

---

## 37. Creating Entity Instances

Instances are created with `new`:

```pulsar
define user = new User("Alex");
```

Methods can then be called:

```pulsar
show(user.getName());
```

---

## 38. `self`

Inside entity methods, `self` refers to the current entity instance.

```pulsar
entity User {
    init(name) {
        self.name = name;
    }

    getName() {
        return self.name;
    }
}
```

---

## 39. Entity Inheritance

An entity can inherit from another entity:

```pulsar
entity User {
    init(name) {
        self.name = name;
    }
}

entity Admin inherits User {
    isAdmin() {
        return true;
    }
}
```

The parser recognizes:

```text
inherits
```

followed by a parent entity identifier. 

Create the child entity:

```pulsar
define admin = new Admin("Alex");

show(admin.name);
show(admin.isAdmin());
```

This pattern is also present in the supplied interpreter examples. 

---

## 40. Import Syntax

Pulsar supports import syntax for loading other source functionality.

The exact import forms should follow the parser/runtime version used by the project.

Where imports are used, keep module paths and imported names explicit.

---

## 41. Deploy Syntax

The parser also contains deploy-related syntax.

A declaration can be deployed:

```pulsar
sldeploy func greet() {
    return "Hello";
}
```

A deploy list can use:

```pulsar
sldeploy {
    greet,
    add
}
```

The parser represents these as `DeployStatement` and `DeployNamedStatement` nodes. 

Because deployment behavior is runtime-specific, complete deployment semantics belong in the deployment/CLI documentation rather than this syntax reference.

---

## 42. Error Tracking Syntax

Pulsar supports:

```pulsar
do {
    statements
} track {
    statements
}
```

Example:

```pulsar
do {
    define value = missingVariable;
    show(value);
} track {
    show("Runtime error handled");
}
```

The supplied examples use `do` and `track` for runtime-error handling. 

---

## 43. Server Route Syntax

The built-in server uses normal Pulsar function and arrow-function syntax.

Example:

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return "Hello from Pulsar";
});

app.listen(3000);
```

POST routes use the same form:

```pulsar
app.post("/submit", (req, res) => {
    return {
        name: req.body.name
    };
});
```

These forms are demonstrated by the supplied server documentation.  

---

## 44. HTML Template Syntax

When using the built-in server's template renderer, HTML can contain:

```html
{{name}}
```

For nested values:

```html
{{user.name}}
```

Example:

```html
<h1>{{user.name}}</h1>
<p>{{user.role}}</p>
```

The server documentation specifies these forms for template data injection. 

---

## 45. HTML Data Retrieval

HTML forms send data to Pulsar routes:

```html
<form method="POST" action="/submit">
    <input name="name">
    <input name="email">

    <button type="submit">
        Submit
    </button>
</form>
```

The corresponding Pulsar route accesses the submitted values through:

```pulsar
app.post("/submit", (req, res) => {
    return {
        name: req.body.name,
        email: req.body.email
    };
});
```

The supplied server implementation parses URL-encoded form bodies into `req.body`. 

---

## 46. JSON From HTML

Browser JavaScript can send JSON to a Pulsar route:

```javascript
fetch("/api/users", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        name: "Pulsar",
        age: 20
    })
});
```

Pulsar receives the parsed data through:

```pulsar
app.post("/api/users", (req, res) => {
    return {
        received: req.body
    };
});
```

The supplied server implementation parses JSON request bodies and exposes the result as `req.body`. 

---

## 47. HTML Retrieving Pulsar Data

A static HTML page can request JSON from a Pulsar API:

```javascript
const response = await fetch("/api/message");
const data = await response.json();
```

The corresponding route can return an object:

```pulsar
app.get("/api/message", (req, res) => {
    return {
        message: "Data from Pulsar",
        version: "1.0"
    };
});
```

This is the documented HTML-to-Pulsar data retrieval pattern. 

---

## 48. Complete Syntax Example

The following combines the primary language constructs:

```pulsar
define products = [
    {
        id: 1,
        name: "Laptop",
        price: 1200
    },
    {
        id: 2,
        name: "Keyboard",
        price: 80
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

func calculateTotal(product, quantity) {
    return product.price * quantity;
}

define product = findProduct(1);

if (product != null) {
    define total = calculateTotal(product, 2);

    show(product.name);
    show(total);
} else {
    show("Product not found");
}
```

---

## 49. Syntax Summary

| Construct         | Syntax                                  |
| ----------------- | --------------------------------------- |
| Variable          | `define name = value;`                  |
| Assignment        | `name = value;`                         |
| Function          | `func name(params) { ... }`             |
| Arrow function    | `(params) => { ... }`                   |
| Return            | `return value;`                         |
| If                | `if (condition) { ... }`                |
| Else              | `else { ... }`                          |
| While             | `while (condition) { ... }`             |
| For               | `for (init; condition; update) { ... }` |
| For-in            | `for item in collection { ... }`        |
| Break             | `break;`                                |
| Continue          | `continue;`                             |
| Entity            | `entity Name { ... }`                   |
| Inheritance       | `entity Child inherits Parent { ... }`  |
| Constructor       | `init(params) { ... }`                  |
| Instance          | `new Entity(args)`                      |
| Instance property | `self.name`                             |
| Object            | `{ key: value }`                        |
| Array             | `[value1, value2]`                      |
| Property access   | `object.property`                       |
| Index access      | `array[index]`                          |
| Error tracking    | `do { ... } track { ... }`              |
| Server route      | `app.get(path, handler)`                |
| POST route        | `app.post(path, handler)`               |

---

## 50. Syntax Design

Pulsar's syntax is centered around a small set of readable constructs:

```text
define
func
if
else
while
for
in
return
break
continue
entity
inherits
init
self
new
do
track
```

These constructs combine with expressions, arrays, objects, functions, and runtime built-ins to form complete `.pulsar` programs.