## 1. Overview

Pulsar provides a standard counter-based `for` loop.

The general form is:

```pulsar
for (initialization; condition; update) {
    statements;
}
```

The supplied examples identify standard `for` loops as a separate language feature, and the evaluator implements them using an initialization expression, a test expression, a loop body, and an update expression.  

---

## 2. Basic `for`

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

Output:

```text
0
1
2
3
4
```

This is the first standard `for` example in the supplied collection. 

---

## 3. Starting From One

```pulsar
for (define i = 1; i <= 5; i++) {
    show(i);
}
```

Output:

```text
1
2
3
4
5
```



---

## 4. Counting Down

```pulsar
for (define i = 5; i > 0; i--) {
    show(i);
}
```

Output:

```text
5
4
3
2
1
```

The supplied examples explicitly include a decreasing `for` loop. 

---

# 5. The Three Parts

A standard Pulsar `for` contains three expressions:

```pulsar
for (initialization; condition; update) {
    statements;
}
```

### Initialization

Runs once before the loop begins.

```pulsar
define i = 0;
```

### Condition

Runs before every iteration.

```pulsar
i < 5;
```

### Update

Runs after each iteration.

```pulsar
i++;
```

Together:

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

The evaluator creates a local environment, evaluates `node.init`, repeatedly evaluates `node.test`, evaluates the body, and then evaluates `node.update`. 

---

# 6. Execution Order

For:

```pulsar
for (define i = 0; i < 3; i++) {
    show(i);
}
```

the execution order is conceptually:

```text
define i = 0
       ↓
   i < 3 ?
       ↓
   show(i)
       ↓
      i++
       ↓
   i < 3 ?
       ↓
   show(i)
       ↓
      i++
       ↓
   i < 3 ?
       ↓
   show(i)
       ↓
      i++
       ↓
   i < 3 ?
       ↓
     stop
```

---

# 7. Summing Numbers

```pulsar
define total = 0;

for (define i = 1; i <= 10; i++) {
    total += i;
}

show(total);
```

Output:

```text
55
```

This pattern is directly included in the supplied examples. 

---

# 8. Even Numbers

```pulsar
for (define i = 0; i < 10; i++) {
    if i % 2 == 0 {
        show(i);
    }
}
```

Output:

```text
0
2
4
6
8
```



---

# 9. Odd Numbers

```pulsar
for (define i = 1; i <= 10; i++) {
    if i % 2 != 0 {
        show(i);
    }
}
```

Output:

```text
1
3
5
7
9
```



---

# 10. Custom Increment

The update expression can use a value other than `1`.

```pulsar
for (define i = 2; i <= 20; i += 2) {
    show(i);
}
```

Output:

```text
2
4
6
8
10
12
14
16
18
20
```

The supplied examples explicitly demonstrate this form. 

---

# 11. Custom Decrement

```pulsar
for (define i = 10; i >= 0; i -= 2) {
    show(i);
}
```

Output:

```text
10
8
6
4
2
0
```

---

# 12. Multiplication

```pulsar
define result = 1;

for (define i = 1; i <= 5; i++) {
    result *= i;
}

show(result);
```

Output:

```text
120
```

---

# 13. Factorial

```pulsar
define factorial = 1;

for (define i = 1; i <= 5; i++) {
    factorial *= i;
}

show(factorial);
```

---

# 14. Nested `for`

A standard `for` can contain another `for`.

```pulsar
for (define i = 1; i <= 3; i++) {
    for (define j = 1; j <= 3; j++) {
        show(i * j);
    }
}
```

---

# 15. Nested Counter Example

```pulsar
for (define i = 1; i <= 3; i++) {
    show("Outer: " + i);

    for (define j = 1; j <= 2; j++) {
        show("Inner: " + j);
    }
}
```

---

# 16. `if` Inside `for`

```pulsar
for (define i = 1; i <= 10; i++) {
    if i > 5 {
        show(i);
    }
}
```

