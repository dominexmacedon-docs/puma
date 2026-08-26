## 1. Overview

An environment is the runtime structure used by Pulsar to store variables and resolve their values during program execution.

Pulsar environments are particularly important for:

* variables
* functions
* parameters
* local variables
* nested functions
* outer-scope access
* variable lookup
* variable assignment
* scope chains

The Pulsar interpreter uses an `Environment` for this purpose. Functions create a new environment connected to the environment in which the function was defined. 

---

# 2. Basic Environment

At the top level, Pulsar executes code inside an environment.

For example:

```pulsar id="j7f2sp"
define name = "Pulsar";

show(name);
```

The variable:

```text
name
```

is stored in the current environment.

---

# 3. Defining a Variable

```pulsar id="qv4n6c"
define x = 100;

show(x);
```

Conceptually:

```text
Environment
└── x → 100
```

---

# 4. Multiple Variables

```pulsar id="8d6u3s"
define name = "Pulsar";
define version = 1;
define active = true;
```

The environment can contain multiple bindings:

```text
Environment
├── name → "Pulsar"
├── version → 1
└── active → true
```

---

# 5. Variable Lookup

When Pulsar evaluates:

```pulsar id="0z2qkv"
show(x);
```

the runtime must locate `x` in the current environment or an appropriate surrounding environment.

---

# 6. Function Environment

When a function is called, Pulsar creates a new environment for that function execution.

```pulsar id="w6j9la"
func calculate(value) {
    define result = value * 2;

    return result;
}

show(calculate(10));
```

Conceptually:

```text
Global Environment
└── calculate

Function Environment
├── value  → 10
└── result → 20
```

The supplied interpreter creates the function environment using the environment captured by the function. 

---

# 7. Environment Parent

A function environment has a parent environment.

Conceptually:

```text
Function Environment
        |
        v
Parent Environment
```

This allows code executing inside the function to access values from its surrounding environment.

---

# 8. Accessing an Outer Variable

```pulsar id="i3x3f7"
define x = 100;

func getX() {
    return x;
}

show(getX());
```

The function can find `x` through its surrounding environment. This behavior is explicitly demonstrated in the supplied Pulsar examples. 

---

# 9. Environment Chain

With nested scopes, environments form a chain.

```text
Current Environment
        |
        v
Parent Environment
        |
        v
Outer Environment
        |
        v
Global Environment
```

A variable lookup can therefore proceed outward through the chain.

---

# 10. Local Function Variables

```pulsar id="f7oyiy"
func test() {
    define value = 100;

    return value;
}

show(test());
```

`value` belongs to the function's environment.

The supplied function examples demonstrate local variables such as `result`, `y`, and `z` being created inside functions. 

---

# 11. Function Parameters

Function parameters are also placed into the function environment.

```pulsar id="gl0kh7"
func add(a, b) {
    return a + b;
}

show(add(10, 20));
```

Conceptually:

```text
Function Environment
├── a → 10
└── b → 20
```

The evaluator explicitly defines function parameters inside the newly created function environment. 

---

# 12. Local and Outer Variables

```pulsar id="3f7jz9"
define x = 10;

func test() {
    define y = 20;

    return x + y;
}

show(test());
```

The function environment contains `y`, while `x` is found through the outer environment.

---

# 13. Environment Shadowing

```pulsar id="9r7k8e"
define value = 100;

func test() {
    define value = 200;

    return value;
}

show(test());
show(value);
```

Conceptually:

```text
Function Environment
└── value → 200
       |
       v
Global Environment
└── value → 100
```

The local binding takes precedence when the function looks up `value`.

The supplied examples explicitly demonstrate this shadowing behavior. 

---

# 14. Outer Assignment

Pulsar can also assign to an existing outer variable.

```pulsar id="4v5j5u"
define value = 10;

func change() {
    value = 20;
}

change();

show(value);
```

Output:

```text
20
```

The supplied examples demonstrate this behavior directly. 

---

# 15. Assignment vs Definition

These operations have different purposes.

### Definition

```pulsar id="8x2a9g"
define value = 20;
```

Creates a binding in the current environment.

### Assignment

```pulsar id="f2c8pn"
value = 20;
```

Updates an existing binding according to the interpreter's environment resolution behavior.

The supplied scope examples distinguish local declarations from assignments to outer variables. 

---

# 16. Nested Functions

Pulsar supports nested function declarations.

```pulsar id="b7m8h1"
func outer(value) {
    func inner() {
        return value;
    }

    return inner();
}

show(outer(100));
```

The nested function can access the surrounding function's environment.

This pattern is explicitly demonstrated in the supplied examples. 

---

# 17. Nested Environment Chain

For the previous example, the conceptual structure is:

```text
Global Environment
        |
        v
outer Environment
├── value
└── inner
        |
        v
inner Environment
```

The inner function can resolve `value` through the surrounding environment.

---

# 18. Outer Function Parameter

