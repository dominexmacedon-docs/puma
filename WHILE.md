## 1. Overview

Pulsar provides the `while` loop for repeatedly executing a block of code while a condition remains true.

The basic syntax is:

```pulsar
while condition {
    statements;
}
```

The supplied Pulsar examples use `while` with comparisons, variables, arithmetic updates, `break`, and `continue`. 

---

## 2. Basic `while`

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
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

This is the basic `while` pattern used by the supplied examples. 

---

## 3. Countdown

```pulsar
define i = 5;

while i > 0 {
    show(i);
    i--;
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



---

## 4. Condition

The condition is evaluated before each iteration.

```pulsar
define i = 0;

while i < 3 {
    show(i);
    i++;
}
```

Execution:

```text
i = 0 → condition true → body
i = 1 → condition true → body
i = 2 → condition true → body
i = 3 → condition false → stop
```

---

## 5. Updating the Variable

A `while` loop normally needs something inside its body to change the condition.

```pulsar
define count = 0;

while count < 10 {
    show(count);
    count++;
}
```

Without an update such as `count++`, the condition may remain true indefinitely.

---

## 6. Summing Numbers

```pulsar
define total = 0;
define i = 1;

while i <= 10 {
    total += i;
    i++;
}

show(total);
```

Output:

```text
55
```

The supplied examples use this exact accumulation pattern. 

---

## 7. Even Numbers

```pulsar
define i = 1;

while i <= 10 {
    if i % 2 == 0 {
        show(i);
    }

    i++;
}
```

Output:

```text
2
4
6
8
10
```



---

## 8. Odd Numbers

```pulsar
define i = 1;

