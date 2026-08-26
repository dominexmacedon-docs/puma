## 1. Overview

Scope determines where a variable can be accessed and which environment a function uses when it executes.

Pulsar's supplied examples demonstrate:

* variables defined outside functions
* functions reading outer variables
* functions modifying outer variables
* local variables inside functions
* nested functions
* shadowing
* functions using values from their surrounding environment

The supplied interpreter implements function execution by creating a new `Environment` whose parent is the environment in which the function was created. 

---

# 2. Global Scope

A variable defined at the top level is available from the surrounding program scope.

```pulsar
define name = "Pulsar";

show(name);
```

Output:

```text
Pulsar
```

---

# 3. Function Accessing an Outer Variable

A function can read a variable defined outside the function.

```pulsar
define outside = 100;

func test() {
    return outside;
}

show(test());
```

Output:

```text
100
```

This behavior is explicitly demonstrated in the supplied examples. 

---

# 4. Another Outer-Scope Example

```pulsar
define x = 10;

func readX() {
    return x;
}

show(readX());
```

Output:

```text
10
```



---

# 5. Functions Can Modify Outer Variables

The supplied examples demonstrate that assignment can update an existing variable from an outer environment.

```pulsar
define x = 10;

func change() {
    x = 20;
}

change();

show(x);
```

Output:

```text
20
```



---

# 6. Function Local Scope

Variables created inside a function belong to that function's execution environment.

```pulsar
func calculate(value) {
    define result = value * 2;

    return result;
}

show(calculate(10));
```

Here `result` is created inside `calculate`.

---

# 7. Local Variable Example

```pulsar
func makeValue(x) {
    define y = x + 10;

    return y;
}

show(makeValue(5));
```

Output:

```text
15
```

This pattern appears directly in the supplied function-scope examples. 

---

# 8. Local Variables Do Not Replace Outer Variables Automatically

```pulsar
define message = "outer";

func test() {
    define message = "inner";

    return message;
}

show(test());
show(message);
```

Output:

```text
inner
outer
```

The inner `message` shadows the outer `message` inside the function. 

---

# 9. Variable Shadowing

Shadowing occurs when an inner scope defines a variable with the same name as a variable in an outer scope.

```pulsar
define value = 100;

func test() {
    define value = 200;

    return value;
}

show(test());
show(value);
```

The function reads its local `value`, while the outer `value` remains unchanged.

---

# 10. Function Parameters Are Local

Function parameters are placed into the function's local environment.

```pulsar
func multiply(value) {
    return value * 2;
}

show(multiply(5));
```

Here:

```text
value
```

is available inside the function.

The evaluator creates the local function environment and defines each parameter there. 

---

# 11. Parameters Can Shadow Outer Variables

```pulsar
define value = 100;

func test(value) {
    return value;
}

show(test(50));
show(value);
```

The parameter `value` is the local value inside `test`.

---

# 12. Outer Variables and Parameters

```pulsar
define base = 5;

func multiply(x) {
    return x * base;
}

show(multiply(4));
```

Output:

```text
20
```

The function receives `x` as a parameter while reading `base` from its surrounding scope. 

---

# 13. Prefix Example

```pulsar
define prefix = "Hello ";

func greet(name) {
    return prefix + name;
}

show(greet("Pulsar"));
```

Output:

```text
Hello Pulsar
```



---

# 14. Nested Functions

Pulsar supports functions declared inside another function.

```pulsar
func outer(value) {
    func inner() {
        return value * 2;
    }

    return inner();
}

show(outer(10));
```

Output:

```text
20
```

This nested-function pattern is explicitly present in the supplied examples. 

---

# 15. Nested Function Accessing the Outer Function's Parameter

```pulsar
func outer(value) {
    func inner() {
        return value + 10;
    }

    return inner();
}

show(outer(5));
```

The inner function can access `value` from the surrounding function scope.

---

# 16. Nested Scope Chain

Conceptually:

```text
Global Environment
        |
        v
   outer Environment
        |
        v
   inner Environment
```

When `inner` looks for a variable, it can use values available through its surrounding environment.

The evaluator's arrow-function implementation follows the same environment-parent pattern:

```text
new Environment(env)
```

where `env` is the environment surrounding the function. 

---

# 17. Closure Example

```pulsar
define factor = 3;

func calculate(x) {
    return x * factor + 1;
}

show(calculate(5));
```

