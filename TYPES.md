## 1. Overview

Pulsar is a dynamically evaluated language. Values produced by expressions have runtime types, and those types determine what operations can be performed on them.

The primary value categories represented in the Pulsar interpreter are:

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

Pulsar does not require traditional static declarations such as:

```text
int
float
string
bool
```

Instead, the type of a value comes from the value produced at runtime.

---

## 2. Runtime Typing

A variable is a name associated with a runtime value:

```pulsar
define name = "Pulsar";
define version = 1;
define active = true;
```

Conceptually:

```text
name    -> String
version -> Number
active  -> Boolean
```

The variable declaration itself does not contain an explicit type.

---

## 3. String

A string represents textual data.

```pulsar
define name = "Pulsar";
define message = "Hello world";
```

Strings can be combined:

```pulsar
define first = "Hello";
define second = "Pulsar";

define message = first + " " + second;
```

Strings are also valid values inside arrays and objects:

```pulsar
define data = [
    "Pulsar",
    "language",
    "runtime"
];
```

---

## 4. Number

Numbers represent numeric values.

```pulsar
define integer = 100;
define decimal = 3.14;
```

Arithmetic expressions produce numbers:

```pulsar
define a = 10;
define b = 20;

define result = a + b;
```

Other arithmetic operations include:

```pulsar
define addition = 10 + 5;
define subtraction = 10 - 5;
define multiplication = 10 * 5;
define division = 10 / 5;
define remainder = 10 % 3;
```

Pulsar's supplied examples demonstrate integer and decimal numeric values and arithmetic expressions.  

---

## 5. Boolean

A boolean has one of two values:

```pulsar
true
false
```

Example:

```pulsar
define connected = true;
define finished = false;
```

Booleans are commonly produced by comparisons:

```pulsar
define result = 10 > 5;
```

and logical expressions:

```pulsar
define allowed = true && false;
```

They are particularly useful with conditional statements:

```pulsar
if (connected) {
    show("Connected");
}
```

---

## 6. Null

`null` represents the absence of a value.

```pulsar
define result = null;
```

It is especially useful for representing an unavailable result:

```pulsar
func findUser(id) {
    return null;
}
```

Then:

```pulsar
define user = findUser(10);

if (user == null) {
    show("User not found");
}
```

`null` is a distinct runtime value and should not be confused with an empty string, empty array, or empty object.

---

## 7. Array

An array represents an ordered collection.

```pulsar
define numbers = [10, 20, 30];
```

Arrays can contain different types:

```pulsar
define values = [
    10,
    "Pulsar",
    true,
    null
];
```

They can also contain objects:

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

## 8. Nested Arrays

An array can contain other arrays.

```pulsar
define matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
];
```

Values can be accessed through indexes:

```pulsar
show(matrix[0][1]);
```

Arrays therefore allow arbitrary nested data structures.

---

## 9. Object

An object is a collection of named properties.

```pulsar
define user = {
    name: "Pulsar",
    age: 20,
    active: true
};
```

Properties can be accessed with dot notation:

```pulsar
show(user.name);
show(user.age);
show(user.active);
```

The supplied examples demonstrate objects containing strings, numbers, booleans, and nested structures. 

---

## 10. Nested Objects

Objects can contain other objects:

```pulsar
define user = {
    profile: {
        name: "Pulsar",
        version: 1
    }
};

show(user.profile.name);
```

Objects and arrays can also be combined:

```pulsar
define application = {
    name: "Pulsar",
    versions: [
        1,
        2,
        3
    ]
};
```

---

## 11. Empty Values

Pulsar can represent several different empty states:

```pulsar
define nothing = null;
define text = "";
define list = [];
define object = {};
```

These are different values:

```text
null
""
[]
{}
```

The supplied interpreter's `isEmpty()` implementation specifically recognizes `null`, empty arrays, empty strings, and empty objects. 

---

## 12. Function

Functions are callable runtime values.

Named function:

```pulsar
func add(a, b) {
    return a + b;
}
```

Calling it:

```pulsar
define result = add(10, 20);
```

The result has the type of the value returned by the function.

For example:

```pulsar
func getNumber() {
    return 100;
}
```

produces a number when called.

```pulsar
define value = getNumber();
```

---

## 13. Function Values

Functions can themselves be stored in variables.

```pulsar
define add = (a, b) => a + b;
```

The variable:

```text
add
```

contains a callable value.

It can then be used:

```pulsar
show(add(10, 20));
```

---

## 14. Arrow Function

Arrow functions are another way to create callable values.

```pulsar
define square = x => x * x;
```

Multiple parameters:

```pulsar
define add = (a, b) => a + b;
```

Block body:

```pulsar
define calculate = (a, b) => {
    define result = a * b;
    return result;
};
```

The supplied examples demonstrate arrow functions returning numbers, strings, booleans, array values, and object properties. 

---

## 15. Callable vs Non-Callable Types

Not every value is callable.

This is valid:

```pulsar
define add = (a, b) => a + b;

define result = add(1, 2);
```

This is not:

```pulsar
define number = 10;

number();
```

