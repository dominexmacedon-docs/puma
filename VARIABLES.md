## 1. Overview

Variables in Pulsar are named bindings that allow a program to store and work with values.

Pulsar uses the `define` keyword to declare variables.

```pulsar
define name = "Pulsar";
define age = 20;
define active = true;
```

A variable can contain a primitive value, array, object, function, entity instance, or another runtime value.

---

## 2. Basic Variable Declaration

The basic syntax is:

```pulsar
define identifier = expression;
```

Example:

```pulsar
define name = "Pulsar";
```

The expression on the right side is evaluated and its result becomes the variable's value.

```pulsar
define x = 10;
define y = 20;

define total = x + y;

show(total);
```

Output:

```text
30
```

---

## 3. `define`

`define` is the primary variable-declaration keyword.

```pulsar
define username = "Alex";
define score = 100;
define loggedIn = true;
```

The parser recognizes `define` as a variable declaration and creates a variable-declaration AST node containing the variable name and initializer. 

---

## 4. Variable Names

Variables use identifiers.

Examples:

```pulsar
define name = "Pulsar";
define age = 20;
define totalPrice = 100;
define userName = "Alex";
define productCount = 5;
```

Descriptive names are preferable:

```pulsar
define price = 1200;
define quantity = 2;

define total = price * quantity;
```

---

## 5. Variables Can Store Different Values

A variable can hold a string:

```pulsar
define language = "Pulsar";
```

A number:

```pulsar
define version = 1;
```

A boolean:

```pulsar
define active = true;
```

`null`:

```pulsar
define result = null;
```

An array:

```pulsar
define numbers = [10, 20, 30];
```

An object:

```pulsar
define user = {
    name: "Alex",
    age: 20
};
```

A function:

```pulsar
define add = (a, b) => {
    return a + b;
};
```

---

## 6. Initializer Expressions

The value assigned to a variable can be an expression.

```pulsar
define total = 10 + 20;
```

Another variable can be used:

```pulsar
define price = 100;
define quantity = 3;

define total = price * quantity;
```

A function call can also be used:

```pulsar
define name = ask("Name: ");
```

The initializer is evaluated when the declaration is evaluated.

---

## 7. Variables Without an Initializer

The parser allows a declaration without an initializer:

```pulsar
define value;
```

The variable-declaration parser checks for `=` and, when it is absent, produces a declaration with no initializer. 

Because the exact runtime behavior of an uninitialized variable is interpreter-version dependent, programs should prefer explicit initialization:

```pulsar
define value = null;
```

This makes the intended state clear.

---

## 8. Assignment

Declaration and assignment are different operations.

Declaration:

```pulsar
define score = 10;
```

Assignment:

```pulsar
score = 20;
```

Example:

```pulsar
define score = 10;

show(score);

score = 20;

show(score);
```

The first statement creates the binding.

The second changes its value.

---

## 9. Assignment Expressions

Variables can be updated using expressions.

```pulsar
define price = 100;

price = price + 20;

show(price);
```

Result:

```text
120
```

Another example:

```pulsar
define quantity = 5;

quantity = quantity - 1;
```

---

## 10. Increment and Decrement

Numeric variables can be updated using increment/decrement syntax where supported by the interpreter.

```pulsar
define counter = 0;

counter++;

show(counter);
```

Decrement:

```pulsar
counter--;
```

These operations are particularly useful in loops:

```pulsar
define i = 0;

while (i < 5) {
    show(i);
    i++;
}
```

---

## 11. Reassigning Variables

A variable can be assigned another value.

```pulsar
define value = 10;

value = 20;
value = 30;
value = 40;
```

The variable remains the same binding while its stored value changes.

---

## 12. Variables and Expressions

Variables can participate in arithmetic:

```pulsar
define a = 10;
define b = 5;

define sum = a + b;
define difference = a - b;
define product = a * b;
define quotient = a / b;
```

They can participate in comparisons:

```pulsar
define age = 20;

if (age >= 18) {
    show("Allowed");
}
```

They can participate in logical expressions:

```pulsar
define active = true;
define verified = true;

if (active && verified) {
    show("Verified");
}
```

