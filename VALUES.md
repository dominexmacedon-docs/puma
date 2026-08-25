## 1. Overview

A value is the runtime result produced by evaluating a Pulsar expression.

Examples:

```pulsar
define name = "Pulsar";
define version = 1;
define active = true;
define empty = null;
```

Pulsar programs can also produce compound values:

```pulsar
define numbers = [1, 2, 3];

define user = {
    name: "Pulsar",
    active: true
};
```

The supplied examples explicitly cover strings, numbers, booleans, `null`, arrays, objects, functions, and entity instances.  

---

# 2. Value Categories

The main runtime value categories used by Pulsar are:

```text
String
Number
Boolean
Null
Array
Object
Function
Entity Instance
```

There are also runtime-specific values associated with the interpreter, such as callable built-ins and entity definitions.

---

# 3. String Values

A string is a sequence of characters enclosed in quotation marks.

```pulsar
define language = "Pulsar";

show(language);
```

String literals can be combined:

```pulsar
define message = "Hello " + "Pulsar";

show(message);
```

The supplied examples demonstrate both literal strings and string concatenation. 

Strings can also be passed to functions:

```pulsar
func greet(name) {
    return "Hello " + name;
}

show(greet("Pulsar"));
```

---

# 4. Number Values

Numbers can represent integer and decimal values.

```pulsar
define version = 1;
define pi = 3.14159;
```

Arithmetic produces numeric values:

```pulsar
define a = 10;
define b = 20;

define sum = a + b;
```

The supplied examples include integer values, decimal values, arithmetic operations, and unary positive/negative numbers.  

Examples:

```pulsar
show(10 + 5);
show(10 - 5);
show(10 * 5);
show(20 / 5);
show(17 % 5);
```

---

# 5. Boolean Values

Boolean values are:

```pulsar
true
false
```

Example:

```pulsar
define active = true;
define inactive = false;

show(active);
show(inactive);
```

The examples explicitly demonstrate both boolean values. 

Booleans are commonly used in conditions:

```pulsar
define active = true;

if (active) {
    show("Active");
}
```

---

# 6. Null

`null` represents the absence of a value.

```pulsar
define empty = null;

show(empty);
```

The supplied basic-value examples explicitly include `null`. 

A function can intentionally return `null`:

```pulsar
func findUser(id) {
    return null;
}
```

It can then be tested:

```pulsar
define user = findUser(10);

if (user == null) {
    show("User not found");
}
```

---

# 7. Arrays

An array is an ordered collection of values.

```pulsar
define numbers = [1, 2, 3, 4];
```

Arrays can contain different value types:

```pulsar
define mixed = [
    1,
    "two",
    true,
    null
];
```

The supplied examples explicitly demonstrate mixed arrays containing numbers, strings, booleans, and `null`. 

---

# 8. Array Elements

Array elements can themselves be arrays:

```pulsar
define matrix = [
    [1, 2],
    [3, 4]
];
```

Accessing an element:

```pulsar
show(matrix[0]);
show(matrix[0][1]);
```

Arrays can contain objects:

```pulsar
define products = [
    {
        name: "Laptop",
        price: 1200
    },
    {
        name: "Mouse",
        price: 40
    }
];
```

---

# 9. Array Mutation

An array value can be modified:

```pulsar
define values = [10, 20, 30];

values[0] = 100;

show(values[0]);
```

Array values can also be manipulated through built-in array operations.

For example, the interpreter's examples use arrays with higher-order operations such as map, filter, and reduce.

---

# 10. Array Slicing

Pulsar supports slicing syntax for arrays.

```pulsar
define values = [0, 1, 2, 3, 4];

show(values[1:4]);
```

The supplied examples also demonstrate:

```pulsar
define values = [0, 1, 2, 3, 4];

show(values[2:]);
```

and:

```pulsar
define values = [0, 1, 2, 3, 4, 5];

show(values[0:6:2]);
```

They also demonstrate negative indices and omitted bounds. 

---

# 11. String Slicing

The slicing syntax can also be applied to strings.

