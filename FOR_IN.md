## 1. Overview

Pulsar provides `for ... in` for iterating over arrays and objects.

The basic syntax is:

```pulsar
for item in iterable {
    statements;
}
```

Unlike the standard `for` loop, `for ... in` does not require an initialization, condition, or update expression.

The Pulsar parser represents this syntax as a `ForInStatement`, containing:

* a loop variable
* an iterable expression
* a loop body 

---

# 2. Basic Array Iteration

```pulsar
define numbers = [
    10,
    20,
    30
];

for number in numbers {
    show(number);
}
```

Output:

```text
10
20
30
```

The supplied examples demonstrate this basic array iteration pattern. 

---

# 3. Array Values

When the iterable is an array, the loop variable receives each value in the array.

```pulsar
define names = [
    "Alice",
    "Bob",
    "Charlie"
];

for name in names {
    show(name);
}
```

Conceptually:

```text
name = "Alice"
name = "Bob"
name = "Charlie"
```

The evaluator uses:

```text
for (const value of iterable)
```

for arrays. 

---

# 4. Numbers

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

for value in values {
    show(value);
}
```

---

# 5. Strings

```pulsar
define names = [
    "Pulsar",
    "Server",
    "Language"
];

for name in names {
    show(name);
}
```

---

# 6. Processing Values

The loop variable can be used in expressions.

```pulsar
define values = [
    1,
    2,
    3
];

for value in values {
    show(value * 10);
}
```

Output:

```text
10
20
30
```

The supplied examples demonstrate processing each array value inside the loop. 

---

# 7. Conditional Filtering

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

Output:

```text
4
5
```

The supplied examples explicitly demonstrate conditional filtering inside `for ... in`. 

---

# 8. Even Numbers

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
        show(number);
    }
}
```

Output:

```text
2
4
6
```

---

# 9. Odd Numbers

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
        show(number);
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

# 10. Accumulating Values

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

Output:

```text
12
```

The supplied examples demonstrate this accumulation pattern. 

---

# 11. Building Output

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

The supplied examples demonstrate string construction using the loop variable. 

---

# 12. Object Iteration

`for ... in` also works with objects.

```pulsar
define user = {
    name: "Pulsar",
    age: 20
};

for key in user {
    show(key);
}
```

For an object, the loop variable receives property keys.

The supplied evaluator implements this with:

```text
Object.keys(iterable)
```



---

# 13. Object Keys

```pulsar
define user = {
    name: "Pulsar",
    age: 20,
    active: true
};

for key in user {
    show(key);
}
```

The loop iterates through the object's keys rather than directly yielding the property values. 

---

# 14. Another Object Example

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

Output consists of the object's property names.

The supplied examples explicitly demonstrate object-key iteration. 

---

# 15. Array vs Object

The behavior differs depending on the iterable.

### Array

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

The variable receives:

```text
10
20
30
```

### Object

```pulsar
define values = {
    a: 10,
    b: 20,
    c: 30
};

for key in values {
    show(key);
}
```

The variable receives the property keys.

The evaluator explicitly separates arrays from other objects. 

---

# 16. Object Values

The loop itself provides the key. To retrieve the corresponding value, use the key to access the object.

```pulsar
define scores = {
    math: 90,
    english: 85,
    science: 95
};

for subject in scores {
    show(scores[subject]);
}
```

This uses the object key supplied by the loop to access its corresponding property.

---

# 17. Key and Value

```pulsar
define user = {
    name: "Pulsar",
    age: 20
};

for key in user {
    show(key);
    show(user[key]);
}
```

This allows both the property name and its associated value to be processed.

---

# 18. Object Conditional Processing

```pulsar
define scores = {
    math: 90,
    english: 65,
    science: 95
};

for subject in scores {
    if scores[subject] >= 80 {
        show(subject);
    }
}
```

---

# 19. Object Value Filtering