---

## 13. Variable Scope

Pulsar uses environments to store variable bindings.

Conceptually:

```text
Global Environment
        |
        v
Function Environment
        |
        v
Nested Environment
```

An environment can define variables and search its parent environment.

The runtime environment provides operations corresponding to:

```text
define
get
set
has
```

This environment chain is used by functions, loops, blocks, and other evaluator operations.

---

## 14. Global Variables

A variable declared at the top level belongs to the program's outer environment.

```pulsar
define appName = "Pulsar";

func showName() {
    show(appName);
}

showName();
```

The function can resolve `appName` through its parent environment.

---

## 15. Function Variables

Functions can be assigned to variables.

```pulsar
define add = (a, b) => {
    return a + b;
};
```

The variable can then be called:

```pulsar
define result = add(10, 20);

show(result);
```

A variable does not have to contain only primitive data.

---

## 16. Variables Inside Functions

Variables can be declared inside functions:

```pulsar
func calculate() {
    define price = 100;
    define quantity = 2;

    return price * quantity;
}

show(calculate());
```

These variables belong to the function's execution environment.

---

## 17. Function Parameters Are Variables

Function parameters become bindings inside the function environment.

```pulsar
func greet(name) {
    show(name);
}
```

When:

```pulsar
greet("Pulsar");
```

is evaluated, `name` receives the supplied argument.

Multiple parameters:

```pulsar
func add(a, b) {
    return a + b;
}
```

Here `a` and `b` are local bindings.

---

## 18. Variables in Loops

Variables can be declared in a standard `for` loop:

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

The standard loop creates a local environment for its initialization, condition, body, and update operations.

---

## 19. For-In Variables

A `for-in` loop binds the current value to its loop variable.

```pulsar
define numbers = [10, 20, 30];

for number in numbers {
    show(number);
}
```

Here:

```text
number
```

is the loop variable.

For arrays, each iteration receives an array value.

For objects, the loop variable receives an object key.

```pulsar
define user = {
    name: "Alex",
    age: 20
};

for key in user {
    show(key);
}
```

---

## 20. Loop Variable Environments

The interpreter's `for-in` evaluator creates a loop environment when the relevant loop declaration requires it.

Conceptually:

```text
Outer Environment
       |
       +-- Loop Environment
       |      number = 10
       |
       +-- Loop Environment
              number = 20
```

This prevents loop iteration bindings from being confused with unrelated surrounding bindings.

---

## 21. Variables and Arrays

An array can be stored in a variable:

```pulsar
define products = [
    "Laptop",
    "Keyboard",
    "Mouse"
];
```

Its elements can be accessed:

```pulsar
show(products[0]);
show(products[1]);
```

An array element can also be assigned:

```pulsar
products[0] = "Monitor";
```

---

## 22. Variables and Objects

Objects can be assigned to variables:

```pulsar
define product = {
    id: 1,
    name: "Laptop",
    price: 1200
};
```

Properties can be accessed:

```pulsar
show(product.name);
show(product.price);
```

Properties can be modified:

```pulsar
product.price = 1100;
```

---

## 23. Nested Variables

Objects and arrays can be combined:

```pulsar
define shop = {
    name: "Pulsar Shop",

    products: [
        {
            name: "Laptop",
            price: 1200
        },
        {
            name: "Mouse",
            price: 40
        }
    ]
};
```

Access:

```pulsar
show(shop.name);
show(shop.products[0].name);
show(shop.products[0].price);
```

---

## 24. Variable Aliasing

Assigning one variable to another can cause both variables to refer to the same runtime object when the value is an object or array.

```pulsar
define first = {
    name: "Pulsar"
};

define second = first;

second.name = "Updated";

show(first.name);
```

The exact mutation behavior follows the JavaScript-based runtime representation used by the interpreter.

---

## 25. Variables and `null`

A variable can intentionally contain `null`:

```pulsar
define product = null;
```

Later:

```pulsar
product = {
    name: "Laptop"
};
```

This is useful when a value is not immediately available.

A common lookup pattern is:

