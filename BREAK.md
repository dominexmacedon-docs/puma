## 1. Overview

Pulsar provides the `break` statement for immediately terminating the current loop.

The basic syntax is:

```pulsar
break;
```

`break` can be used inside loop bodies such as `while`, `for`, and `for ... in`.

When Pulsar encounters `break`, execution leaves the current loop and continues with the statement immediately after that loop.

---

## 2. Basic `break`

```pulsar
define i = 0;

while i < 10 {
    if i == 5 {
        break;
    }

    show(i);
    i++;
}

show("Finished");
```

Output:

```text
0
1
2
3
4
Finished
```

---

## 3. `break` in `while`

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

The loop stops as soon as `i` reaches `5`.

The supplied Pulsar examples demonstrate `break` inside `while`. 

---

## 4. `break` With `while true`

A common pattern is an intentionally open-ended loop that terminates using `break`.

```pulsar
define i = 0;

while true {
    i++;

    if i == 5 {
        break;
    }

    show(i);
}
```

Output:

```text
1
2
3
4
```

The supplied examples explicitly use `while true` together with `break`. 

---

## 5. `break` in `for`

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

---

## 6. `break` in `for ... in`

```pulsar
define values = [
    10,
    20,
    30,
    40,
    50
];

for value in values {
    if value == 30 {
        break;
    }

    show(value);
}
```

Output:

```text
10
20
```

The supplied examples demonstrate `break` inside `for ... in`. 

---

## 7. Search With `break`

`break` is useful when searching for the first matching value.

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define found = null;

for value in values {
    if value == 30 {
        found = value;
        break;
    }
}

show(found);
```

Output:

```text
30
```

---

## 8. Search for a Product

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

for product in products {
    if product.id == 2 {
        found = product;
        break;
    }
}

if found == null {
    show("Product not found");
} else {
    show(found.name);
}
```

Output:

```text
Keyboard
```

---

## 9. Search With `while`

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define i = 0;
define found = null;

while i < values.length {
    if values[i] == 30 {
        found = values[i];
        break;
    }

    i++;
}

show(found);
```

---

## 10. Stop at a Limit

```pulsar
define i = 1;

while i <= 100 {
    if i > 10 {
        break;
    }

    show(i);
    i++;
}
```

This lets the loop have a broad condition while using `break` for an additional stopping condition.

---

## 11. `break` Inside `if`

`break` is normally placed inside a conditional.

```pulsar
define i = 0;

while i < 20 {
    if i == 7 {
        break;
    }

    show(i);
    i++;
}
```

The `if` determines when the loop should terminate.

---

## 12. `break` After Processing

```pulsar
define i = 0;

while i < 10 {
    show(i);

    if i == 4 {
        break;
    }

    i++;
}
```

Here the current iteration performs its work before the loop terminates.

---

## 13. `break` Before Processing

```pulsar
define i = 0;

while i < 10 {
    if i == 4 {
        break;
    }

    show(i);
    i++;
}
```

Here the value that triggers the condition is not processed.

Output:

```text
0
1
2
3
```

---

## 14. `break` With `continue`

Both statements can appear in the same loop.

```pulsar
define i = 0;