```pulsar
define text = "Pulsar";

show(text[0:3]);
```

The supplied examples explicitly demonstrate string slicing:

```pulsar
define text = "Puma";

show(text[0:2]);
```



---

# 12. Object Values

Objects are collections of named properties.

```pulsar
define user = {
    name: "Pulsar",
    active: true
};
```

The supplied examples demonstrate object literals containing multiple property types. 

Properties can be accessed with dot notation:

```pulsar
show(user.name);
show(user.active);
```

---

# 13. Nested Objects

Objects can contain other objects.

```pulsar
define nested = {
    user: {
        name: "Pulsar"
    }
};

show(nested.user.name);
```

The supplied examples explicitly demonstrate nested object access. 

---

# 14. Object Keys

Object keys can use quoted names when necessary.

```pulsar
define data = {
    "first-name": "Pulsar"
};

show(data["first-name"]);
```

Bracket notation is useful when a property name cannot conveniently be accessed with normal dot notation.

This form is included in the supplied examples. 

---

# 15. Empty Objects

An object can contain no properties:

```pulsar
define empty = {};

show(empty);
```

The supplied examples explicitly test empty objects. 

---

# 16. Object Mutation

Object properties can be changed after the object has been created.

```pulsar
define user = {
    name: "Pulsar",
    score: 100
};

user.score = 110;

show(user.score);
```

Compound assignment is also demonstrated by the supplied examples:

```pulsar
user.score += 10;
```



---

# 17. Mixed Objects

Objects can contain different value types:

```pulsar
define product = {
    id: 1,
    name: "Laptop",
    price: 1200,
    available: true,
    tags: ["computer", "portable"],
    metadata: {
        manufacturer: "Example"
    }
};
```

The value of each property is evaluated independently.

---

# 18. Functions as Values

Functions are runtime values.

A named function can be called:

```pulsar
func add(a, b) {
    return a + b;
}

show(add(2, 3));
```

The supplied examples demonstrate functions returning numbers, strings, booleans, objects, and other computed values. 

A function can also be assigned to a variable:

```pulsar
define add = (a, b) => a + b;

show(add(10, 20));
```

---

# 19. Function Return Values

A function can produce a value with `return`.

```pulsar
func square(x) {
    return x * x;
}

define result = square(5);

show(result);
```

The value returned by the function becomes the value of the function-call expression.

---

# 20. Functions Returning Objects

Functions can return objects:

```pulsar
func makePoint(x, y) {
    return {
        x: x,
        y: y
    };
}

define point = makePoint(10, 20);

show(point.x);
```

This pattern is explicitly included in the supplied examples. 

---

# 21. Functions Returning Booleans

A function can return `true` or `false`.

```pulsar
func isEven(x) {
    return x % 2 == 0;
}

define result = isEven(8);

show(result);
```

The supplied examples use this exact value pattern. 

---

# 22. Functions With No Explicit Return

A function can execute without explicitly returning a value:

```pulsar
func noResult() {
    show("inside");
}

define result = noResult();

show(result);
```

The evaluator normalizes an undefined function result to `null`. The supplied evaluator explicitly performs this normalization for both native and user-defined calls. 

Therefore, conceptually:

```pulsar
func test() {
}
```

produces:

```text
null
```

when called.

---

# 23. Arrow Functions as Values

Arrow functions are also callable runtime values.

```pulsar
define double = x => x * 2;

show(double(5));
```

Multiple parameters:

```pulsar
define add = (a, b) => a + b;

show(add(2, 8));
```

The supplied examples demonstrate arrow functions returning numbers, strings, booleans, array elements, and object properties. 

---

# 24. Entity Instances

An entity instance is a runtime object created from an entity definition.

```pulsar
entity User {
    init(name) {
        self.name = name;
    }
}

define user = new User("Pulsar");
```

The instance can contain properties and methods.

```pulsar
show(user.name);
```

The supplied entity examples demonstrate construction, properties, methods, and inheritance. 

---

# 25. Entity Methods as Values