```pulsar
func findProduct(id) {
    for product in products {
        if (product.id == id) {
            return product;
        }
    }

    return null;
}

define product = findProduct(10);

if (product == null) {
    show("Product not found");
}
```

---

## 26. Constants

The current `define` syntax does not establish a separate `const` declaration form in the documented Pulsar syntax.

For example, Pulsar code normally uses:

```pulsar
define version = 1;
```

rather than:

```pulsar
const version = 1;
```

Do not document `const` as a Pulsar language feature unless it is actually implemented by the interpreter.

---

## 27. Type Declarations

The current variable syntax does not require explicit type annotations.

Use:

```pulsar
define age = 20;
```

rather than requiring:

```text
int age = 20;
```

Pulsar determines the runtime value through evaluation.

A variable can therefore contain different kinds of values at different points:

```pulsar
define value = 10;

value = "Pulsar";
```

Whether this is desirable is a programming-design decision rather than a separate static type declaration.

---

## 28. Variable Lookup

When an expression references a variable:

```pulsar
show(name);
```

the evaluator resolves the identifier through the current environment.

Conceptually:

```text
Current Environment
        |
        | name exists?
        |---- yes -> value
        |
        v
Parent Environment
        |
        | name exists?
        |---- yes -> value
        |
        v
Continue searching
```

If the variable cannot be found, the runtime reports an undefined-variable error.

---

## 29. Variable Assignment Lookup

Assignment:

```pulsar
score = 100;
```

updates an existing binding.

The environment chain is used to locate the appropriate variable.

This differs from:

```pulsar
define score = 100;
```

which creates a declaration in the current environment.

---

## 30. Variable Shadowing

Nested environments can contain bindings with the same name.

For example:

```pulsar
define name = "Global";

func example() {
    define name = "Local";

    show(name);
}

example();

show(name);
```

The inner binding takes precedence while evaluating the inner environment.

The outer binding remains available after the inner scope ends.

The exact shadowing behavior follows the environment implementation.

---

## 31. Variables and Closures

A function can retain access to values from the environment where the function was created.

Conceptually:

```pulsar
func makeCounter() {
    define count = 0;

    return () => {
        count++;
        return count;
    };
}
```

The function's environment is retained as part of the function value.

This behavior depends on the evaluator's environment-chain implementation.

---

## 32. Variables Returned From Functions

A function can return a variable:

```pulsar
func getName() {
    define name = "Pulsar";

    return name;
}

define result = getName();

show(result);
```

The returned value becomes the initializer value of `result`.

---

## 33. Variables Passed to Functions

Variables can be supplied as arguments:

```pulsar
define price = 100;
define quantity = 3;

define total = calculateTotal(price, quantity);
```

Function:

```pulsar
func calculateTotal(price, quantity) {
    return price * quantity;
}
```

The parameter bindings receive the evaluated argument values.

---

## 34. Variables in Conditions

Variables are commonly used as conditions:

```pulsar
define loggedIn = true;

if (loggedIn) {
    show("Welcome");
}
```

More complex:

```pulsar
define age = 20;
define verified = true;

if (age >= 18 && verified) {
    show("Access granted");
}
```

---

## 35. Variables in Expressions

Variables can appear anywhere an expression is accepted.

```pulsar
define a = 10;
define b = 20;

define result = (a + b) * 2;
```

They can also be used inside arrays:

```pulsar
define x = 10;

define values = [
    x,
    x + 1,
    x + 2
];
```

And objects:

```pulsar
define name = "Pulsar";
define version = 1;

define info = {
    name: name,
    version: version
};
```

---

## 36. Variables With Built-ins

Variables commonly receive values returned by built-in functions:

```pulsar
define input = ask("Enter a number: ");

define number = num(input);

show(number);
```

Another example:

```pulsar
define text = "Pulsar";

define upperText = upper(text);

show(upperText);
```

---

## 37. Variables and JSON

Parsed JSON can be stored in a variable:

```pulsar
define jsonText = "{\"name\":\"Pulsar\"}";

define data = JSONParse(jsonText);

show(data.name);
```

A variable can then contain the parsed object.

---