```pulsar id="m9w5z0"
func outer(value) {
    func inner() {
        return value * 2;
    }

    return inner();
}

show(outer(5));
```

The `value` parameter belongs to the outer function's environment.

The nested function can read it.

---

# 19. Outer Local Variable

```pulsar id="n8bq3s"
func outer(value) {
    define doubled = value * 2;

    func inner() {
        return doubled;
    }

    return inner();
}

show(outer(10));
```

Here:

```text
outer Environment
├── value
├── doubled
└── inner
```

The inner function can access `doubled`.

---

# 20. Global Environment

A simple program can be represented as:

```text
Global Environment
├── products
├── cart
├── findProduct
├── addProduct
└── checkout
```

For example:

```pulsar id="8f8w8q"
define products = [];

define cart = [];

func checkout() {
    return 0;
}
```

---

# 21. Function Environment Example

When:

```pulsar id="3y8t3n"
checkout();
```

executes, the runtime creates the function's execution environment.

Conceptually:

```text
Checkout Environment
        |
        v
Global Environment
├── products
├── cart
└── checkout
```

---

# 22. Environment and Function Definition

The supplied evaluator evaluates a function declaration by creating a function value with access to the current environment. 

Conceptually:

```text
Function
├── parameters
├── body
└── environment
```

The environment is important because it tells the function where surrounding variables can be found.

---

# 23. Environment and Function Call

When the function is invoked, its captured environment becomes the parent of the new call environment.

Conceptually:

```text
Function
   |
   | call
   v
New Call Environment
   |
   v
Captured Environment
```

The supplied evaluator implements this relationship when executing function calls. 

---

# 24. Arrow Function Environment

Arrow functions use the same basic environment model.

```pulsar id="g9y4q5"
define factor = 10;

define multiply = x => x * factor;

show(multiply(5));
```

The arrow function receives its own execution environment while retaining access to the surrounding environment.

---

# 25. Arrow Function Parameters

```pulsar id="m5z2de"
define add = (a, b) => a + b;

show(add(10, 20));
```

Conceptually:

```text
Arrow Function Environment
├── a → 10
└── b → 20
```

The evaluator defines arrow-function parameters in the newly created environment. 

---

# 26. Arrow Function Outer Access

```pulsar id="q4w9zz"
define factor = 3;

define multiply = x => x * factor;

show(multiply(5));
```

The function receives:

```text
x → 5
```

from its call environment and obtains:

```text
factor → 3
```

from its surrounding environment.

---

# 27. Function Environment and `return`

```pulsar id="v5q8k3"
func calculate(value) {
    define result = value * 2;

    return result;
}
```

The function executes in its own environment.

When `return` is encountered, the return value is propagated out of the function execution. The evaluator explicitly handles `ReturnValue` while executing function bodies. 

---

# 28. Environment and `if`

An `if` statement can execute code using the current environment.

```pulsar id="0w4l9v"
define value = 10;

if value > 5 {
    show(value);
}
```

The condition and its body can access variables available in the surrounding environment.

---

# 29. Environment and Loops

```pulsar id="p2t0yb"
define values = [
    10,
    20,
    30
];

for value in values {
    show(value);
}
```

The loop evaluates its body with the environment associated with the loop execution.

The supplied interpreter has dedicated handling for `ForInStatement` and creates a loop environment when the syntax requests one. 

---

# 30. `for-in` Loop Environment

Conceptually:

```text
Outer Environment
       |
       v
Loop Environment
└── value → current element
```

For an array:

```pulsar id="w7g5q4"
define values = [
    10,
    20,
    30
];

for value in values {
    show(value);
}
```

the loop variable receives each array value.

---

# 31. Standard `for` Environment

```pulsar id="x5o4kq"
for (define i = 0; i < 5; i++) {
    show(i);
}
```

The supplied evaluator creates a local environment for standard `for` execution. 

Conceptually:

```text
For Environment
└── i
```

---

# 32. Environment and Objects

Objects themselves contain properties, while the environment contains variable bindings that may refer to those objects.

```pulsar id="f3p7g2"
define user = {
    name: "Alice",
    age: 20
};

show(user.name);
```

Conceptually:

```text
Environment
└── user ───────┐
                v
             Object
             ├── name → "Alice"
             └── age  → 20
```

---

# 33. Environment and Arrays

Similarly:

```pulsar id="5w1l5y"
define numbers = [
    10,
    20,
    30
];
```

Conceptually:

```text
Environment
└── numbers ─────┐
                 v
               Array
               ├── 10
               ├── 20
               └── 30
```

---

# 34. Environment Does Not Equal Object

An environment is used for variable bindings.

An object is a Pulsar value containing properties.

For example:

```pulsar id="y9c7q1"
define user = {
    name: "Alice"
};
```

The environment contains:

```text
user → object
```

while the object contains:

```text
name → "Alice"
```

These are different runtime concepts.

---

# 35. Environment Lookup Example

```pulsar id="0s7j5d"
define a = 10;

func test() {
    define b = 20;

    return a + b;
}

show(test());
```

