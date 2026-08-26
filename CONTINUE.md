## 1. Overview

Pulsar provides the `continue` statement for skipping the remainder of the current loop iteration and continuing with the next iteration.

The basic syntax is:

```pulsar
continue;
```

`continue` is a loop-control statement. It does not return a value.

It can be used inside loop bodies such as:

* `while`
* `for`
* `for ... in`

The supplied Pulsar examples explicitly demonstrate `continue` inside `while` and `for ... in` loops, including its combination with `break`.  

---

# 2. Basic `continue`

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

Output:

```text
1
2
4
5
```

When `i` becomes `3`, `continue` skips the `show(i)` statement and starts the next iteration.

---

# 3. `continue` in `while`

```pulsar
define i = 0;

while i < 10 {
    i++;

    if i == 5 {
        continue;
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
6
7
8
9
10
```

The supplied examples demonstrate this form of `continue` in a `while` loop. 

---

# 4. `continue` in `for`

```pulsar
for (define i = 0; i < 10; i++) {
    if i == 5 {
        continue;
    }

    show(i);
}
```

The iteration where `i == 5` is skipped.

---

# 5. `continue` in `for ... in`

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    if value == 3 {
        continue;
    }

    show(value);
}
```

Output:

```text
1
2
4
5
```

The supplied Pulsar examples demonstrate `continue` inside `for ... in`. 

---

# 6. Skip Even Numbers

```pulsar
define numbers = [
    1,
    2,
    3,
    4,
    5,
    6
];

for number in numbers {
    if number % 2 == 0 {
        continue;
    }

    show(number);
}
```

Output:

```text
1
3
5
```

---

# 7. Skip Odd Numbers

```pulsar
define numbers = [
    1,
    2,
    3,
    4,
    5,
    6
];

for number in numbers {
    if number % 2 != 0 {
        continue;
    }

    show(number);
}
```

Output:

```text
2
4
6
```

---

# 8. Skip Negative Values

```pulsar
define values = [
    10,
    -5,
    20,
    -3,
    30
];

for value in values {
    if value < 0 {
        continue;
    }

    show(value);
}
```

Output:

```text
10
20
30
```

---

# 9. Skip Zero

```pulsar
define values = [
    10,
    0,
    20,
    0,
    30
];

for value in values {
    if value == 0 {
        continue;
    }

    show(value);
}
```

---

# 10. Skip Values Below a Limit

```pulsar
define values = [
    5,
    15,
    25,
    35
];

for value in values {
    if value < 20 {
        continue;
    }

    show(value);
}
```

Output:

```text
25
35
```

---

# 11. `continue` With `if`

The most common pattern is:

```pulsar
for value in values {
    if condition {
        continue;
    }

    statements;
}
```

For example:

```pulsar
define values = [
    10,
    20,
    30,
    40
];

for value in values {
    if value == 20 {
        continue;
    }

    show(value);
}
```

---

# 12. Multiple `continue` Conditions

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5,
    6
];

for value in values {
    if value == 2 {
        continue;
    }

    if value == 5 {
        continue;
    }

    show(value);
}
```

Output:

```text
1
3
4
6
```

---

# 13. `continue` With `break`

`continue` and `break` have different effects.

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

# 14. Skip Then Stop

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5,
    6
];

for value in values {
    if value % 2 == 0 {
        continue;
    }

    if value > 4 {
        break;
    }

    show(value);
}
```

Output:

```text
1
3
```

Here:

* even numbers are skipped
* the loop stops when an odd number greater than `4` is reached

---

# 15. `continue` in a Search

```pulsar
define values = [
    10,
    20,
    30,
    40
];