```pulsar
define scores = {
    math: 90,
    english: 65,
    science: 95
};

for subject in scores {
    if scores[subject] >= 80 {
        show(subject + ": " + scores[subject]);
    }
}
```

---

# 20. `break`

`break` exits the current `for ... in` loop.

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

Output:

```text
1
2
3
```

The supplied examples explicitly demonstrate `break` inside `for ... in`. 

---

# 21. `continue`

`continue` skips the remainder of the current iteration.

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

Output:

```text
1
3
5
```

The supplied examples explicitly demonstrate `continue` in `for ... in`. 

---

# 22. `break` and `continue`

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

---

# 23. Search an Array

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

if found == null {
    show("Not found");
} else {
    show(found);
}
```

---

# 24. Find a Product

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

---

# 25. Process Products

```pulsar
define products = [
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

for product in products {
    show(product.name);
    show(product.price);
}
```

---

# 26. Calculate Cart Total

```pulsar
define cart = [
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

for item in cart {
    total += item.price * item.quantity;
}

show(total);
```

---

# 27. Check Stock

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
    if product.stock <= 0 {
        show(product.name + " is out of stock");
    }
}
```

---

# 28. Check Available Products

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
    if product.stock > 0 {
        show(product.name);
    }
}
```

---

# 29. Nested `for ... in`

A `for ... in` loop can be placed inside another loop.

```pulsar
define groups = [
    [1, 2, 3],
    [4, 5, 6]
];

for group in groups {
    for value in group {
        show(value);
    }
}
```

---

# 30. Nested Mixed Loops

A `for ... in` loop can also be combined with a standard `for`.

```pulsar
define groups = [
    [10, 20],
    [30, 40]
];

for group in groups {
    for (define i = 0; i < group.length; i++) {
        show(group[i]);
    }
}
```

---

# 31. `for ... in` Inside a Function

```pulsar
func sum(values) {
    define total = 0;

    for value in values {
        total += value;
    }

    return total;
}

define values = [
    10,
    20,
    30
];

show(sum(values));
```

---

# 32. Function Search

```pulsar
func contains(values, target) {
    for value in values {
        if value == target {
            return true;
        }
    }

    return false;
}

define values = [
    10,
    20,
    30
];

show(contains(values, 20));
```

---

# 33. Function Finding an Object

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
        name: "Mouse"
    }
];

define product = findProduct(products, 2);

if product == null {
    show("Not found");
} else {
    show(product.name);
}
```

---

# 34. Object Configuration

```pulsar
define config = {
    host: "localhost",
    port: 8080,
    mode: "development"
};

for key in config {
    show(key + ": " + config[key]);
}
```

---

# 35. Validate Object Properties

```pulsar
define user = {
    name: "Pulsar",
    email: "user@example.com",
    age: 20
};

for key in user {
    if user[key] == null {
        show(key + " is missing");
    }
}
```

---

# 36. Count Array Values

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

# 37. Count Matching Values

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5,
    6
];

define count = 0;

for value in values {
    if value % 2 == 0 {
        count++;
    }
}

show(count);
```

---

# 38. Calculate an Average

```pulsar
define scores = [
    80,
    90,
    100
];

define total = 0;
define count = 0;

for score in scores {
    total += score;
    count++;
}

define average = total / count;

show(average);
```

---

# 39. Find the Maximum

```pulsar
define values = [
    10,
    50,
    20,
    40
];

define maximum = values[0];

for value in values {
    if value > maximum {
        maximum = value;
    }
}

show(maximum);
```

---

# 40. Find the Minimum

```pulsar
define values = [
    10,
    50,
    20,
    40
];

define minimum = values[0];

for value in values {
    if value < minimum {
        minimum = value;
    }
}

show(minimum);
```

---

# 41. Iterate and Transform

```pulsar
define values = [
    1,
    2,
    3,
    4
];

for value in values {
    show(value * value);
}
```

---

# 42. Iterate With a Function

```pulsar
func double(value) {
    return value * 2;
}

define values = [
    1,
    2,
    3
];

