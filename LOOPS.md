## 1. Overview

Pulsar provides three loop forms:

1. `while`
2. Standard `for`
3. `for ... in`

It also supports:

* `break`
* `continue`
* nested loops
* conditional logic inside loops
* loop counters and compound updates
* iterating arrays
* iterating object keys

These forms are represented directly in the supplied parser and evaluator.  

---

# 2. While Loops

A `while` loop repeatedly executes its body while its condition is truthy.

Basic syntax:

```pulsar
while condition {
    statements;
}
```

The evaluator evaluates the test before every iteration and stops when the test becomes falsy. 

---

## 3. Basic `while`

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
}
```

The supplied examples use this exact pattern. 

---

## 4. Counting Down

```pulsar
define i = 5;

while i > 0 {
    show(i);
    i--;
}
```

The supplied examples explicitly demonstrate a decreasing counter. 

---

## 5. Summing Numbers

```pulsar
define total = 0;
define i = 1;

while i <= 10 {
    total += i;
    i++;
}

show(total);
```

This pattern is included in the supplied examples. 

---

## 6. Even Numbers

```pulsar
define i = 1;

while i <= 10 {
    if i % 2 == 0 {
        show(i);
    }

    i++;
}
```

The supplied examples demonstrate filtering values inside a `while` loop. 

---

## 7. Odd Numbers

```pulsar
define i = 1;

while i <= 10 {
    if i % 2 != 0 {
        show(i);
    }

    i++;
}
```



---

## 8. Multiplication Loop

```pulsar
define n = 1;

while n < 100 {
    n *= 2;
}

show(n);
```

This pattern is included in the supplied examples. 

---

## 9. Repeated String Output

```pulsar
define i = 0;

while i < 3 {
    show("loop");
    i++;
}
```



---

## 10. Truthy `while`

The supplied examples also use a variable directly as the loop condition.

```pulsar
define count = 3;

while count {
    show(count);
    count--;
}
```



The evaluator explicitly coerces the test to a boolean. 

---

# 11. Standard `for` Loops

Pulsar supports the classic three-part `for` loop:

```pulsar
for (initialization; condition; update) {
    statements;
}
```

The parser requires parentheses around the three clauses. 

---

## 12. Basic `for`

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```



---

## 13. Starting at One

```pulsar
for (define i = 1; i <= 5; i++) {
    show(i);
}
```



---

## 14. Counting Down

```pulsar
for (define i = 5; i > 0; i--) {
    show(i);
}
```



---

## 15. Summing With `for`

```pulsar
define total = 0;

for (define i = 1; i <= 10; i++) {
    total += i;
}

show(total);
```



---

## 16. Even Numbers With `for`

```pulsar
for (define i = 0; i < 10; i++) {
    if i % 2 == 0 {
        show(i);
    }
}
```



---

## 17. Odd Numbers With `for`

```pulsar
for (define i = 1; i <= 10; i++) {
    if i % 2 != 0 {
        show(i);
    }
}
```



---

## 18. Custom Step

The update expression does not have to be `i++`.

```pulsar
for (define i = 2; i <= 20; i += 2) {
    show(i);
}
```



---

## 19. Decreasing Custom Step

```pulsar
for (define i = 10; i >= 0; i -= 2) {
    show(i);
}
```



---

## 20. Factorial With `for`

```pulsar
define product = 1;

for (define i = 1; i <= 5; i++) {
    product *= i;
}

show(product);
```



---

# 21. `for ... in`

Pulsar also provides a `for ... in` loop for iterating over arrays and objects.

Basic syntax:

```pulsar
for item in iterable {
    statements;
}
```

The parser creates a `ForInStatement` containing the loop variable, iterable, and body. 

---

## 22. Iterating an Array

```pulsar
define values = [
    10,
    20,
    30
];

for item in values {
    show(item);
}
```



---

## 23. Iterating Strings in an Array

```pulsar
define names = [
    "A",
    "B",
    "C"
];

for name in names {
    show(name);
}
```