The supplied examples use conditional expressions inside loops. 

---

# 17. Multiple Conditions

```pulsar
for (define i = 1; i <= 20; i++) {
    if i > 5 and i < 15 {
        show(i);
    }
}
```

---

# 18. Searching With `for`

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define found = false;

for (define i = 0; i < values.length; i++) {
    if values[i] == 30 {
        found = true;
        break;
    }
}

show(found);
```

---

# 19. Accessing Array Elements

```pulsar
define values = [
    10,
    20,
    30
];

for (define i = 0; i < values.length; i++) {
    show(values[i]);
}
```

The supplied examples demonstrate array indexing such as `values[2]` and array mutation. 

---

# 20. Modifying Array Values

```pulsar
define values = [
    1,
    2,
    3
];

for (define i = 0; i < values.length; i++) {
    values[i] *= 2;
}

show(values);
```

---

# 21. Building a Total From an Array

```pulsar
define prices = [
    100,
    200,
    300
];

define total = 0;

for (define i = 0; i < prices.length; i++) {
    total += prices[i];
}

show(total);
```

---

# 22. Building a New Result

```pulsar
define values = [
    1,
    2,
    3,
    4
];

define total = 0;

for (define i = 0; i < values.length; i++) {
    total += values[i] * 2;
}

show(total);
```

---

# 23. `break`

`break` stops the current `for` loop immediately.

```pulsar
for (define i = 0; i < 10; i++) {
    if i == 5 {
        break;
    }

    show(i);
}
```

Output:

```text
0
1
2
3
4
```

The evaluator catches `BreakSignal` and exits the loop. 

---

# 24. `continue`

`continue` skips the rest of the current iteration.

```pulsar
for (define i = 0; i < 10; i++) {
    if i % 2 == 0 {
        continue;
    }

    show(i);
}
```

Output:

```text
1
3
5
7
9
```

The evaluator explicitly evaluates the update expression when `continue` is encountered in a standard `for`. 

---

# 25. `break` and `continue`

```pulsar
for (define i = 1; i <= 10; i++) {
    if i == 3 {
        continue;
    }

    if i == 8 {
        break;
    }

    show(i);
}
```

Output:

```text
1
2
4
5
6
7
```

---

# 26. `continue` With Custom Update

```pulsar
for (define i = 0; i < 20; i += 2) {
    if i == 10 {
        continue;
    }

    show(i);
}
```

---

# 27. Empty Initialization

The evaluator allows the initialization expression to be absent.

```pulsar
define i = 0;

for (; i < 5; i++) {
    show(i);
}
```

The evaluator checks `node.init` before evaluating it, so an absent initializer is supported by the runtime implementation. 

---

# 28. Empty Update

The update expression can also be absent.

```pulsar
define i = 0;

for (; i < 5;) {
    show(i);
    i++;
}
```

The evaluator checks `node.update` before evaluating it. 

---

# 29. Empty Condition

The evaluator also permits an absent test:

```pulsar
for (define i = 0; ; i++) {
    show(i);

    if i == 4 {
        break;
    }
}
```

Because the evaluator uses:

```text
!node.test || evaluate(node.test)
```

an absent test does not stop the loop; `break` is therefore needed to terminate it. 

---

# 30. Infinite `for`

```pulsar
for (;;) {
    show("running");

    break;
}
```

This relies on the evaluator's support for an absent test and terminates through `break`. 

---

# 31. Loop Variable

A common pattern is to define the counter directly inside the `for`.

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

The standard loop receives its own local environment in the evaluator. 

---

# 32. Counter Outside the Loop

The counter can also be defined before the loop.

```pulsar
define i = 0;

for (; i < 5; i++) {
    show(i);
}
```

---

# 33. Updating Multiple Variables

A loop update can contain an expression supported by Pulsar.

```pulsar
define i = 0;
define total = 0;

for (; i < 5; i++) {
    total += i;
}