while i <= 10 {
    if i % 2 != 0 {
        show(i);
    }

    i++;
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

## 9. Multiplication Loop

```pulsar
define n = 1;

while n < 100 {
    n *= 2;
}

show(n);
```

The supplied examples demonstrate repeatedly multiplying a value until the condition becomes false. 

---

## 10. Repeating an Action

```pulsar
define i = 0;

while i < 3 {
    show("loop");
    i++;
}
```

Output:

```text
loop
loop
loop
```



---

# 11. Truthy Conditions

A `while` condition does not have to be an explicit comparison.

```pulsar
define count = 3;

while count {
    show(count);
    count--;
}
```

The supplied examples demonstrate using the value itself as the condition. 

---

# 12. Factorial

```pulsar
define i = 1;
define product = 1;

while i <= 5 {
    product *= i;
    i++;
}

show(product);
```

Output:

```text
120
```



---

# 13. Countdown From Ten

```pulsar
define i = 10;

while i >= 1 {
    show(i);
    i--;
}
```

Output:

```text
10
9
8
7
6
5
4
3
2
1
```



---

# 14. `while true`

Pulsar supports a `while` condition containing `true`.

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

The supplied examples use this pattern to create a loop that is explicitly terminated with `break`. 

---

# 15. `break`

`break` immediately exits the current `while` loop.

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

Output:

```text
1
2
3
4
```

The supplied examples demonstrate `break` inside `while`. 

---

# 16. `continue`

`continue` skips the remainder of the current iteration.

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



---

# 17. `break` With a Condition

```pulsar
define i = 1;

while i <= 10 {
    if i > 7 {
        break;
    }

    show(i);
    i++;
}
```

Output:

```text
1
2
3
4
5
6
7
```



---

# 18. `continue` and `break` Together

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

Output:

```text
1
3
```

This combination is directly represented in the supplied test examples. 

---

# 19. Nested `while`

A `while` loop can contain another `while`.

```pulsar
define i = 1;

while i <= 3 {
    define j = 1;

    while j <= 2 {
        show(i);
        show(j);

        j++;
    }

    i++;
}
```

---

# 20. `while` Inside a Function

```pulsar
func repeatMessage(message, count) {
    define i = 0;

    while i < count {
        show(message);
        i++;
    }
}

repeatMessage("Hello", 3);
```

The supplied function examples use this exact pattern. 

---

# 21. Returning From a Function

```pulsar
func findFirst(values, target) {
    define i = 0;

    while i < values.length {
        if values[i] == target {
            return values[i];
        }

        i++;
    }

    return null;
}

define values = [
    10,
    20,
    30
];

show(findFirst(values, 20));
```

---

# 22. Array Processing

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define i = 0;
define total = 0;

while i < values.length {
    total += values[i];
    i++;
}

show(total);
```

---

# 23. Array Search

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define i = 0;
define found = false;

while i < values.length {
    if values[i] == 30 {
        found = true;
        break;
    }

    i++;
}

show(found);
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

define i = 0;
define found = null;

while i < products.length {
    if products[i].id == 2 {
        found = products[i];
        break;
    }

    i++;
}

if found == null {
    show("Not found");
} else {
    show(found.name);
}
```

---

# 25. Cart Calculation

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

define i = 0;
define total = 0;

while i < cart.length {
    total += cart[i].price * cart[i].quantity;
    i++;
}

show(total);
```

---

# 26. Input-Driven Loop

The loop condition can depend on a variable that changes during execution.

```pulsar
define count = 3;

while count > 0 {
    show(count);
    count--;
}

show("Finished");
```

---

# 27. Multiple Conditions

```pulsar
define i = 0;

while i < 20 {
    if i > 5 and i < 10 {
        show(i);
    }

    i++;
}
```

Pulsar's supplied examples use logical expressions such as `and` inside conditional expressions. 

---

# 28. Conditional Update

```pulsar
define i = 0;

while i < 10 {
    if i % 2 == 0 {
        i += 2;
    } else {
        i++;
    }

    show(i);
}
```

---

# 29. Multiple Variables

```pulsar
define a = 0;
define b = 10;

while a < b {
    show(a);

    a++;
    b--;
}
```

---

# 30. Nested Conditions

```pulsar
define i = 1;

while i <= 20 {
    if i % 2 == 0 {
        if i > 10 {
            show(i);
        }
    }

    i++;
}
```

---

# 31. Sum Until a Limit

```pulsar
define total = 0;
define i = 1;

while total < 100 {
    total += i;
    i++;
}

show(total);
```

---

# 32. Power of Two

```pulsar
define value = 1;

while value < 1000 {
    value *= 2;
}

show(value);
```

---

# 33. Countdown With a Step

```pulsar
define i = 20;

while i >= 0 {
    show(i);
    i -= 2;
}
```

---

# 34. Increment by Two

```pulsar
define i = 0;

while i <= 20 {
    show(i);
    i += 2;
}
```

---

# 35. Processing Until an Index

```pulsar
define values = [
    10,
    20,
    30,
    40,
    50
];

define i = 0;

while i < 3 {
    show(values[i]);
    i++;
}
```

---

# 36. Reverse Array Traversal

```pulsar
define values = [
    10,
    20,
    30,
    40
];

define i = values.length - 1;

while i >= 0 {
    show(values[i]);
    i--;
}
```

---

# 37. Maximum Value

```pulsar
define values = [
    10,
    50,
    20,
    40
];

define i = 1;
define maximum = values[0];

while i < values.length {
    if values[i] > maximum {
        maximum = values[i];
    }

    i++;
}

show(maximum);
```

---

# 38. Minimum Value

```pulsar
define values = [
    10,
    50,
    20,
    40
];

define i = 1;
define minimum = values[0];

while i < values.length {
    if values[i] < minimum {
        minimum = values[i];
    }

    i++;
}

show(minimum);
```

---

# 39. Count Matching Values

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5,
    6
];

define i = 0;
define count = 0;

while i < values.length {
    if values[i] % 2 == 0 {
        count++;
    }

    i++;
}

show(count);
```

---

# 40. Average

```pulsar
define values = [
    10,
    20,
    30
];

define i = 0;
define total = 0;

while i < values.length {
    total += values[i];
    i++;
}

define average = total / values.length;

show(average);
```

---

# 41. `while` With Strings

```pulsar
define count = 3;

while count > 0 {
    show("Pulsar");
    count--;
}
```

---

# 42. `while` With Objects

```pulsar
define user = {
    name: "Pulsar",
    score: 0
};

while user.score < 5 {
    user.score++;
}

show(user.score);
```

---

# 43. `while` With Function Calls

```pulsar
func double(value) {
    return value * 2;
}

define value = 1;

while value < 100 {
    value = double(value);
}

show(value);
```

---

# 44. Early Exit

```pulsar
define i = 0;

while i < 100 {
    i++;

    if i == 10 {
        break;
    }
}

show(i);
```

---

# 45. Skip Specific Values

```pulsar
define i = 0;

while i < 10 {
    i++;

    if i == 3 {
        continue;
    }

    if i == 7 {
        continue;
    }

    show(i);
}
```

---

# 46. Infinite Loop With `break`

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

The supplied examples explicitly use `while true` with `break`. 

---

# 47. `while` With `null`

```pulsar
define value = null;

while value {
    show(value);
}
```

The supplied examples establish truthy/falsy-style conditions through constructs such as `while count`, but the source does not separately document the exact truthiness rules for every Pulsar value. 

---

# 48. Loop Variable Outside

```pulsar
define i = 0;

while i < 5 {
    i++;
}

show(i);
```

This allows the final counter value to be used after the loop.

---

# 49. Complete Search Example

```pulsar
define users = [
    {
        id: 1,
        name: "Alice"
    },
    {
        id: 2,
        name: "Bob"
    },
    {
        id: 3,
        name: "Charlie"
    }
];

define i = 0;
define found = null;

while i < users.length {
    if users[i].id == 2 {
        found = users[i];
        break;
    }

    i++;
}

if found == null {
    show("User not found");
} else {
    show(found.name);
}
```

---

# 50. Complete Example

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
        stock: 10
    },
    {
        name: "Mouse",
        price: 40,
        stock: 20
    }
];

define i = 0;
define total = 0;

while i < products.length {
    define product = products[i];

    if product.stock > 0 {
        total += product.price;
        show(product.name);
    }

    i++;
}

show("Total: " + total);
```

---

# 51. `while` vs Standard `for`

A `while` loop:

```pulsar
define i = 0;

while i < 10 {
    show(i);
    i++;
}
```

A standard `for` loop:

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

Both can implement counter-based repetition, but `while` keeps initialization and updating outside the loop declaration.

The supplied examples use both forms as separate language features. 

---

# 52. Recommended `while` Tests

```text
1. Basic while
2. Countdown
3. Counting upward
4. Counting downward
5. Sum numbers
6. Even numbers
7. Odd numbers
8. Multiplication
9. Factorial
10. Truthy condition
11. while true
12. break
13. continue
14. break + continue
15. Nested while
16. while inside function
17. Array traversal
18. Reverse array traversal
19. Array search
20. Product search
21. Cart calculation
22. Maximum
23. Minimum
24. Average
25. Count matching values
26. Multiple conditions
27. Conditional update
28. Multiple variables
29. Early exit
30. Infinite loop with break
```