for value in values {
    show(double(value));
}
```

---

# 43. Iterate Through User Data

```pulsar
define users = [
    {
        name: "Alice",
        active: true
    },
    {
        name: "Bob",
        active: false
    }
];

for user in users {
    if user.active {
        show(user.name);
    }
}
```

---

# 44. Iterate Through Orders

```pulsar
define orders = [
    {
        id: 1,
        total: 100
    },
    {
        id: 2,
        total: 500
    },
    {
        id: 3,
        total: 250
    }
];

for order in orders {
    if order.total >= 300 {
        show(order.id);
    }
}
```

---

# 45. Iterate Through Messages

```pulsar
define messages = [
    "Hello",
    "Welcome",
    "Goodbye"
];

for message in messages {
    show(message);
}
```

---

# 46. Iterate Through Configuration

```pulsar
define settings = {
    debug: true,
    port: 8080,
    host: "localhost"
};

for key in settings {
    show(key);
}
```

---

# 47. Invalid Iterable

`for ... in` requires an object-like iterable.

```pulsar
define value = 123;

for item in value {
    show(item);
}
```

The evaluator checks:

```text
iterable == null || typeof iterable !== "object"
```

and raises:

```text
Cannot iterate over non-iterable
```

when the value cannot be iterated. 

---

# 48. `null` Iterable

```pulsar
define values = null;

for value in values {
    show(value);
}
```

This is invalid because `null` is rejected before iteration begins. 

---

# 49. Loop Variable

The loop variable is introduced by the `for ... in` statement.

```pulsar
define values = [
    10,
    20
];

for value in values {
    show(value);
}
```

Conceptually:

```text
first iteration → value = 10
second iteration → value = 20
```

The evaluator obtains the variable name from `node.variable` and defines it in the loop environment. 

---

# 50. Complete Example

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

for product in products {
    if product.stock > 0 {
        show(product.name);
        show("Price: " + product.price);

        total += product.price;
    }
}

show("Total: " + total);
```

---

# 51. Execution Model

For an array:

```pulsar
for value in values {
    statements;
}
```

Pulsar effectively performs:

```text
evaluate values
       ↓
check iterable
       ↓
take first array value
       ↓
define loop variable
       ↓
execute body
       ↓
take next value
       ↓
define loop variable
       ↓
execute body
       ↓
...
       ↓
finish
```

The evaluator implements array iteration with `for ... of`. 

For an object:

```pulsar
for key in object {
    statements;
}
```

the evaluator obtains the object's keys and iterates those keys. 

---

# 52. Syntax Reference

## Array

```pulsar
for value in array {
    statements;
}
```

## Object

```pulsar
for key in object {
    statements;
}
```

## With `if`

```pulsar
for value in values {
    if condition {
        statements;
    }
}
```

## With `break`

```pulsar
for value in values {
    if condition {
        break;
    }
}
```

## With `continue`

```pulsar
for value in values {
    if condition {
        continue;
    }
}
```

## Nested

```pulsar
for group in groups {
    for value in group {
        statements;
    }
}
```

---

# 53. Standard `for` vs `for ... in`

### Standard `for`

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

Best suited to counter-controlled iteration.

### `for ... in`

```pulsar
for value in values {
    show(value);
}
```

Best suited to directly iterating an existing array or object.

The parser and evaluator implement these as separate statement types. 

---

# 54. Recommended Tests

```text
1. Basic array iteration
2. Numeric array
3. String array
4. Empty array
5. Single-value array
6. Array calculation
7. Array filtering
8. Even values
9. Odd values
10. Array accumulation
11. Object keys
12. Object values through keys
13. Object filtering
14. Object configuration
15. Object validation
16. break
17. continue
18. break + continue
19. Nested for-in
20. Mixed for + for-in
21. Search array
22. Find product
23. Calculate total
24. Count values
25. Count matching values
26. Maximum
27. Minimum
28. Average
29. Function with for-in
30. Invalid iterable
```