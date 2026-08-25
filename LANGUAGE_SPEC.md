## 1. Introduction

Pulsar is an interpreted programming language using the `.pulsar` file extension.

Pulsar is designed around a readable syntax and an interpreter architecture consisting of source parsing, evaluation, environments, runtime values, functions, control flow, built-ins, and application-oriented features.

A basic Pulsar program looks like this:

```pulsar
define name = "Pulsar";

show("Hello, " + name);
````

Pulsar programs are evaluated by the Pulsar interpreter rather than compiled directly to native machine code.

---

# 2. Source Files

Pulsar source files use:

```text
.pulsar
```

Example:

```text
hello.pulsar
```

A source file can contain declarations, expressions, functions, entities, control-flow statements, imports, and other supported language constructs.

---

# 3. Program Structure

A Pulsar program consists of statements evaluated in sequence.

```pulsar
define name = "Pulsar";

show(name);

define version = 1;

show(version);
```

The interpreter evaluates the program body sequentially. Runtime control signals such as `return`, `break`, and `continue` are propagated rather than treated as ordinary values.

---

# 4. Comments

Single-line comments are supported using the language's comment syntax.

Example:

```pulsar
// This is a comment

define name = "Pulsar";
```

Comments do not produce runtime values.

---

# 5. Variables

Pulsar uses `define` for variable declarations.

```pulsar
define name = "Pulsar";
define version = 1;
define active = true;
```

A declaration requires an initializer.

```pulsar
define value = 100;
```

A declaration without an initializer is invalid.

```pulsar
define value;
```

The interpreter validates variable declarations and reports a runtime error when an initializer is missing.

Variables are stored in an `Environment`.

The runtime environment provides:

* `define`
* `get`
* `set`
* `has`

Variable lookup first checks the current environment and then walks through parent environments.

---

# 6. Assignment

An existing variable can be assigned a new value.

```pulsar
define score = 10;

score = 20;

show(score);
```

Assignment can also target object properties.

```pulsar
define user = {
    name: "Alex"
};

user.name = "Pulsar";
```

The evaluator resolves the assignment target and updates the corresponding value.

---

# 7. Values

Pulsar programs can work with values including:

```pulsar
define text = "Pulsar";
define number = 100;
define decimal = 12.5;
define active = true;
define empty = null;

define numbers = [1, 2, 3];

define user = {
    name: "Alex"
};
```

The interpreter represents runtime values using JavaScript values and runtime objects.

---

# 8. Null

Pulsar supports `null`.

```pulsar
define value = null;

show(value);
```

`null` can be used to represent the absence of a value.

For example:

```pulsar
func findUser(id) {
    return null;
}
```

A function that does not explicitly produce a value is normalized to `null` by the current evaluator.

---

# 9. Strings

Strings are written using quotation marks.

```pulsar
define name = "Pulsar";
```

Strings can be combined with `+`.

```pulsar
define name = "Pulsar";

show("Hello " + name);
```

String values can be passed to functions:

```pulsar
func greet(name) {
    return "Hello " + name;
}

show(greet("Pulsar"));
```

---

# 10. Numbers

Pulsar supports numeric values.

```pulsar
define integer = 100;
define decimal = 12.5;
```

Arithmetic expressions can be evaluated directly:

```pulsar
show(10 + 5);
show(10 - 5);
show(10 * 5);
show(10 / 5);
show(10 % 3);
```

Parentheses can control evaluation order:

```pulsar
define result = (2 + 3) * 4;

show(result);
```

---

# 11. Booleans

Boolean values are:

```pulsar
true
false
```

Example:

```pulsar
define active = true;
define disabled = false;
```

Boolean expressions can be used in conditional statements:

```pulsar
define loggedIn = true;

if (loggedIn) {
    show("Welcome");
}
```

---

# 12. Arrays

Arrays are ordered collections.

```pulsar
define numbers = [10, 20, 30];