Lookup for `b`:

```text
Function Environment
└── b → 20
```

Lookup for `a`:

```text
Function Environment
      |
      v
Global Environment
└── a → 10
```

---

# 36. Three-Level Environment Example

```pulsar id="4w0qj8"
define a = 10;

func outer() {
    define b = 20;

    func inner() {
        define c = 30;

        return a + b + c;
    }

    return inner();
}

show(outer());
```

Conceptually:

```text
Inner Environment
└── c → 30
       |
       v
Outer Environment
└── b → 20
       |
       v
Global Environment
└── a → 10
```

---

# 37. Environment and Shadowing

```pulsar id="h3t7b0"
define value = 10;

func outer() {
    define value = 20;

    func inner() {
        define value = 30;

        return value;
    }

    return inner();
}

show(outer());
```

The innermost `value` is the one found by the inner function.

Conceptually:

```text
Inner Environment
└── value → 30

Outer Environment
└── value → 20

Global Environment
└── value → 10
```

---

# 38. Environment and Mutation

```pulsar id="n8f4j6"
define counter = 0;

func increment() {
    counter++;
}

increment();
increment();

show(counter);
```

The function can update the existing outer binding.

The supplied scope examples establish the same behavior with assignment. 

---

# 39. Environment and Functions as Values

Pulsar functions can themselves be represented as values.

```pulsar id="u4w3zs"
define double = x => x * 2;

show(double(10));
```

The variable `double` is an environment binding referring to a function value.

Conceptually:

```text
Environment
└── double ───────┐
                  v
               Function
```

---

# 40. Environment and Callbacks

```pulsar id="2k1q5v"
define values = [
    1,
    2,
    3
];

define doubled = map(
    values,
    x => x * 2
);

show(doubled);
```

The arrow function is stored as a function value and passed to `map`.

The supplied examples explicitly use arrow functions as callbacks for `map`, `filter`, and `reduce`. 

---

# 41. Environment Lifecycle

A simplified function-call lifecycle is:

```text
Function definition
        |
        v
Function value stores surrounding environment
        |
        v
Function call
        |
        v
Create call environment
        |
        v
Define parameters
        |
        v
Execute function body
        |
        v
Return result
        |
        v
Call completes
```

The supplied evaluator implements the function environment creation and parameter binding steps. 

---

# 42. Environment Tree

A larger program can be visualized as:

```text
Global Environment
│
├── products
├── cart
├── findProduct
│
├── addProduct
│     │
│     └── Call Environment
│
└── checkout
      │
      └── Call Environment
            │
            └── calculateDiscount
                  │
                  └── Call Environment
```

Each execution context can have access to its surrounding environment.

---

# 43. Complete Environment Example

```pulsar id="v5h0h2"
define taxRate = 0.10;

func calculateTax(price) {
    define tax = price * taxRate;

    return tax;
}

func calculateTotal(price) {
    define tax = calculateTax(price);
    define total = price + tax;

    return total;
}

show(calculateTotal(100));
```

Conceptually:

```text
Global Environment
└── taxRate → 0.10
       |
       ├── calculateTax
       │       |
       │       └── Call Environment
       │             ├── price
       │             └── tax
       |
       └── calculateTotal
               |
               └── Call Environment
                     ├── price
                     ├── tax
                     └── total
```

---

# 44. Environment Rules

The demonstrated Pulsar implementation establishes these core rules:

1. Variables are stored in environments.
2. Functions execute with a function environment.
3. Function parameters are defined in that environment.
4. The function environment has access to its surrounding environment.
5. Functions can read outer variables.
6. Existing outer variables can be modified through assignment.
7. Local declarations can shadow outer variables.
8. Nested functions can access surrounding values.
9. Arrow functions also use an environment for their parameters and execution.
10. Loop execution has environment handling as well.

These behaviors are demonstrated by the supplied interpreter and examples.   

---

# 45. Recommended Environment Tests

```text
1. Global variable lookup
2. Multiple global variables
3. Function parameter binding
4. Function local variable
5. Function reading global variable
6. Function modifying global variable
7. Local variable shadowing
8. Nested function
9. Nested function reading outer parameter
10. Nested function reading outer local variable
11. Nested function reading global variable
12. Three-level environment chain
13. Arrow function parameter environment
14. Arrow function reading outer variable
15. Arrow function shadowing
16. Function returning an outer value
17. Function returning a local value
18. Function modifying an outer object
19. Standard for-loop environment
20. For-in environment
21. Nested loops
22. Function calling another function
23. Function calling nested function
24. Callback environment
25. map with arrow function
26. filter with arrow function
27. reduce with arrow function
28. Scope shadowing in nested functions
29. Scope mutation
30. Complete multi-function environment test
```

---

# 46. Environment Summary

Pulsar's environment model can be represented simply as:

```text
Environment
│
├── Variables
├── Functions
├── Parameters
└── Parent Environment
          │
          v
     Outer Environment
          │
          v
     Global Environment
```