An entity method can be called through an instance:

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }

    increment() {
        self.value++;
        return self.value;
    }
}

define counter = new Counter(0);

show(counter.increment());
```

The supplied examples demonstrate this exact value flow. 

---

# 26. Inherited Entity Values

An inherited entity can access properties initialized by its parent.

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

define admin = new Admin("Pulsar");

show(admin.name);
show(admin.isAdmin());
```

The supplied examples demonstrate inherited instances containing parent-created state and child methods. 

---

# 27. Callable Values

The interpreter distinguishes callable values from ordinary values.

A callable can be:

```text
User-defined function
Native JavaScript function / built-in
Function expression
Arrow function
Entity method
```

When a function call is evaluated, the evaluator checks whether the value is callable.

If it is not callable, the runtime produces:

```text
Value is not callable
```

The evaluator explicitly performs this check. 

---

# 28. Values in Variables

Any runtime value can be stored in a variable.

```pulsar
define number = 100;
define text = "Pulsar";
define flag = true;
define nothing = null;

define array = [1, 2, 3];

define object = {
    name: "Pulsar"
};
```

The same variable can be used in later expressions:

```pulsar
define price = 100;
define quantity = 3;

define total = price * quantity;
```

---

# 29. Values in Arrays

Arrays can contain other values:

```pulsar
define data = [
    10,
    "Pulsar",
    true,
    null,
    [1, 2],
    {
        name: "Alex"
    }
];
```

This allows nested data structures.

---

# 30. Values in Objects

Object properties can contain any supported runtime value:

```pulsar
define application = {
    name: "Pulsar",
    version: 1,
    active: true,
    tags: ["language", "runtime"],
    config: {
        debug: false
    }
};
```

A function can also be stored as a property where the runtime supports callable object properties:

```pulsar
define calculator = {
    add: (a, b) => a + b
};

show(calculator.add(10, 20));
```

---

# 31. Values Produced by Operators

Expressions produce values.

Arithmetic:

```pulsar
define result = 10 + 20;
```

Comparison:

```pulsar
define valid = 10 < 20;
```

Logical expression:

```pulsar
define allowed = true && false;
```

Property access:

```pulsar
define name = user.name;
```

Index access:

```pulsar
define first = numbers[0];
```

Function call:

```pulsar
define result = add(10, 20);
```

---

# 32. Values and Conditions

Values can be used as conditions:

```pulsar
define active = true;

if (active) {
    show("Active");
}
```

Comparison expressions themselves produce boolean values:

```pulsar
define age = 20;

define adult = age >= 18;

if (adult) {
    show("Adult");
}
```

---

# 33. Values Returned From Loops

Loop evaluation is a control-flow operation rather than a normal value-producing expression.

The evaluator returns `null` after completing `for` and `for-in` evaluation. 

For example:

```pulsar
define result = for (define i = 0; i < 3; i++) {
    show(i);
};
```

should not be treated as producing an array of loop results.

The loop's purpose is execution.

---

# 34. Values and `break`

`break` is a control-flow signal rather than an ordinary value.

```pulsar
while (true) {
    break;
}
```

The evaluator catches the internal `BreakSignal` and exits the current loop. 

---

# 35. Values and `continue`

Similarly, `continue` is a control-flow signal.

```pulsar
for (define i = 0; i < 5; i++) {
    if (i == 2) {
        continue;
    }

    show(i);
}
```

The evaluator handles `ContinueSignal` separately from normal values. 

---

# 36. Values and `return`

`return` transfers a value out of a function.

```pulsar
func getValue() {
    return 100;
}

define value = getValue();
```

Internally, the evaluator represents the return operation using a return-control value/signal and then extracts its contained value. 

---

# 37. Values and JSON

Pulsar values can be represented as JSON-compatible data.

Example:

```pulsar
define user = {
    name: "Pulsar",
    age: 20,
    active: true
};
```

The interpreter provides JSON parsing functionality that converts JSON text into runtime values.

```pulsar
define text = "{\"name\":\"Pulsar\"}";

define data = JSONParse(text);

show(data.name);
```