show(numbers[0]);
show(numbers[1]);
show(numbers[2]);
```

Arrays can contain different value types:

```pulsar
define values = [
    10,
    "Pulsar",
    true,
    null
];
```

Arrays can contain objects:

```pulsar
define products = [
    {
        id: 1,
        name: "Laptop",
        price: 1200
    },
    {
        id: 2,
        name: "Mouse",
        price: 40
    }
];
```

---

# 13. Objects

Objects contain named properties.

```pulsar
define user = {
    name: "Alex",
    age: 20,
    active: true
};
```

Properties can be accessed with dot notation:

```pulsar
show(user.name);
show(user.age);
```

Properties can be modified:

```pulsar
user.age = 21;
```

Objects can contain nested objects:

```pulsar
define user = {
    name: "Alex",
    address: {
        city: "Mandalay",
        country: "Myanmar"
    }
};

show(user.address.city);
```

---

# 14. Arithmetic Operators

Pulsar supports arithmetic expressions such as:

```pulsar
show(10 + 5);
show(10 - 5);
show(10 * 5);
show(10 / 5);
show(10 % 3);
```

Unary numeric expressions are also supported:

```pulsar
show(-25);
show(+25);
```

Operator precedence applies to expressions.

For example:

```pulsar
show(2 + 3 * 4);
```

is evaluated according to the language's expression precedence.

Parentheses can override precedence:

```pulsar
show((2 + 3) * 4);
```

---

# 15. Comparison Operators

Comparison expressions include:

```pulsar
10 == 10
10 != 20
5 < 10
5 <= 5
10 > 5
10 >= 10
```

Example:

```pulsar
define age = 20;

if (age >= 18) {
    show("Adult");
}
```

---

# 16. Logical Expressions

Logical expressions can be used to combine conditions.

```pulsar
define age = 20;
define active = true;

if (age >= 18 && active) {
    show("Allowed");
}
```

Alternative conditions can be expressed with logical OR:

```pulsar
if (age < 18 || active == false) {
    show("Not allowed");
}
```

Logical negation can be used where supported:

```pulsar
if (!active) {
    show("Inactive");
}
```

---

# 17. Conditional Statements

## If

```pulsar
if (score >= 50) {
    show("Pass");
}
```

## If / Else

```pulsar
if (score >= 50) {
    show("Pass");
} else {
    show("Fail");
}
```

## Else If

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

Conditional statements evaluate their condition and execute the appropriate block.

---

# 18. While Loops

A `while` loop repeatedly evaluates its condition.

```pulsar
define i = 1;

while (i <= 5) {
    show(i);
    i++;
}
```

The loop stops when the condition becomes false.

---

# 19. Standard For Loops

Pulsar supports standard `for` loops.

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

A standard loop consists conceptually of:

```text
initialization
condition
body
update
```

For example:

```pulsar
for (
    define i = 0;
    i < 10;
    i++
) {
    show(i);
}
```

The interpreter creates a local environment for the standard loop.

---

# 20. For-In Loops

Pulsar supports `for-in` iteration.

```pulsar
define numbers = [10, 20, 30];

for number in numbers {
    show(number);
}
```

For arrays, the loop variable receives each array value.

For objects, the loop variable receives each object key.

```pulsar
define user = {
    name: "Alex",
    age: 20
};

for key in user {
    show(key);
}
```

The evaluator checks that the value being iterated is an object.

Arrays are iterated by value.

Objects are iterated using their keys.

---

# 21. Break

`break` exits the current loop.

```pulsar
for (define i = 0; i < 10; i++) {
    if (i == 5) {
        break;
    }

    show(i);
}
```

The evaluator represents this operation internally using a control-flow signal.

---

# 22. Continue

`continue` skips the remainder of the current iteration.

```pulsar
for (define i = 0; i < 5; i++) {
    if (i == 2) {
        continue;
    }

    show(i);
}
```

For a standard `for` loop, the update expression is still evaluated when `continue` is encountered.

---

# 23. Functions

Functions are declared using `func`.

```pulsar
func greet() {
    show("Hello");
}