The evaluator explicitly checks whether a function-call target is callable. If it is not, it raises:

```text
Value is not callable
```



---

## 16. Entity Instance

Pulsar supports entities as runtime object types.

Example:

```pulsar
entity User {
    init(name) {
        self.name = name;
    }

    greet() {
        return "Hello " + self.name;
    }
}
```

An instance can be created:

```pulsar
define user = new User("Pulsar");
```

The variable `user` contains an entity instance.

The supplied interpreter examples demonstrate entity construction, properties, methods, and inheritance. 

---

## 17. Entity Instance Properties

An entity instance can contain state:

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }
}

define counter = new Counter(10);

show(counter.value);
```

The property itself can contain another runtime value.

---

## 18. Entity Methods

Entity methods are callable values associated with an entity.

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

define value = counter.increment();

show(value);
```

The supplied examples demonstrate state-changing entity methods and returned numeric values. 

---

## 19. Inherited Entity Types

Entities can inherit from other entities.

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

Creating an instance:

```pulsar
define admin = new Admin("Pulsar");
```

The resulting instance has access to inherited behavior and its own behavior.

The supplied entity examples demonstrate parent initialization and child methods. 

---

## 20. Dynamic Typing

Pulsar variables do not require a declared static type.

For example:

```pulsar
define value = 100;
```

The value is numeric.

A later assignment can change the stored runtime value:

```pulsar
value = "Pulsar";
```

The language therefore operates around runtime values rather than declarations such as:

```text
int value
string value
```

Do not treat `define` as a static type declaration.

---

## 21. Expression Result Types

Expressions produce values.

```pulsar
define a = 10;
define b = 20;

define result = a + b;
```

Here:

```text
a       -> Number
b       -> Number
a + b   -> Number
result  -> Number
```

A comparison produces a boolean:

```pulsar
define result = 10 > 5;
```

Conceptually:

```text
10      -> Number
5       -> Number
10 > 5  -> Boolean
result  -> Boolean
```

---

## 22. Property Access Types

Accessing a property produces the property's value.

```pulsar
define user = {
    name: "Pulsar",
    age: 20
};

define name = user.name;
define age = user.age;
```

Conceptually:

```text
user      -> Object
user.name -> String
user.age  -> Number
```

---

## 23. Array Access Types

An array access produces the value stored at that position.

```pulsar
define values = [
    100,
    "Pulsar",
    true
];

define first = values[0];
define second = values[1];
define third = values[2];
```

Conceptually:

```text
first  -> Number
second -> String
third  -> Boolean
```

The same array can therefore contain values of different runtime types.

---

## 24. Function Return Types

Pulsar functions do not require a declared return type.

```pulsar
func getName() {
    return "Pulsar";
}
```

The returned value is a string.

Another function can return a number:

```pulsar
func getVersion() {
    return 1;
}
```

A function can return an object:

```pulsar
func getUser() {
    return {
        name: "Pulsar"
    };
}
```

The runtime type comes from the actual returned value.

---

## 25. Functions Returning Different Values

Because return values are evaluated at runtime, a function can choose between different values:

```pulsar
func getValue(active) {
    if (active) {
        return "Pulsar";
    }

    return null;
}
```

The result can therefore be:

```text
String
```

or:

```text
Null
```

depending on the runtime condition.

---

## 26. Parameters and Types

Function parameters do not require static type annotations.

```pulsar
func add(a, b) {
    return a + b;
}
```

The values supplied by the caller determine what the parameters contain at runtime.

```pulsar
add(10, 20);
```

supplies numeric values.

```pulsar
add("Hello ", "Pulsar");
```

supplies string values.

The actual operation must still be valid for the supplied values.

---

## 27. Mixed-Type Collections

Pulsar arrays and objects can contain multiple value types.

```pulsar
define data = [
    10,
    "Pulsar",
    true,
    null,
    [1, 2],
    {
        name: "Pulsar"
    }
];
```

This creates a heterogeneous collection.

Its elements have different runtime types.

---

## 28. JSON-Compatible Types

The following common Pulsar values naturally correspond to JSON data:

```text
String
Number
Boolean
Null
Array
Object
```

Example:

```pulsar
define user = {
    name: "Pulsar",
    age: 20,
    active: true,
    tags: [
        "language",
        "runtime"
    ]
};
```

This makes these value types useful for APIs and server responses.

The supplied server implementation supports returning object values as JSON responses. 

---

## 29. JSON Parsing

JSON text can be converted into runtime values:

```pulsar
define text = "{\"name\":\"Pulsar\",\"version\":1}";

define data = JSONParse(text);

show(data.name);
show(data.version);
```

The resulting `data` value is an object.

The supplied evaluator uses JSON parsing for this built-in and reports invalid JSON as a runtime error. 

---

## 30. Server Values

The built-in server works with normal Pulsar runtime values.

For example:

```pulsar
app.get("/api/status", (req, res) => {
    return {
        status: "running",
        online: true
    };
});
```

The returned value is an object and is serialized as a JSON response by the server. 

---

## 31. HTML Values

Server-side values can also be passed into HTML rendering.