## 38. Variables and Server Requests

In a server application, request values can be stored in variables:

```pulsar
app.get("/users/:id", (req, res) => {
    define id = req.params.id;

    return {
        id: id
    };
});
```

Query parameters:

```pulsar
app.get("/search", (req, res) => {
    define query = req.query.q;

    return {
        query: query
    };
});
```

Request body:

```pulsar
app.post("/users", (req, res) => {
    define name = req.body.name;

    return {
        name: name
    };
});
```

---

## 39. Variables and HTML Templates

Server-side data can be stored in variables before being injected into an HTML template:

```pulsar
define title = "Pulsar";
define message = "Hello from the server";

return res.render("index.html", {
    title: title,
    message: message
});
```

HTML:

```html
<h1>{{title}}</h1>
<p>{{message}}</p>
```

The template renderer resolves the supplied values.

---

## 40. Good Variable Naming

Prefer names that describe the value:

```pulsar
define productPrice = 1200;
define quantity = 2;
define customerName = "Alex";
define totalPrice = productPrice * quantity;
```

Avoid unnecessarily ambiguous names:

```pulsar
define x = 1200;
define a = 2;
define z = x * a;
```

Short names are still useful for mathematical expressions and loop counters:

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

---

## 41. Complete Variable Example

```pulsar
define productName = "Laptop";
define productPrice = 1200;
define quantity = 2;
define discountRate = 0.10;

define subtotal = productPrice * quantity;
define discount = subtotal * discountRate;
define total = subtotal - discount;

show(productName);
show(subtotal);
show(discount);
show(total);
```

---

## 42. Variables in a Shop Program

A larger example:

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
    }
];

define cart = [];

func addProduct(id, quantity) {
    for product in products {
        if (product.id == id) {
            if (product.stock >= quantity) {
                cart.push({
                    product: product,
                    quantity: quantity
                });

                product.stock =
                    product.stock - quantity;

                return true;
            }
        }
    }

    return false;
}

define added = addProduct(1, 1);

if (added) {
    show("Product added");
}
```

This demonstrates variables at several levels:

```text
products
cart
id
quantity
product
added
```

---

## 43. Variable Declaration vs Assignment

| Operation           | Syntax                | Purpose                         |
| ------------------- | --------------------- | ------------------------------- |
| Declaration         | `define x = 10;`      | Create a variable               |
| Assignment          | `x = 20;`             | Change an existing variable     |
| Property assignment | `user.name = "Alex";` | Change an object property       |
| Array assignment    | `items[0] = value;`   | Change an array element         |
| Parameter binding   | `func test(x) {}`     | Create function-local parameter |
| Loop binding        | `for x in items {}`   | Bind iteration value            |

---

## 44. Recommended Patterns

Initialize values explicitly:

```pulsar
define result = null;
```

Use descriptive names:

```pulsar
define customerName = "Alex";
```

Keep calculations readable:

```pulsar
define subtotal = price * quantity;
define discount = subtotal * 0.10;
define total = subtotal - discount;
```

Use separate variables when a calculation represents an important concept.

---

## 45. Important Runtime Behavior

Variables are runtime bindings rather than statically declared machine-level storage.

The interpreter evaluates:

```pulsar
define x = expression;
```

by evaluating the initializer and defining the resulting value in the current environment.

Function calls create child environments, and the evaluator resolves names through the environment chain.

The interpreter's environment implementation is therefore fundamental to variable behavior.

---

## 46. Summary

Pulsar variables are created with `define`:

```pulsar
define name = "Pulsar";
```

They can store many kinds of runtime values:

```pulsar
define number = 10;
define text = "Pulsar";
define active = true;
define items = [1, 2, 3];
define user = {
    name: "Alex"
};
define empty = null;
```

Existing variables can be reassigned:

```pulsar
number = 20;
```

Variables can be used in:

```text
Expressions
Conditions
Loops
Functions
Arrays
Objects
Entities
JSON
Server routes
HTML rendering
```

The core pattern is:

```pulsar
define variable = value;
```

followed by normal expression and assignment syntax:

```pulsar
variable = newValue;
```