greet();
```

Functions can receive parameters:

```pulsar
func greet(name) {
    show("Hello " + name);
}

greet("Pulsar");
```

Functions can return values:

```pulsar
func add(a, b) {
    return a + b;
}

define result = add(10, 20);

show(result);
```

---

# 24. Return

`return` exits the current function.

```pulsar
func find(numbers, target) {
    for number in numbers {
        if (number == target) {
            return number;
        }
    }

    return null;
}
```

The interpreter represents function returns using a `ReturnValue` control signal.

A return signal is propagated through blocks and loops until it reaches the function call evaluator.

This allows code such as:

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

to return directly from the function even though the `return` occurs inside the loop.

---

# 25. Function Scope

A function call creates a child environment.

```pulsar
define globalName = "Pulsar";

func greet(name) {
    define message = "Hello " + name;

    return message;
}

show(greet("Alex"));
```

The function receives its own local environment.

Function parameters are defined inside that environment.

The environment also maintains a link to the environment in which the function was created.

---

# 26. Closures

Functions can retain access to the environment in which they were created.

Conceptually:

```pulsar
func makeCounter() {
    define count = 0;

    return () => {
        count++;
        return count;
    };
}

define counter = makeCounter();

show(counter());
show(counter());
show(counter());
```

The exact behavior of a particular closure example depends on the parser and evaluator implementation used by the current Pulsar interpreter.

---

# 27. Arrow Functions

Pulsar supports arrow functions.

```pulsar
define add = (a, b) => {
    return a + b;
};

show(add(10, 20));
```

An arrow function can also contain an expression body where supported:

```pulsar
define double = value => value * 2;
```

Arrow functions create a local environment for their parameters.

---

# 28. Function Expressions

Functions can be represented as values and assigned to variables.

```pulsar
define add = func(a, b) {
    return a + b;
};

show(add(10, 20));
```

A function value can be passed to another function.

---

# 29. Built-in Functions

Pulsar provides built-in runtime functions.

Examples include:

```pulsar
show("Hello");

define value = ask("Enter a value: ");

define number = num(value);

show(str(number));
```

Other built-ins provide functionality for strings, arrays, objects, JSON, mathematics, files, random values, and other runtime operations.

The complete list belongs in `BUILTINS.md`.

---

# 30. Type Inspection

Values can be inspected using the available type functionality.

```pulsar
show(type("Pulsar"));
show(type(100));
show(type(true));
show(type([1, 2, 3]));
```

---

# 31. Strings and String Operations

Pulsar provides string-related operations through built-ins.

Examples include:

```pulsar
define text = "Pulsar Language";

show(len(text));
show(lower(text));
show(upper(text));
show(trim(text));
```

String operations should be documented individually in `STRING_BUILTINS.md`.

---

# 32. Array Operations

Pulsar supports operations over arrays, including higher-order operations such as map, filter, and reduce where provided by the runtime.

Example:

```pulsar
define numbers = [1, 2, 3, 4];

define doubled = map(
    numbers,
    (value) => value * 2
);

show(doubled);
```

Filtering:

```pulsar
define numbers = [1, 2, 3, 4, 5];

define even = filter(
    numbers,
    (value) => value % 2 == 0
);

show(even);
```

Reduction:

```pulsar
define numbers = [1, 2, 3, 4];

define total = reduce(
    numbers,
    (sum, value) => sum + value,
    0
);

show(total);
```

---

# 33. JSON

Pulsar supports JSON conversion and parsing.

Example:

```pulsar
define text = "{\"name\":\"Pulsar\",\"version\":1}";

define data = JSONParse(text);