The runtime's JSON parsing functionality uses JavaScript JSON parsing and reports invalid JSON through a runtime error. 

---

# 38. Values and Server Responses

Pulsar values can be returned directly from server routes.

For example:

```pulsar
app.get("/api/status", (req, res) => {
    return {
        ok: true,
        status: "running"
    };
});
```

The built-in server treats a returned object as a JSON response. 

This makes normal Pulsar values useful for API development.

---

# 39. Values and HTML Templates

Pulsar objects can provide values to HTML templates.

```pulsar
return res.render("index.html", {
    title: "Pulsar",
    message: "Hello from the server"
});
```

The template can reference those values:

```html
<h1>{{title}}</h1>
<p>{{message}}</p>
```

Nested object values are also supported:

```html
<h1>{{user.name}}</h1>
```

The supplied server documentation explicitly describes direct and nested value injection.  

---

# 40. Values and Request Data

HTTP request data becomes runtime values.

For example:

```pulsar
app.get("/users/:id", (req, res) => {
    define id = req.params.id;

    return {
        id: id
    };
});
```

Form data can become an object:

```pulsar
app.post("/submit", (req, res) => {
    define name = req.body.name;

    return {
        name: name
    };
});
```

The built-in server places parsed form data in `req.body`. 

---

# 41. Value Conversion

Pulsar provides built-ins for converting values.

For example:

```pulsar
define text = "123";

define number = num(text);

show(number);
```

And:

```pulsar
define number = 123;

define text = str(number);

show(text);
```

The exact conversion behavior belongs to the built-in-function reference.

---

# 42. Value Inspection

Values can be displayed:

```pulsar
define data = {
    name: "Pulsar",
    version: 1
};

show(data);
```

The supplied examples use `show()` with primitive, array, object, and computed values throughout the test collection. 

---

# 43. Empty Values

Several empty states are possible:

```pulsar
define nothing = null;
define emptyArray = [];
define emptyObject = {};
define emptyString = "";
```

These values are distinct.

For example:

```text
null
[]
{}
""
```

should not be treated as the same runtime value.

The interpreter also provides `isEmpty()` for checking supported empty values. Its implementation considers `null`, empty arrays, empty strings, and empty objects. 

---

# 44. Deeply Nested Values

Pulsar values can be nested to create structured application data.

```pulsar
define company = {
    name: "Pulsar",
    owner: {
        name: "Alex",
        contact: {
            email: "example@example.com"
        }
    },
    products: [
        {
            name: "Runtime",
            versions: [1, 2, 3]
        }
    ]
};
```

Values can then be accessed through combinations of property and index access:

```pulsar
show(company.owner.contact.email);
show(company.products[0].versions[2]);
```

---

# 45. Value References

Objects and arrays are JavaScript runtime objects in the supplied evaluator.

Consequently, assigning a compound value to another variable can preserve the same underlying object reference:

```pulsar
define original = {
    value: 10
};

define copy = original;

copy.value = 20;

show(original.value);
```

This follows the JavaScript object model used by the interpreter rather than creating an automatic deep copy.

When an independent copy is required, the runtime provides operations such as `deepClone()`.

The supplied evaluator implements `deepClone()` using JSON serialization/deserialization. 

---

# 46. Runtime Value Formatting

The evaluator contains runtime formatting logic for displaying values.

This matters because:

```pulsar
show(value);
```

does not necessarily mean that the internal JavaScript representation is exposed directly. The evaluator has its own value-formatting behavior.

Therefore, the displayed representation of an object, array, function, or special runtime value should be considered interpreter output rather than a language-level serialization format.

---

# 47. Value Errors

Some operations require particular value categories.

For example, the `for-in` evaluator requires an object-like iterable value:

```pulsar
for item in value {
    show(item);
}
```

If the evaluated value is `null` or not an object, the evaluator raises:

```text
Cannot iterate over non-iterable
```

This behavior is explicitly implemented in the evaluator. 

---

# 48. Callable vs Non-Callable Values

This is an important distinction.