while i < 10 {
    i++;

    if i == 3 {
        continue;
    }

    if i == 7 {
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
```

The supplied examples explicitly test `continue` followed by `break`. 

---

## 15. Skip Then Stop

```pulsar
define i = 0;

while i < 10 {
    i++;

    if i % 2 == 0 {
        continue;
    }

    if i > 7 {
        break;
    }

    show(i);
}
```

This demonstrates the distinction:

* `continue` skips an iteration.
* `break` terminates the loop.

---

## 16. `break` Inside a Function

```pulsar
func find(values, target) {
    define result = null;

    for value in values {
        if value == target {
            result = value;
            break;
        }
    }

    return result;
}

define values = [
    10,
    20,
    30
];

show(find(values, 20));
```

`break` terminates the loop; `return` terminates the function.

---

## 17. Find the First Matching Value

```pulsar
define values = [
    5,
    12,
    8,
    20,
    12
];

define found = null;

for value in values {
    if value == 12 {
        found = value;
        break;
    }
}

show(found);
```

The loop stops at the first matching value.

---

## 18. Find the First Large Number

```pulsar
define values = [
    10,
    20,
    30,
    80,
    100
];

define found = null;

for value in values {
    if value >= 50 {
        found = value;
        break;
    }
}

show(found);
```

Output:

```text
80
```

---

## 19. Find the First Available Product

```pulsar
define products = [
    {
        name: "Laptop",
        stock: 0
    },
    {
        name: "Keyboard",
        stock: 0
    },
    {
        name: "Mouse",
        stock: 10
    }
];

define available = null;

for product in products {
    if product.stock > 0 {
        available = product;
        break;
    }
}

if available == null {
    show("No products available");
} else {
    show(available.name);
}
```

---

## 20. Stop Processing a Cart

```pulsar
define cart = [
    {
        name: "Laptop",
        price: 1200
    },
    {
        name: "Keyboard",
        price: 80
    },
    {
        name: "Mouse",
        price: 40
    }
];

define total = 0;

for item in cart {
    if total >= 1000 {
        break;
    }

    total += item.price;
}

show(total);
```

---

## 21. Nested Loops

`break` terminates the current loop in which it executes.

```pulsar
define groups = [
    [1, 2, 3],
    [4, 5, 6]
];

for group in groups {
    for value in group {
        if value == 5 {
            break;
        }

        show(value);
    }
}
```

The `break` terminates the inner loop.

---

## 22. Nested `while`

```pulsar
define i = 1;

while i <= 3 {
    define j = 1;

    while j <= 5 {
        if j == 3 {
            break;
        }

        show(j);
        j++;
    }

    i++;
}
```

The inner `while` stops when `j == 3`, while the outer loop continues.

---

## 23. Break From a Search

```pulsar
define names = [
    "Alice",
    "Bob",
    "Charlie",
    "David"
];

define found = false;

for name in names {
    if name == "Charlie" {
        found = true;
        break;
    }
}

if found {
    show("Found");
} else {
    show("Not found");
}
```

---

## 24. Break From a Calculation

```pulsar
define total = 0;
define i = 1;

while true {
    total += i;

    if total >= 100 {
        break;
    }

    i++;
}

show(total);
```

The loop stops when the accumulated total reaches the required threshold.

---

## 25. Break With Multiple Conditions

```pulsar
define i = 0;

while i < 100 {
    if i > 10 and i % 2 == 0 {
        break;
    }

    show(i);
    i++;
}
```

---

## 26. Break After a Function Call

```pulsar
func isValid(value) {
    return value > 50;
}

define values = [
    10,
    20,
    70,
    90
];

for value in values {
    if isValid(value) {
        show(value);
        break;
    }
}
```

Output:

```text
70
```

---

## 27. Break in a Product Lookup

```pulsar
func findProduct(products, id) {
    for product in products {
        if product.id == id {
            return product;
        }
    }

    return null;
}

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

define product = findProduct(products, 3);

if product == null {
    show("Not found");
} else {
    show(product.name);
}
```

The `return` exits the function directly, while the underlying loop can use `break` when a result is stored first.

---

## 28. Break With an Index

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define i = 0;

while i < values.length {
    if values[i] == 30 {
        break;
    }

    i++;
}

show(i);
```

Output:

```text
2
```

---

## 29. Break After Three Items

```pulsar
define values = [
    10,
    20,
    30,
    40,
    50
];

define count = 0;

for value in values {
    show(value);

    count++;

    if count == 3 {
        break;
    }
}
```

Output:

```text
10
20
30
```

---

## 30. Break When Stock Is Found

```pulsar
define products = [
    {
        name: "Laptop",
        stock: 0
    },
    {
        name: "Keyboard",
        stock: 5
    },
    {
        name: "Mouse",
        stock: 20
    }
];

for product in products {
    if product.stock > 0 {
        show(product.name);
        break;
    }
}
```

Output:

```text
Keyboard
```

---

# 31. Behavior

Conceptually, a loop containing `break` behaves like:

```text
start loop
    ↓
evaluate condition
    ↓
execute body
    ↓
break encountered?
   / \
 yes  no
 ↓     ↓
exit   next iteration
loop
```

For the supplied evaluator, loop control is handled through a `BreakSignal`. When the evaluator catches that signal inside a loop, it exits the loop rather than treating the signal as a normal runtime error. 

The same mechanism is used for `for ... in` loops. 

---

# 32. `break` Is Not a Value

`break` is a control-flow statement.

Correct:

```pulsar
while true {
    break;
}
```

It should not be used as an expression:

```pulsar
define x = break;
```

The supplied language structure treats `break` separately from ordinary expressions and statements.

---

# 33. `break` Terminates the Current Loop

Consider:

```pulsar
define i = 0;

while i < 10 {
    if i == 3 {
        break;
    }

    i++;
}

show("After loop");
```

The execution is:

```text
i = 0
i = 1
i = 2
i = 3
break
After loop
```

The statement after the loop is executed normally.

---

# 34. `break` vs `continue`

| Statement  | Effect                            |
| ---------- | --------------------------------- |
| `break`    | Terminates the current loop       |
| `continue` | Skips the current iteration       |
| `return`   | Returns from the current function |

Example:

```pulsar
define i = 0;

while i < 10 {
    i++;

    if i == 3 {
        continue;
    }

    if i == 7 {
        break;
    }

    show(i);
}
```

---

# 35. Recommended Tests

```text
1. Basic break
2. Break in while
3. Break in for
4. Break in for-in
5. Break with if
6. Break with while true
7. Break after processing
8. Break before processing
9. Break + continue
10. Search array
11. Search object array
12. Find product
13. Find first matching value
14. Find first large number
15. Find available product
16. Stop after N items
17. Break with index
18. Break inside function
19. Break in nested loop
20. Break in nested while
21. Break with multiple conditions
22. Break after calculation
23. Break after function call
24. Break with cart processing
25. Break with stock checking
```