show(data.name);
show(data.version);
```

Structured Pulsar values can be converted back to JSON using the corresponding JSON functionality.

JSON is particularly useful when communicating with web applications and HTTP APIs.

---

# 34. Error Handling

Pulsar provides runtime error handling using `do` and `track`.

```pulsar
do {
    define value = missingVariable;

    show(value);
} track {
    show("An error occurred");
}
```

The error can be accessed through the error value:

```pulsar
do {
    define value = missingVariable;
} track {
    show(error);
}
```

The interpreter uses `RuntimeError` for runtime failures and preserves known control-flow signals separately.

---

# 35. Runtime Errors

A runtime error contains information about the failure, including the associated AST node and source information.

For example, accessing an undefined variable produces an error similar to:

```text
Undefined variable: "name"
```

The runtime environment checks the current scope and its parents before reporting an undefined variable.

---

# 36. Environments

The Pulsar evaluator uses an `Environment` abstraction.

Conceptually:

```text
Environment
├── local variables
└── parent environment
```

An environment provides:

```text
define(name, value)
get(name)
set(name, value)
has(name)
```

`define` creates a binding in the current environment.

`get` searches the current environment and then parent environments.

`set` updates an existing binding when it exists in the current environment or one of its parents.

This environment chain provides lexical scope behavior for functions and nested evaluation.

---

# 37. Entities

Pulsar supports entity declarations.

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

An instance can be created with `new`:

```pulsar
define user = new User("Alex");

show(user.getName());
```

Entities provide a structured way to group state and methods.

---

# 38. `self`

Inside an entity method, `self` refers to the current instance.

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

When an entity instance is created, the evaluator creates the instance and binds `self` in the entity method environment.

---

# 39. Entity Initialization

An entity can define an `init` method.

```pulsar
entity User {
    init(name) {
        self.name = name;
    }
}
```

When:

```pulsar
define user = new User("Alex");
```

is evaluated, the evaluator creates an instance and invokes the entity's `init` method when present.

---

# 40. Inheritance

Entities can inherit from another entity.

```pulsar
entity User {
    init(name) {
        self.name = name;
    }

    getName() {
        return self.name;
    }
}

entity Admin inherits User {
    isAdmin() {
        return true;
    }
}
```

An inherited entity can use functionality from its parent.

```pulsar
define admin = new Admin("Alex");

show(admin.name);
show(admin.getName());
show(admin.isAdmin());
```

The evaluator validates that the parent is a valid entity.

---

# 41. Base Methods

Inherited entities can access parent methods through `base`.

The runtime creates a base-method proxy when an entity has a parent.

Conceptually:

```pulsar
entity User {
    getRole() {
        return "User";
    }
}

entity Admin inherits User {
    getRole() {
        return base.getRole();
    }
}
```

The exact available base syntax should follow the parser and evaluator version shipped with Pulsar.

---

# 42. Object Construction

The `new` expression creates entity instances.

```pulsar
define user = new User("Alex");
```

The evaluator:

1. Evaluates the constructor target.
2. Evaluates constructor arguments.
3. Creates the instance.
4. Creates an entity environment.
5. Defines `self`.
6. Defines `base` when inheritance exists.
7. Executes `init` when available.
8. Installs the entity methods.
9. Returns the instance.

---

# 43. Imports

Pulsar supports imports.

The evaluator can resolve imported modules and bind imported values into the current environment.

Conceptually:

```pulsar
import something from "./module.pulsar";
```

Named imports and namespace/default-style imports are represented by the interpreter's import evaluator.

The exact module resolution rules should be documented alongside the CLI and runtime module system.

---

# 44. Server Programming

Pulsar includes a built-in HTTP server.

A minimal server is:

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return "Hello from Pulsar";
});

app.listen(3000);
```

The server supports route registration, request parsing, responses, middleware, static files, templates, sessions, cookies, and HTTP-related functionality.

---

# 45. Static Files

A server can expose a directory containing completed static files.

```pulsar
define app = createServer({
    staticDir: "./public"
});

app.listen(3000);
```

For example:

```text
project/
├── server.pulsar
└── public/
    └── index.html
```

Static HTML is served directly when no server-side data injection is required.

---

# 46. Templates

Pulsar's built-in server supports HTML templates.

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("index.html", {
        title: "Pulsar",
        message: "Hello from Pulsar"
    });
});