---

## 24. Processing Each Value

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    show(value * 2);
}
```



---

## 25. Conditional `for ... in`

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    if value > 3 {
        show(value);
    }
}
```



---

## 26. Iterating Object Keys

For objects, `for ... in` iterates over property keys.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

for key in user {
    show(key);
}
```

The supplied examples demonstrate this behavior. 

The evaluator implements object iteration using `Object.keys(iterable)`. 

---

## 27. Object With Multiple Keys

```pulsar
define scores = {
    math: 90,
    english: 85,
    science: 95
};

for subject in scores {
    show(subject);
}
```



---

## 28. Processing Array Values

```pulsar
define letters = [
    "a",
    "b",
    "c"
];

for letter in letters {
    show(upper(letter));
}
```



---

## 29. Accumulating Values

```pulsar
define values = [
    2,
    4,
    6
];

define total = 0;

for value in values {
    total += value;
}

show(total);
```



---

## 30. String Construction

```pulsar
define values = [
    "one",
    "two",
    "three"
];

for value in values {
    show("value=" + value);
}
```



---

# 31. Arrays vs Objects in `for ... in`

Pulsar handles the two cases differently.

For an array:

```pulsar
for value in values {
    show(value);
}
```

the loop variable receives each array value.

For an object:

```pulsar
for key in data {
    show(key);
}
```

the loop variable receives each object key.

This distinction is implemented directly in the evaluator. 

---

# 32. Invalid `for ... in`

The evaluator requires the iterable to be an object-like value.

```pulsar
define value = 123;

for item in value {
    show(item);
}
```

This produces the runtime error:

```text
Cannot iterate over non-iterable
```

The supplied evaluator explicitly checks for `null` and non-object values before beginning a `for ... in` loop. 

---

# Break and Continue

## 33. `break`

`break` immediately stops the current loop.

```pulsar
define i = 0;

while i < 10 {
    i++;

    if i == 5 {
        break;
    }

    show(i);
}
```

The supplied examples explicitly demonstrate `break` in a `while` loop. 

---

## 34. `break` in a `for`

```pulsar
for (define i = 0; i < 10; i++) {
    if i == 4 {
        break;
    }

    show(i);
}
```



---

## 35. `break` in `for ... in`

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    if value == 4 {
        break;
    }

    show(value);
}
```



---

## 36. `continue`

`continue` skips the remainder of the current iteration and proceeds to the next iteration.

```pulsar
define i = 0;

while i < 5 {
    i++;

    if i == 3 {
        continue;
    }

    show(i);
}
```



---

## 37. `continue` in a `for`

```pulsar
for (define i = 0; i < 6; i++) {
    if i % 2 == 0 {
        continue;
    }

    show(i);
}
```



---

## 38. `continue` in `for ... in`

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    if value % 2 == 0 {
        continue;
    }

    show(value);
}
```



---

## 39. `break` and `continue` Together

```pulsar
define i = 0;

while i < 5 {
    i++;

    if i == 2 {
        continue;
    }

    if i == 4 {
        break;
    }

    show(i);
}
```

The supplied examples explicitly demonstrate both controls in the same loop. 

---

## 40. `break` Before `continue`

```pulsar
for (define i = 1; i <= 10; i++) {
    if i == 8 {
        break;
    }

    if i % 2 == 0 {
        continue;
    }

    show(i);
}
```



---

# Infinite Loops

## 41. `while true`

A `while` loop can intentionally use a truthy constant and terminate with `break`.

```pulsar
define i = 0;

while true {
    i++;

    if i == 3 {
        break;
    }

    show(i);
}
```

This exact pattern appears in the supplied examples. 

---

# Loop Scope and Evaluation

## 42. Standard `for` Environment

The evaluator creates a local environment for a standard `for` loop:

```javascript
const local = new Environment(env);
```

The initialization, test, body, and update are evaluated using that loop environment. 

Therefore, the classic loop structure is evaluated as:

```text
initialize
    ↓
test
    ↓