show(total);
```

---

# 34. `for` Inside a Function

```pulsar
func sumTo(n) {
    define total = 0;

    for (define i = 1; i <= n; i++) {
        total += i;
    }

    return total;
}

show(sumTo(10));
```

---

# 35. Function With `for` and `break`

```pulsar
func findValue(values, target) {
    for (define i = 0; i < values.length; i++) {
        if values[i] == target {
            return i;
        }
    }

    return -1;
}

define values = [
    10,
    20,
    30
];

show(findValue(values, 20));
```

---

# 36. Product Search

```pulsar
define products = [
    {
        id: 1,
        name: "Laptop"
    },
    {
        id: 2,
        name: "Keyboard"
    },
    {
        id: 3,
        name: "Mouse"
    }
];

define found = null;

for (define i = 0; i < products.length; i++) {
    if products[i].id == 2 {
        found = products[i];
        break;
    }
}

if found == null {
    show("Product not found");
} else {
    show(found.name);
}
```

---

# 37. Shop Total

```pulsar
define products = [
    {
        price: 1200,
        quantity: 1
    },
    {
        price: 80,
        quantity: 2
    },
    {
        price: 40,
        quantity: 3
    }
];

define total = 0;

for (define i = 0; i < products.length; i++) {
    total += products[i].price * products[i].quantity;
}

show(total);
```

---

# 38. Discount Calculation

```pulsar
define prices = [
    100,
    250,
    500
];

define total = 0;

for (define i = 0; i < prices.length; i++) {
    total += prices[i];
}

if total >= 1000 {
    show("15% discount");
} else if total >= 500 {
    show("10% discount");
} else if total >= 200 {
    show("5% discount");
} else {
    show("No discount");
}
```

---

# 39. Nested Product Data

```pulsar
define stores = [
    [
        100,
        200
    ],
    [
        300,
        400
    ]
];

define total = 0;

for (define i = 0; i < stores.length; i++) {
    for (define j = 0; j < stores[i].length; j++) {
        total += stores[i][j];
    }
}

show(total);
```

---

# 40. Complete Example

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

define total = 0;

for (define i = 0; i < products.length; i++) {
    define product = products[i];

    if product.stock > 0 {
        total += product.price;
        show(product.name);
    }
}

show("Total: " + total);
```

---

# Standard `for` vs `for ... in`

A standard `for` is counter-based:

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

A `for ... in` loop iterates an iterable directly:

```pulsar
define values = [10, 20, 30];

for value in values {
    show(value);
}
```

The standard `for` uses `init`, `test`, `body`, and `update`, while `ForInStatement` has a variable, iterable, and body. 

---

# Syntax Reference

## Basic

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

## Increment

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

## Decrement

```pulsar
for (define i = 10; i > 0; i--) {
    show(i);
}
```

## Custom Increment

```pulsar
for (define i = 0; i <= 20; i += 2) {
    show(i);
}
```

## Custom Decrement

```pulsar
for (define i = 20; i >= 0; i -= 2) {
    show(i);
}
```

## With `break`

```pulsar
for (define i = 0; i < 10; i++) {
    if i == 5 {
        break;
    }
}
```

## With `continue`

```pulsar
for (define i = 0; i < 10; i++) {
    if i % 2 == 0 {
        continue;
    }

    show(i);
}
```

---

# Recommended Tests

```text
1. Basic for
2. for starting at 1
3. Countdown
4. Custom increment
5. Custom decrement
6. Sum numbers
7. Product numbers
8. Even numbers
9. Odd numbers
10. if inside for
11. Multiple conditions
12. Array indexing
13. Array modification
14. Array total
15. Search array
16. break
17. continue
18. break + continue
19. Nested for
20. for inside function
21. for with return
22. Empty initialization
23. Empty update
24. Empty condition
25. Infinite for with break
26. Product search
27. Shop calculation
28. Discount calculation
29. Nested arrays
30. Complete business loop
```