app.listen(3000);
```

Template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{title}}</title>
</head>
<body>
    <h1>{{title}}</h1>
    <p>{{message}}</p>
</body>
</html>
```

The current renderer supports simple substitutions such as `{{name}}` and nested values such as `{{user.name}}`.

---

# 47. HTML Data Injection

Server-side Pulsar values can be supplied to templates.

```pulsar
return res.render("profile.html", {
    user: {
        name: "Alex",
        role: "Developer"
    }
});
```

HTML:

```html
<h1>{{user.name}}</h1>
<p>{{user.role}}</p>
```

The template renderer resolves the supplied data when generating the response.

---

# 48. HTML Data Retrieval

HTML forms can submit data to Pulsar routes.

```html
<form method="POST" action="/submit">
    <input name="name">
    <input name="email">

    <button type="submit">
        Submit
    </button>
</form>
```

The Pulsar route can access submitted values through `req.body`:

```pulsar
app.post("/submit", (req, res) => {
    return {
        name: req.body.name,
        email: req.body.email
    };
});
```

The current built-in server parses URL-encoded form bodies into `req.body`.

---

# 49. Route Parameters

Routes can contain parameters.

```pulsar
app.get("/users/:id", (req, res) => {
    return {
        id: req.params.id
    };
});
```

A request such as:

```text
/users/123
```

provides:

```pulsar
req.params.id
```

with the corresponding path value.

---

# 50. Query Parameters

Query parameters are available through `req.query`.

```pulsar
app.get("/search", (req, res) => {
    return {
        query: req.query.q,
        page: req.query.page
    };
});
```

A request such as:

```text
/search?q=laptop&page=2
```

provides the query values to the route.

---

# 51. Request Object

The built-in server exposes request information through the request object.

The current implementation includes request properties such as:

```text
req.path
req.method
req.params
req.query
req.body
req.files
req.cookies
req.session
req.headers
```

Applications can use these values to process incoming HTTP requests.

---

# 52. Response Object

Routes receive:

```pulsar
(req, res)
```

The response object supports response operations including:

```pulsar
res.send(...)
res.json(...)
res.render(...)
res.status(...)
```

A route can also return a value directly:

```pulsar
app.get("/", (req, res) => {
    return "Hello";
});
```

Returning an object can produce a JSON response.

---

# 53. JSON APIs

Pulsar can be used to create JSON APIs.

```pulsar
define app = createServer();

app.get("/api/status", (req, res) => {
    return {
        ok: true,
        status: "running"
    };
});

app.listen(3000);
```

A POST API can receive request data:

```pulsar
app.post("/api/profile", (req, res) => {
    return res.status(201).json({
        saved: true,
        profile: req.body
    });
});
```

---

# 54. Sessions

The request object exposes session data through:

```pulsar
req.session
```

Example:

```pulsar
app.get("/", (req, res) => {
    if (req.session.visits == null) {
        req.session.visits = 0;
    }

    req.session.visits++;

    return {
        visits: req.session.visits
    };
});
```

The current built-in server keeps session data in memory.

---

# 55. Cookies

Cookie information is available through the request object.

```pulsar
app.get("/", (req, res) => {
    show(req.cookies);

    return "OK";
});
```

Cookie-related response functionality belongs to the server API reference.

---

# 56. Middleware

Pulsar's built-in server supports middleware.

Middleware can inspect or modify a request before the route handler executes.

The exact middleware API should be documented in `MIDDLEWARE.md` according to the installed interpreter version.

---

# 57. Server + HTML Data Flow

A complete server-side HTML application can follow this flow:

```text
Pulsar application
        |
        v
HTTP route
        |
        v
res.render()
        |
        v
HTML template
        |
        v
Browser
```

Data can travel in the opposite direction through forms or HTTP requests:

```text
Browser
   |
   v
HTML form / HTTP request
   |
   v
Pulsar route
   |
   v
req.body / req.query / req.params
```

This allows Pulsar to combine application logic, HTTP routing, server-side rendering, and browser interaction.

---

# 58. Interpreter Architecture