Output:

```text
16
```

The function uses `factor` from its surrounding scope. 

---

# 18. Another Closure Example

```pulsar
define language = "Pulsar";

func identify() {
    return language;
}

show(identify());
```

Output:

```text
Pulsar
```



---

# 19. Function Scope and Closures

A closure is a function together with access to the environment surrounding it.

For example:

```pulsar
define multiplier = 10;

func multiply(value) {
    return value * multiplier;
}

show(multiply(5));
```

The function uses:

```text
value
```

from its parameter and:

```text
multiplier
```

from its surrounding environment.

---

# 20. Scope Lookup

When a function evaluates a variable, the runtime searches the current environment and its surrounding environments.

Conceptually:

```text
Current scope
     |
     v
Parent scope
     |
     v
Outer scope
     |
     v
Global scope
```

The supplied interpreter's function implementation creates a child environment from the environment captured when the function is evaluated. 

---

# 21. Local Variable Inside a Function

```pulsar
func calculate(a, b) {
    define sum = a + b;
    define product = a * b;

    return sum + product;
}

show(calculate(2, 3));
```

`sum` and `product` belong to the function's local execution environment.

---

# 22. Outer Variable Plus Local Variable

```pulsar
define base = 100;

func calculate(value) {
    define result = base + value;

    return result;
}

show(calculate(25));
```

Output:

```text
125
```

---

# 23. Local Variable Does Not Change Outer Variable

```pulsar
define value = 10;

func test() {
    define value = 20;

    show(value);
}

test();

show(value);
```

Output:

```text
20
10
```

---

# 24. Assignment Can Reach an Existing Outer Variable

```pulsar
define counter = 0;

func increment() {
    counter++;
}

increment();
increment();

show(counter);
```

Output:

```text
2
```

The supplied scope examples demonstrate the same principle using direct assignment. 

---

# 25. Function Scope With Arrays

```pulsar
define values = [
    10,
    20,
    30
];

func firstValue() {
    return values[0];
}

show(firstValue());
```

Output:

```text
10
```

---

# 26. Function Scope With Objects

```pulsar
define user = {
    name: "Pulsar"
};

func getName() {
    return user.name;
}

show(getName());
```

Output:

```text
Pulsar
```

---

# 27. Function Scope With Object Mutation

```pulsar
define user = {
    score: 10
};

func increaseScore() {
    user.score += 5;
}

increaseScore();

show(user.score);
```

Output:

```text
15
```

The supplied variable examples also demonstrate assignment to object properties. 

---

# 28. Scope Inside a Loop

Loops can contain variables used for their iteration.

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

The supplied standard `for` examples use loop-local initialization such as `define i = 0`. 

---

# 29. For-In Scope

```pulsar
define values = [
    10,
    20,
    30
];

for value in values {
    show(value);
}
```

The supplied `for-in` examples use this syntax for iterating array values. 

---

# 30. Function Containing a Loop

```pulsar
func printValues(values) {
    for value in values {
        show(value);
    }
}

printValues([
    10,
    20,
    30
]);
```

---

# 31. Function Scope With Nested Function

```pulsar
func outer(value) {
    define doubled = value * 2;

    func inner() {
        return doubled;
    }

    return inner();
}

show(outer(10));
```

The inner function can use a value belonging to the surrounding function environment.

---

# 32. Arrow Function Scope

Arrow functions also receive a local environment.

```pulsar
define factor = 10;

define multiply = x => x * factor;

show(multiply(5));
```

The evaluator explicitly creates:

```text
new Environment(env)
```

for an arrow-function invocation and defines its parameters in that environment. 

---

# 33. Arrow Function With Local Parameter

```pulsar
define double = x => x * 2;

show(double(10));
```

`x` belongs to the arrow function's invocation environment.

---

# 34. Arrow Function Reading an Outer Variable

```pulsar
define factor = 3;

define multiply = x => x * factor;

show(multiply(4));
```

Output:

```text
12
```

---

# 35. Arrow Function Shadowing

```pulsar
define value = 100;

define test = value => value * 2;

show(test(5));
show(value);
```

The arrow function's parameter named `value` is separate from the outer `value`.

---

# 36. Nested Scope Example

```pulsar
define outerValue = 10;

func outer() {
    define middleValue = 20;

    func inner() {
        return outerValue + middleValue;
    }

    return inner();
}

show(outer());
```