for value in values {
    if value < 20 {
        continue;
    }

    if value == 30 {
        show("Found");
        break;
    }
}
```

Output:

```text
Found
```

---

# 16. Processing Products

```pulsar
define products = [
    {
        name: "Laptop",
        stock: 5
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

for product in products {
    if product.stock == 0 {
        continue;
    }

    show(product.name);
}
```

Output:

```text
Laptop
Mouse
```

---

# 17. Skip Out-of-Stock Products

```pulsar
define products = [
    {
        name: "Laptop",
        price: 1200,
        stock: 5
    },
    {
        name: "Keyboard",
        price: 80,
        stock: 0
    },
    {
        name: "Mouse",
        price: 40,
        stock: 20
    }
];

for product in products {
    if product.stock <= 0 {
        continue;
    }

    show(product.name);
    show(product.price);
}
```

---

# 18. Calculate Available Stock

```pulsar
define products = [
    {
        name: "Laptop",
        stock: 5
    },
    {
        name: "Keyboard",
        stock: 0
    },
    {
        name: "Mouse",
        stock: 20
    }
];

define totalStock = 0;

for product in products {
    if product.stock <= 0 {
        continue;
    }

    totalStock += product.stock;
}

show(totalStock);
```

Output:

```text
25
```

---

# 19. Skip Invalid Cart Items

```pulsar
define cart = [
    {
        price: 100,
        quantity: 2
    },
    {
        price: 50,
        quantity: 0
    },
    {
        price: 20,
        quantity: 3
    }
];

define total = 0;

for item in cart {
    if item.quantity <= 0 {
        continue;
    }

    total += item.price * item.quantity;
}

show(total);
```

---

# 20. Skip Expensive Products

```pulsar
define products = [
    {
        name: "Mouse",
        price: 40
    },
    {
        name: "Keyboard",
        price: 80
    },
    {
        name: "Laptop",
        price: 1200
    }
];

for product in products {
    if product.price > 100 {
        continue;
    }

    show(product.name);
}
```

Output:

```text
Mouse
Keyboard
```

---

# 21. `continue` With `while`

```pulsar
define i = 0;

while i < 10 {
    i++;

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

---

# 22. Important `while` Pattern

When using `continue` in a `while` loop, make sure the loop's controlling variable is updated before the `continue`.

Correct:

```pulsar
define i = 0;

while i < 10 {
    i++;

    if i == 5 {
        continue;
    }

    show(i);
}
```

The increment happens before `continue`, so the loop can progress.

---

# 23. Skipping a Range

```pulsar
define i = 0;

while i < 20 {
    i++;

    if i >= 5 and i <= 10 {
        continue;
    }

    show(i);
}
```

This skips values from `5` through `10`.

---

# 24. Skip Multiples

```pulsar
define i = 1;

while i <= 20 {
    if i % 3 == 0 {
        i++;
        continue;
    }

    show(i);
    i++;
}
```

Output:

```text
1
2
4
5
7
8
10
11
13
14
16
17
19
20
```

---

# 25. Skip Empty Values

```pulsar
define values = [
    "Pulsar",
    "",
    "Language",
    "",
    "Server"
];

for value in values {
    if value == "" {
        continue;
    }

    show(value);
}
```

---

# 26. Skip Specific Names

```pulsar
define names = [
    "Alice",
    "Bob",
    "Charlie",
    "David"
];

for name in names {
    if name == "Bob" {
        continue;
    }

    show(name);
}
```

Output:

```text
Alice
Charlie
David
```

---

# 27. Skip Inactive Users

```pulsar
define users = [
    {
        name: "Alice",
        active: true
    },
    {
        name: "Bob",
        active: false
    },
    {
        name: "Charlie",
        active: true
    }
];

for user in users {
    if !user.active {
        continue;
    }

    show(user.name);
}
```

---

# 28. Skip Failed Orders

```pulsar
define orders = [
    {
        id: 1,
        status: "paid"
    },
    {
        id: 2,
        status: "failed"
    },
    {
        id: 3,
        status: "paid"
    }
];

for order in orders {
    if order.status == "failed" {
        continue;
    }

    show(order.id);
}
```

---

# 29. Continue Inside a Function

```pulsar
func showPositive(values) {
    for value in values {
        if value <= 0 {
            continue;
        }

        show(value);
    }
}

define values = [
    -10,
    10,
    -20,
    20
];

showPositive(values);
```

Output:

```text
10
20
```

---

# 30. Continue While Calculating

```pulsar
define values = [
    10,
    -5,
    20,
    -10,
    30
];

define total = 0;

for value in values {
    if value < 0 {
        continue;
    }

    total += value;
}

show(total);
```

Output:

```text
60
```

---

# 31. Continue With Nested Loops

```pulsar
define groups = [
    [1, 2, 3],
    [4, 5, 6]
];

for group in groups {
    for value in group {
        if value % 2 == 0 {
            continue;
        }

        show(value);
    }
}
```

Output:

```text
1
3
5
```

---

# 32. Continue Only Affects the Current Loop

```pulsar
define groups = [
    [1, 2],
    [3, 4]
];

for group in groups {
    for value in group {
        if value == 2 {
            continue;
        }

        show(value);
    }
}
```

The `continue` applies to the loop in which the statement occurs.

---

# 33. Continue With Object Keys

```pulsar
define settings = {
    host: "localhost",
    debug: true,
    port: 8080
};

for key in settings {
    if key == "debug" {
        continue;
    }

    show(key);
}
```

---

# 34. Continue With Object Values

```pulsar
define scores = {
    math: 90,
    english: 50,
    science: 95
};

for subject in scores {
    if scores[subject] < 80 {
        continue;
    }

    show(subject);
}
```

---

# 35. Continue During Validation

```pulsar
define values = [
    10,
    null,
    20,
    null,
    30
];

for value in values {
    if value == null {
        continue;
    }

    show(value);
}
```

---

# 36. Continue Before Processing

```pulsar
define values = [
    1,
    2,
    3,
    4
];

for value in values {
    if value == 2 {
        continue;
    }

    show("Processing: " + value);
}
```

---

# 37. Continue After Processing

```pulsar
define values = [
    1,
    2,
    3
];

for value in values {
    show("Checking: " + value);

    if value == 2 {
        continue;
    }

    show("Accepted: " + value);
}
```

Output:

```text
Checking: 1
Accepted: 1
Checking: 2
Checking: 3
Accepted: 3
```

---

# 38. Continue and Loop Update

For a standard `for` loop:

```pulsar
for (define i = 0; i < 5; i++) {
    if i == 2 {
        continue;
    }

    show(i);
}
```

The loop's update expression still executes when `continue` is encountered.

This makes `continue` particularly useful in counter-controlled `for` loops.

---

# 39. Continue vs Break

### `continue`

```pulsar
if condition {
    continue;
}
```

Means:

```text
skip this iteration
```

### `break`

```pulsar
if condition {
    break;
}
```

Means:

```text
stop the loop
```

Example:

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    if value == 2 {
        continue;
    }

    if value == 5 {
        break;
    }

    show(value);
}
```

Output:

```text
1
3
4
```

---

# 40. Continue vs Return

`continue` affects the loop.

`return` affects the function.

```pulsar
func process(values) {
    for value in values {
        if value < 0 {
            continue;
        }

        if value == 100 {
            return value;
        }

        show(value);
    }

    return null;
}
```

Here:

* negative values are skipped
* `100` exits the function
* other values continue normally

---

# 41. Complete Example

```pulsar
define products = [
    {
        name: "Laptop",
        price: 1200,
        stock: 5
    },
    {
        name: "Keyboard",
        price: 80,
        stock: 0
    },
    {
        name: "Mouse",
        price: 40,
        stock: 20
    },
    {
        name: "Monitor",
        price: 300,
        stock: 3
    }
];

define total = 0;

for product in products {
    if product.stock <= 0 {
        continue;
    }

    total += product.price;

    show(product.name);
}

show("Total: " + total);
```

---

# 42. Execution Model

Conceptually:

```text
start loop
    ↓
evaluate condition / obtain next value
    ↓
execute loop body
    ↓
continue encountered?
    ↓
skip remaining body
    ↓
next iteration
```

The supplied evaluator handles `continue` through a `ContinueSignal`. For `for ... in`, the evaluator catches that signal and proceeds to the next iteration. 

The same loop-control mechanism is used for object iteration. 

---

# 43. Recommended Tests

```text
1. Basic continue
2. Continue in while
3. Continue in for
4. Continue in for-in
5. Skip even numbers
6. Skip odd numbers
7. Skip negative values
8. Skip zero
9. Skip values below a limit
10. Multiple continue conditions
11. Continue + break
12. Continue in nested loops
13. Continue in a function
14. Continue while calculating
15. Skip inactive users
16. Skip unavailable products
17. Skip invalid cart items
18. Skip empty strings
19. Skip object properties
20. Continue with array processing
21. Continue with while update
22. Continue with standard for update
23. Continue with function calls
24. Continue with conditional processing
25. Continue + return
```