The Pulsar interpreter is organized conceptually around:

```text
Source Code
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
     +---- Environment
     |
     +---- Functions
     |
     +---- Entities
     |
     +---- Built-ins
     |
     +---- Runtime
     |
     v
Program Result
```

The evaluator receives an AST and evaluates its nodes against an environment.

---

# 59. Evaluation

The evaluator dispatches based on AST node type.

Different nodes correspond to different language constructs, including:

```text
Program
Block
Variable Declaration
Assignment
Function
Function Call
Arrow Function
If
While
For
For-In
Return
Break
Continue
Entity
New Expression
Import
Expressions
```

Unknown AST node types produce runtime errors.

---

# 60. Function Evaluation

A user-defined function stores its body, parameters, and defining environment.

When called:

```pulsar
define result = add(10, 20);
```

the evaluator:

1. Creates a new environment.
2. Uses the function's defining environment as its parent.
3. Defines the parameters.
4. Evaluates the function body.
5. Handles `ReturnValue`.
6. Produces the function result.

The current evaluator normalizes an undefined function result to `null`.

---

# 61. Control-Flow Signals

Pulsar uses internal control-flow signals for:

```text
ReturnValue
BreakSignal
ContinueSignal
```

These signals allow control flow to travel through nested evaluator functions without being confused with ordinary runtime values.

For example:

```pulsar
func find(numbers, target) {
    for number in numbers {
        if (number == target) {
            return number;
        }
    }

    return null;
}
```

The `ReturnValue` generated by the `return` statement must reach the function evaluator rather than being converted into an ordinary loop result.

---

# 62. Environment Chain

Environments form a parent chain.

```text
Global Environment
       |
       v
Function Environment
       |
       v
Nested Environment
```

A variable lookup starts at the current environment.

If the variable does not exist there, the lookup continues through the parent.

This allows nested functions and runtime scopes to access values from surrounding environments.

---

# 63. Runtime Error Model

Runtime failures are represented by `RuntimeError`.

Examples include:

```text
Undefined variable
Invalid operation
Cannot iterate over non-iterable
Value is not callable
Invalid parent entity
Invalid function expression
```

The evaluator preserves known control-flow signals separately from runtime errors.

This distinction is important because:

```text
return
break
continue
```

are normal language control-flow operations, while:

```text
RuntimeError
```

represents a program failure.

---

# 64. Language Design Principle

Pulsar syntax is intended to remain readable while providing enough runtime functionality for complete programs.

A simple program can be:

```pulsar
show("Hello, Pulsar!");
```

A data-processing program can use:

```pulsar
define numbers = [1, 2, 3, 4];

for number in numbers {
    show(number * 2);
}
```

A larger program can combine:

```text
Variables
Functions
Objects
Arrays
Loops
Entities
JSON
Files
HTTP
HTML
Templates
APIs
```

---

# 65. Complete Example

The following combines variables, arrays, objects, functions, loops, conditions, and return values:

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

define product = findProduct(2);

if (product != null) {
    show(product.name);
    show(product.price);
}
```

This example demonstrates an important interpreter behavior: a `return` inside a `for-in` loop exits the enclosing function.

---

# 66. Complete Server Example

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

define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("index.html", {
        title: "Pulsar Shop",
        products: products
    });
});

app.get("/api/products", (req, res) => {
    return products;
});

app.get("/api/products/:id", (req, res) => {
    define id = num(req.params.id);

    for product in products {
        if (product.id == id) {
            return product;
        }
    }

    return {
        error: "Product not found"
    };
});

app.listen(3000);
```

---

# 67. Specification Status

This document describes the behavior represented by the current Pulsar interpreter and its supplied examples.

The language specification should evolve together with:

```text
Interpreter
Parser
Lexer
Runtime
Tests
Examples
Server
Built-ins
```

When a language feature changes, its:

1. implementation,
2. tests,
3. examples,
4. reference documentation

should be updated together.

The executable interpreter and its regression tests remain the practical authority for behavior that has not yet been formally specified here.