Output:

```text
30
```

---

# 37. Scope Does Not Mean Copying

An outer variable is not necessarily copied into the function as an independent value.

For example:

```pulsar
define x = 10;

func change() {
    x = 20;
}

change();

show(x);
```

The supplied examples demonstrate the outer value being changed through the function. 

---

# 38. Shadowing Versus Assignment

These two programs have different behavior.

### Assignment

```pulsar
define x = 10;

func change() {
    x = 20;
}

change();

show(x);
```

The existing outer variable is assigned.

### Local declaration

```pulsar
define x = 10;

func change() {
    define x = 20;

    show(x);
}

change();

show(x);
```

The function has its own local `x`.

The distinction follows the supplied examples showing both outer assignment and local shadowing.  

---

# 39. Function Scope Does Not Change the Global Scope Automatically

```pulsar
define name = "outer";

func test() {
    define name = "inner";
}

test();

show(name);
```

Output:

```text
outer
```

The local declaration does not replace the outer declaration.

---

# 40. Scope With Function Parameters

```pulsar
define multiplier = 10;

func calculate(value) {
    return value * multiplier;
}

show(calculate(4));
```

There are two different sources of variables:

```text
value       -> function parameter
multiplier  -> surrounding scope
```

---

# 41. Scope With Nested Functions

```pulsar
func create(value) {
    func getValue() {
        return value;
    }

    return getValue();
}

show(create(100));
```

The inner function can access `value` from `create`.

---

# 42. Scope Chain Example

```pulsar
define a = 1;

func outer() {
    define b = 2;

    func inner() {
        define c = 3;

        return a + b + c;
    }

    return inner();
}

show(outer());
```

Output:

```text
6
```

Conceptually:

```text
inner:
    c
    |
    v
outer:
    b
    |
    v
global:
    a
```

---

# 43. Complete Scope Example

```pulsar
define globalValue = 100;

func outer(value) {
    define localValue = 20;

    func inner() {
        return globalValue +
               value +
               localValue;
    }

    return inner();
}

show(outer(30));
```

Output:

```text
150
```

---

# 44. Scope Rules Demonstrated by the Supplied Interpreter

The supplied source establishes the following behavior:

### Global values

Top-level variables are available to functions.

```pulsar
define x = 10;

func getX() {
    return x;
}
```



### Function environments

A function receives a new environment whose parent is the surrounding environment.

```text
new Environment(env)
```



### Parameters

Parameters are defined inside that local environment.



### Outer assignment

Existing outer variables can be modified.



### Shadowing

A local declaration can hide an outer variable with the same name.



### Nested functions

Functions can be declared inside functions and access surrounding values.



---

# 45. Scope and `return`

`return` exits the current function execution.

```pulsar
func calculate(value) {
    define result = value * 2;

    return result;
}
```

The local environment is used while evaluating the function, and the returned value is passed back to the caller.

The evaluator's block execution explicitly propagates `ReturnValue` rather than treating it as an ordinary statement result. 

---

# 46. Scope and Closures

A closure-style example:

```pulsar
func createMultiplier(factor) {
    func multiply(value) {
        return value * factor;
    }

    return multiply;
}
```

The supplied examples establish nested functions accessing surrounding values, but the retrieved source does not establish a complete test showing a nested function being returned and invoked later as a persistent closure. Therefore, that pattern should be treated as a feature to test rather than assumed as a fully documented guarantee. 

---

# 47. Scope Testing Checklist

```text
1. Global variable
2. Function reading global variable
3. Function modifying global variable
4. Function parameter
5. Local variable
6. Local variable shadowing global variable
7. Multiple local variables
8. Nested function
9. Nested function reading outer parameter
10. Nested function reading outer local variable
11. Nested function reading global variable
12. Function using array from outer scope
13. Function using object from outer scope
14. Function modifying outer object
15. Function with loop-local variable
16. For-in variable
17. Arrow function parameter
18. Arrow function reading outer variable
19. Arrow function shadowing outer variable
20. Multiple nested scopes
```

---

# 48. Scope Summary

Pulsar's demonstrated scope model can be summarized as:

```text
Global Environment
       |
       +----------------------+
       |                      |
       v                      v
 Function Environment    Other Global Code
       |
       +------------------+
       |                  |
       v                  v
 Local Variables     Nested Function
                          |
                          v
                   Nested Environment
```