body
    ↓
update
    ↓
test
    ↓
body
    ↓
update
    ↓
...
```

---

## 43. Standard `for` Update Behavior

Normally:

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

performs the update after the body.

The evaluator explicitly evaluates `node.update` after the body. 

---

## 44. `continue` in Standard `for`

When `continue` occurs in a standard `for`, the evaluator still evaluates the update expression before beginning the next iteration.

```pulsar
for (define i = 0; i < 6; i++) {
    if i % 2 == 0 {
        continue;
    }

    show(i);
}
```

This behavior is explicitly implemented in `evalFor`. 

---

## 45. `break` Does Not Run the Update

When `break` is encountered, the loop exits immediately.

```pulsar
for (define i = 0; i < 10; i++) {
    if i == 4 {
        break;
    }

    show(i);
}
```

The evaluator catches `BreakSignal` and exits the loop. 

---

# Nested Loops

## 46. Nested `while`

```pulsar
define outer = 1;

while outer <= 3 {
    define inner = 1;

    while inner <= 3 {
        show(inner);
        inner++;
    }

    outer++;
}
```

---

## 47. Nested `for`

```pulsar
for (define i = 1; i <= 3; i++) {
    for (define j = 1; j <= 3; j++) {
        show(i * j);
    }
}
```

---

## 48. Nested Array Iteration

```pulsar
define groups = [
    [1, 2],
    [3, 4],
    [5, 6]
];

for group in groups {
    for value in group {
        show(value);
    }
}
```

---

# Practical Loop Examples

## 49. Search an Array

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define found = false;

for value in values {
    if value == 30 {
        found = true;
        break;
    }
}

show(found);
```

---

## 50. Find a Product

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

define found = null;

for product in products {
    if product.id == 2 {
        found = product;
        break;
    }
}

if found == null {
    show("Not found");
} else {
    show(found.name);
}
```

---

## 51. Calculate Total

```pulsar
define prices = [
    100,
    200,
    300
];

define total = 0;

for price in prices {
    total += price;
}

show(total);
```

---

## 52. Filter Values

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    if value % 2 != 0 {
        continue;
    }

    show(value);
}
```

---

## 53. Count Values

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define count = 0;

for value in values {
    count++;
}

show(count);
```

---

## 54. Object Key Processing

```pulsar
define scores = {
    math: 90,
    english: 85,
    science: 95
};

for subject in scores {
    show(subject);
}
```

The loop variable is the object's key, not its value. 

---

# Loop Syntax Reference

## 55. `while`

```pulsar
while condition {
    statements;
}
```

## 56. Standard `for`

```pulsar
for (initialization; condition; update) {
    statements;
}
```

## 57. `for ... in`

```pulsar
for item in iterable {
    statements;
}
```

## 58. `break`

```pulsar
break;
```

## 59. `continue`

```pulsar
continue;
```

The parser has dedicated `breakStatement()` and `continueStatement()` handlers. 

---

# Loop Types at a Glance

| Loop                     | Main purpose                       |
| ------------------------ | ---------------------------------- |
| `while`                  | Repeat while a condition is truthy |
| `for`                    | Counter-controlled iteration       |
| `for ... in` with array  | Iterate array values               |
| `for ... in` with object | Iterate object keys                |
| `break`                  | Exit the current loop              |
| `continue`               | Skip to the next iteration         |

---

# Recommended Loop Tests

```text
1. Basic while
2. Countdown while
3. while with arithmetic
4. while with if
5. while with true
6. Basic for
7. Reverse for
8. for with custom increment
9. for with custom decrement
10. for with compound update
11. for with if
12. Basic for-in array
13. for-in string array
14. for-in object
15. for-in with condition
16. for-in accumulation
17. break in while
18. break in for
19. break in for-in
20. continue in while
21. continue in for
22. continue in for-in
23. break and continue together
24. Infinite while with break
25. Nested while
26. Nested for
27. Nested for-in
28. Array search
29. Object-key iteration
30. Product search
```