```pulsar
app.get("/", (req, res) => {
    define title = "Pulsar";

    return res.render("index.html", {
        title: title
    });
});
```

HTML:

```html
<h1>{{title}}</h1>
```

Here:

```text
title -> String
```

and the template receives that value.

The supplied server documentation demonstrates direct and nested template value injection. 

---

## 32. Request Values

HTTP request information can become runtime values.

For example:

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

Form data:

```pulsar
app.post("/users", (req, res) => {
    define name = req.body.name;

    return {
        name: name
    };
});
```

The supplied server implementation exposes route parameters, query parameters, and parsed request bodies through the request object. 

---

## 33. Empty Type Values

The following are distinct:

```pulsar
define a = null;
define b = "";
define c = [];
define d = {};
```

Their categories are:

```text
a -> Null
b -> String
c -> Array
d -> Object
```

They should not be treated as interchangeable.

---

## 34. Reference-Type Values

Compound JavaScript-backed values such as arrays and objects behave as runtime objects.

For example:

```pulsar
define original = {
    value: 10
};

define copy = original;

copy.value = 20;
```

`copy` and `original` refer to the same underlying compound value unless an explicit copy is made.

The supplied evaluator includes `deepClone()` for producing a deep copy of supported JSON-like data. 

---

## 35. Runtime Type vs Variable Name

A variable name is not a type.

For:

```pulsar
define user = {
    name: "Pulsar"
};
```

the terms mean:

```text
user
```

is the variable name.

```text
Object
```

describes the runtime category of its value.

The same principle applies to:

```pulsar
define count = 10;
```

where:

```text
count  -> variable
10     -> Number value
```

---

## 36. Type-Oriented Example

```pulsar
define language = "Pulsar";
define version = 1;
define stable = true;
define metadata = null;

define features = [
    "functions",
    "entities",
    "server"
];

define project = {
    name: language,
    version: version,
    stable: stable,
    metadata: metadata,
    features: features
};
```

The resulting structure is:

```text
language
  String

version
  Number

stable
  Boolean

metadata
  Null

features
  Array
    String
    String
    String

project
  Object
```

---

## 37. Complete Types Example

```pulsar
define text = "Pulsar";
define number = 42;
define decimal = 3.14;
define booleanValue = true;
define nothing = null;

define array = [
    1,
    2,
    3
];

define object = {
    name: "Pulsar",
    version: 1
};

define add = (a, b) => a + b;

show(text);
show(number);
show(decimal);
show(booleanValue);
show(nothing);
show(array);
show(object);
show(add(10, 20));
```

This demonstrates the core runtime value categories in one program.

---

## 38. Type Categories Summary

| Type              | Example            | Description            |
| ----------------- | ------------------ | ---------------------- |
| `String`          | `"Pulsar"`         | Text value             |
| `Number`          | `42`               | Numeric value          |
| `Boolean`         | `true`             | True/false value       |
| `Null`            | `null`             | Absence of a value     |
| `Array`           | `[1, 2, 3]`        | Ordered collection     |
| `Object`          | `{name: "Pulsar"}` | Named properties       |
| `Function`        | `(x) => x * 2`     | Callable value         |
| `Entity Instance` | `new User("Alex")` | Stateful entity object |

---

## 39. Types and the Interpreter

Pulsar's interpreter evaluates expressions into runtime values rather than requiring every variable to carry a static declaration such as:

```text
int
float
string
boolean
```

The runtime environment stores those resulting values.

Conceptually:

```text
Source Code
    |
    v
Parser
    |
    v
Expression
    |
    v
Evaluator
    |
    v
Runtime Value
```

For example:

```pulsar
define result = 10 + 20;
```

becomes conceptually:

```text
10 + 20
   |
   v
30
   |
   v
result -> Number
```

---

## 40. Important Distinction

Pulsar's **value types** should not be confused with every category appearing inside the interpreter implementation.

For example, internal runtime mechanisms may include:

```text
Environment
RuntimeError
BreakSignal
ContinueSignal
ReturnSignal
EntityDefinition
EntityInstance
```

These are interpreter/runtime implementation concepts.

They are not all ordinary user-facing Pulsar value types.

In particular, `break`, `continue`, and `return` represent control flow rather than ordinary data values.

---

## 41. Practical Type Model

For everyday Pulsar programming, the most useful model is:

```text
Primitive Values
├── String
├── Number
├── Boolean
└── Null

Compound Values
├── Array
└── Object

Callable Values
├── Function
└── Arrow Function

Object-Oriented Runtime Values
└── Entity Instance
```

This model covers the primary types demonstrated by the supplied Pulsar interpreter and examples.

---

## 42. Final Example

```pulsar
define name = "Pulsar";
define version = 1;
define released = true;
define previous = null;

define versions = [
    1,
    2,
    3
];

define project = {
    name: name,
    version: version,
    released: released,
    previous: previous,
    versions: versions
};

define getVersion = () => project.version;

show(name);
show(version);
show(released);
show(previous);
show(versions);
show(project);
show(getVersion());
```

The program combines the principal Pulsar runtime types:

```text
String
Number
Boolean
Null
Array
Object
Function
```