Callable:

```pulsar
define add = (a, b) => a + b;

show(add(1, 2));
```

Non-callable:

```pulsar
define number = 10;

number();
```

The latter produces a runtime error because the value is not callable. The evaluator explicitly checks for callable native functions or function objects and otherwise raises `Value is not callable`. 

---

# 49. Complete Mixed-Value Example

```pulsar
define language = "Pulsar";
define version = 1;
define stable = true;
define previousVersion = null;

define numbers = [
    10,
    20,
    30
];

define author = {
    name: "Dominex",
    active: true
};

define project = {
    name: language,
    version: version,
    stable: stable,
    previous: previousVersion,
    numbers: numbers,
    author: author
};

show(project.name);
show(project.version);
show(project.author.name);
show(project.numbers[0]);
```

This combines the primary value categories into one structured value.

---

# 50. Complete Function-Value Example

```pulsar
func createCalculator(base) {
    return {
        add: (value) => base + value,
        multiply: (value) => base * value
    };
}

define calculator = createCalculator(10);

show(calculator.add(5));
show(calculator.multiply(5));
```

Here:

```text
createCalculator
```

is a function value,

```text
calculator
```

is an object value,

and:

```text
calculator.add
calculator.multiply
```

are callable values.

---

# 51. Complete Entity-Value Example

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }

    increment() {
        self.value++;
        return self.value;
    }
}

define counter = new Counter(0);

define first = counter.increment();
define second = counter.increment();

show(first);
show(second);
```

The entity instance stores state in `self.value`, while its methods produce numeric values.

The supplied interpreter examples use this same general entity-state pattern. 

---

# 52. Value Categories Summary

| Value           | Example               | Typical use          |
| --------------- | --------------------- | -------------------- |
| String          | `"Pulsar"`            | Text                 |
| Number          | `100`                 | Numeric data         |
| Boolean         | `true`                | Conditions           |
| Null            | `null`                | No value             |
| Array           | `[1, 2, 3]`           | Ordered collections  |
| Object          | `{name: "Pulsar"}`    | Structured data      |
| Function        | `func add(a,b) {...}` | Callable logic       |
| Arrow function  | `x => x * 2`          | Short callable logic |
| Entity instance | `new User("Alex")`    | Stateful objects     |

---

# 53. Values vs Variables

A variable is a named binding.

A value is what that binding contains.

For:

```pulsar
define age = 20;
```

the distinction is:

```text
Variable:
age

Value:
20
```

For:

```pulsar
define user = {
    name: "Pulsar"
};
```

the distinction is:

```text
Variable:
user

Value:
{
    name: "Pulsar"
}
```

This distinction is fundamental to understanding the Pulsar runtime.

---

# 54. Values vs Expressions

An expression is something the interpreter evaluates.

The result is a value.

For example:

```pulsar
define result = 10 + 20;
```

Conceptually:

```text
Expression:
10 + 20

Evaluation:

10 + 20
   |
   v
30

Resulting value:
30
```

Similarly:

```pulsar
define result = add(10, 20);
```

produces whatever value `add()` returns.

---

# 55. Runtime Model

The supplied evaluator is JavaScript-based.

Its environment stores runtime values directly:

```javascript
store[name] = value;
```

and retrieves them through the environment chain. 

This means Pulsar's runtime values are closely connected to the JavaScript values used internally by the interpreter.

At the same time, Pulsar adds its own runtime semantics for:

```text
Functions
Entities
Methods
Environment scope
Return values
Control-flow signals
Runtime errors
Built-ins
```

---

# 56. Practical Rule

When writing Pulsar code, think of values as the things your expressions produce and manipulate:

```pulsar
define name = "Pulsar";

define age = 20;

define active = true;

define tags = ["language", "interpreter"];

define user = {
    name: name,
    age: age,
    active: active,
    tags: tags
};
```

The language then lets those values flow through:

```text
Variables
Expressions
Functions
Conditions
Loops
Arrays
Objects
Entities
JSON
HTTP requests
HTTP responses
HTML templates
```
