## 1. Overview

Conditionals allow a Pulsar program to execute different code depending on whether a condition is true.

The primary conditional syntax is:

```pulsar
if condition {
    // code
}
```

Pulsar also supports:

* `else`
* `else if`
* comparison expressions
* logical conditions
* nested conditionals
* conditions involving variables, expressions, objects, arrays, and `null`

The supplied examples explicitly include all of these basic conditional patterns. 

---

## 2. Basic `if`

```pulsar
if true {
    show("Condition is true");
}
```

---

## 3. Variable Condition

```pulsar
define active = true;

if active {
    show("Active");
}
```

---

## 4. `if` With Comparison

```pulsar
define age = 20;

if age >= 18 {
    show("adult");
}
```

This pattern is directly demonstrated in the supplied examples. 

---

## 5. `if` and `else`

Use `else` when another block should execute if the condition is false.

```pulsar
define age = 20;

if age >= 18 {
    show("adult");
} else {
    show("minor");
}
```

The supplied examples explicitly demonstrate this syntax. 

---

## 6. Simple Boolean Decision

```pulsar
define loggedIn = true;

if loggedIn {
    show("Welcome");
} else {
    show("Please log in");
}
```

---

## 7. `else if`

Multiple conditions can be tested sequentially.

```pulsar
define score = 85;

if score >= 90 {
    show("A");
} else if score >= 80 {
    show("B");
} else {
    show("C");
}
```

This exact conditional structure is present in the supplied examples. 

---

## 8. Multiple `else if` Branches

```pulsar
define score = 72;

if score >= 90 {
    show("A");
} else if score >= 80 {
    show("B");
} else if score >= 70 {
    show("C");
} else if score >= 60 {
    show("D");
} else {
    show("F");
}
```

---

## 9. Equality Condition

```pulsar
define name = "Puma";

if name == "Puma" {
    show("matched");
}
```

The supplied examples explicitly demonstrate equality inside an `if`. 

---

## 10. Inequality Condition

```pulsar
define value = 10;

if value != 20 {
    show("Values are different");
}
```

---

## 11. Greater Than

```pulsar
define score = 95;

if score > 90 {
    show("High score");
}
```

---

## 12. Greater Than or Equal

```pulsar
define age = 18;

if age >= 18 {
    show("Allowed");
}
```

---

## 13. Less Than

```pulsar
define temperature = 15;

if temperature < 20 {
    show("Cold");
}
```

---

## 14. Less Than or Equal

```pulsar
define age = 17;

if age <= 17 {
    show("Under 18");
}
```

---

## 15. Arithmetic Expression in a Condition

```pulsar
define n = 12;

if n % 2 == 0 {
    show("even");
} else {
    show("odd");
}
```

This exact pattern appears in the supplied examples. 

---

## 16. Logical `and`

Pulsar supports combining conditions with `and`.

```pulsar
define a = 10;
define b = 20;

if a < b and b > 15 {
    show("both conditions are true");
}
```

The supplied examples explicitly demonstrate this form. 

---

## 17. Multiple `and` Conditions

```pulsar
define age = 25;
define active = true;

if age >= 18 and active {
    show("Active adult");
}
```

---

## 18. Logical `or`

```pulsar
define day = "Saturday";

if day == "Saturday" or day == "Sunday" {
    show("Weekend");
}
```

---

## 19. Combining `and` and `or`

```pulsar
define age = 20;
define student = true;

if age < 18 or age >= 18 and student {
    show("Condition matched");
}
```

When writing complex conditions, use parentheses when the intended grouping needs to be explicit.

---

## 20. Parenthesized Condition

```pulsar
define age = 20;
define active = true;

if (age >= 18 and active) {
    show("Active adult");
}
```

---

## 21. `null` Condition

A condition can explicitly test for `null`.

```pulsar
define value = null;

if value == null {
    show("empty");
} else {
    show("not empty");
}
```

This exact pattern is included in the supplied examples. 

---

## 22. Non-Null Condition

```pulsar
define value = "Pulsar";

if value != null {
    show("Value exists");
}
```

---

## 23. Temperature Example

```pulsar
define temperature = 30;

if temperature > 35 {
    show("hot");
} else if temperature >= 20 {
    show("warm");
} else {
    show("cold");
}
```

This exact multi-branch pattern is included in the supplied examples. 

---

## 24. Nested `if`

An `if` can contain another `if`.

```pulsar
define age = 20;
define active = true;

if age >= 18 {
    if active {
        show("Active adult");
    }
}
```

---

## 25. Nested `if` With `else`

```pulsar
define age = 20;
define active = false;

if age >= 18 {
    if active {
        show("Active adult");
    } else {
        show("Inactive adult");
    }
} else {
    show("Minor");
}
```

---

## 26. Conditional Inside a Function

```pulsar
func maxValue(a, b) {
    if a > b {
        return a;
    }

    return b;
}

show(maxValue(10, 20));
```

The supplied examples explicitly use `if` inside a function. 

---

## 27. Function With Multiple Branches

```pulsar
func grade(score) {
    if score >= 90 {
        return "A";
    } else if score >= 80 {
        return "B";
    } else if score >= 70 {
        return "C";
    }

    return "F";
}

show(grade(85));
```

---

## 28. Conditional Return

```pulsar
func isAdult(age) {
    if age >= 18 {
        return true;
    }

    return false;
}

show(isAdult(20));
```

---

## 29. Recursive Conditional

Conditionals can form the stopping condition of recursive functions.

```pulsar
func factorial(n) {
    if n <= 1 {
        return 1;
    }

    return n * factorial(n - 1);
}

show(factorial(5));
```

The supplied examples explicitly use this conditional recursion pattern. 

---

## 30. Conditional Inside a `while`

```pulsar
define i = 1;

while i <= 10 {
    if i % 2 == 0 {
        show(i);
    }

    i++;
}
```

The supplied examples explicitly demonstrate conditionals inside `while` loops. 

---

## 31. Conditional Inside a `for`

```pulsar
for (define i = 1; i <= 10; i++) {
    if i % 2 == 0 {
        show(i);
    }
}
```

---

## 32. Conditional Inside `for ... in`

```pulsar
define numbers = [
    1,
    2,
    3,
    4,
    5
];

for number in numbers {
    if number > 3 {
        show(number);
    }
}
```

---

## 33. Object Property Condition

```pulsar
define user = {
    name: "Pulsar",
    active: true
};

if user.active {
    show(user.name);
}
```

---

## 34. Object Property Comparison

```pulsar
define user = {
    age: 20
};

if user.age >= 18 {
    show("Adult");
}
```

---

## 35. Object Property With `null`

```pulsar
define user = {
    email: null
};

if user.email == null {
    show("Email is missing");
}
```

---

## 36. Array Length Condition

```pulsar
define values = [
    10,
    20,
    30
];

if values.length > 0 {
    show("Array contains values");
}
```

---

## 37. Empty Array Condition

```pulsar
define values = [];

if isEmpty(values) {
    show("Empty");
} else {
    show("Not empty");
}
```

---

## 38. String Condition

```pulsar
define name = "Pulsar";

if name == "Pulsar" {
    show("Correct name");
}
```

---

## 39. String Comparison With `else`

```pulsar
define command = "start";

if command == "start" {
    show("Starting");
} else {
    show("Unknown command");
}
```

---

## 40. Compound Business Rule

```pulsar
define age = 25;
define verified = true;
define active = true;

if age >= 18 and verified and active {
    show("Account accepted");
} else {
    show("Account rejected");
}
```

---

# Conditional Expressions

## 41. Ternary Operator

The supplied Pulsar examples include ternary expressions as a separate language feature.

```pulsar
define age = 20;

define result =
    age >= 18 ? "adult" : "minor";

show(result);
```

The examples collection identifies ternary expressions together with nullish expressions as a supported feature category. 

---

## 42. Ternary With Numbers

```pulsar
define a = 10;
define b = 20;

define max =
    a > b ? a : b;

show(max);
```

---

## 43. Ternary With Boolean Values

```pulsar
define active = true;

define status =
    active ? "active" : "inactive";

show(status);
```

---

## 44. Ternary With Object Properties

```pulsar
define user = {
    active: true
};

define status =
    user.active
        ? "Online"
        : "Offline";

show(status);
```

---

## 45. Ternary With `null`

```pulsar
define value = null;

define result =
    value == null
        ? "Missing"
        : "Available";

show(result);
```

---

# Conditional Logic Patterns

## 46. Grade Classification

```pulsar
define score = 87;

if score >= 90 {
    show("A");
} else if score >= 80 {
    show("B");
} else if score >= 70 {
    show("C");
} else if score >= 60 {
    show("D");
} else {
    show("F");
}
```

---

## 47. Age Classification

```pulsar
define age = 25;

if age < 13 {
    show("Child");
} else if age < 18 {
    show("Teen");
} else {
    show("Adult");
}
```

---

## 48. Number Classification

```pulsar
define number = -5;

if number > 0 {
    show("Positive");
} else if number < 0 {
    show("Negative");
} else {
    show("Zero");
}
```

---

## 49. Even or Odd

```pulsar
define number = 42;

if number % 2 == 0 {
    show("Even");
} else {
    show("Odd");
}
```

---

## 50. Login Check

```pulsar
define loggedIn = true;

if loggedIn {
    show("Dashboard");
} else {
    show("Login required");
}
```

---

## 51. Permission Check

```pulsar
define role = "admin";

if role == "admin" {
    show("Full access");
} else if role == "user" {
    show("Normal access");
} else {
    show("No access");
}
```

---

## 52. Inventory Check

```pulsar
define stock = 5;

if stock <= 0 {
    show("Out of stock");
} else if stock < 5 {
    show("Low stock");
} else {
    show("In stock");
}
```

---

## 53. Price Discount

```pulsar
define price = 1200;

if price >= 1000 {
    show("15% discount");
} else if price >= 500 {
    show("10% discount");
} else if price >= 200 {
    show("5% discount");
} else {
    show("No discount");
}
```

---

## 54. Multiple Requirements

```pulsar
define age = 25;
define verified = true;

if age >= 18 and verified {
    show("Accepted");
} else {
    show("Rejected");
}
```

---

## 55. Alternative Requirements

```pulsar
define role = "admin";
define owner = false;

if role == "admin" or owner {
    show("Access granted");
} else {
    show("Access denied");
}
```

---

# Conditional Control Flow

## 56. `return` From a Conditional

```pulsar
func check(value) {
    if value == null {
        return "Missing";
    }

    return "Available";
}

show(check(null));
```

---

## 57. `break` From a Conditional

```pulsar
define numbers = [
    1,
    2,
    3,
    4,
    5
];

for number in numbers {
    if number == 3 {
        break;
    }

    show(number);
}
```

---

## 58. `continue` From a Conditional

```pulsar
define numbers = [
    1,
    2,
    3,
    4,
    5
];

for number in numbers {
    if number == 3 {
        continue;
    }

    show(number);
}
```

---

## 59. Conditional With Assignment

```pulsar
define score = 50;

if score < 60 {
    score += 10;
}

show(score);
```

---

## 60. Conditional State Update

```pulsar
define user = {
    active: false
};

if user.active == false {
    user.active = true;
}

show(user.active);
```

---

# Conditional Syntax Reference

## 61. Basic Form

```pulsar
if condition {
    statements;
}
```

---

## 62. `if / else`

```pulsar
if condition {
    statements;
} else {
    statements;
}
```

---

## 63. `if / else if / else`

```pulsar
if condition1 {
    statements;
} else if condition2 {
    statements;
} else {
    statements;
}
```

---

## 64. Nested Conditional

```pulsar
if condition1 {
    if condition2 {
        statements;
    }
}
```

---

## 65. Ternary

```pulsar
define result =
    condition
        ? valueIfTrue
        : valueIfFalse;
```

---

# Conditional Operators

## 66. Comparison Operators

The supplied examples use these comparison operators inside conditions:

```text
==
!=
<
<=
>
>=
```

For example:

```pulsar
define a = 10;
define b = 20;

if a < b {
    show("a is smaller");
}
```

The comparison examples in the supplied collection explicitly demonstrate `==`, `!=`, `<`, and `<=`; the conditional examples demonstrate `>=` and related comparisons.  

---

## 67. Logical Operators

The supplied conditional examples use:

```text
and
or
```

For example:

```pulsar
if a < b and b > 15 {
    show("Both are true");
}
```

The `and` form is directly demonstrated in the supplied examples. 

---

## 68. Nullish Operator in Conditional Expressions

Pulsar also supports `??` as a nullish operator.

```pulsar
define value = null;

define result =
    value ?? "default";

show(result);
```

The supplied interpreter documentation groups nullish expressions with ternary expressions. 

---

# Complete Example

## 69. User Access System

```pulsar
define user = {
    name: "Pulsar",
    age: 20,
    verified: true,
    active: true
};

if user.age < 18 {
    show("Too young");
} else if user.verified == false {
    show("Account not verified");
} else if user.active == false {
    show("Account inactive");
} else {
    show("Access granted");
}
```

---

## 70. Shop Decision

```pulsar
define price = 850;
define stock = 10;
define quantity = 2;

if stock <= 0 {
    show("Out of stock");
} else if quantity <= 0 {
    show("Invalid quantity");
} else if quantity > stock {
    show("Insufficient stock");
} else if price >= 1000 {
    show("Large purchase discount");
} else if price >= 500 {
    show("Standard discount");
} else {
    show("No discount");
}
```

---

# Recommended Conditional Tests

Use these to test the Pulsar interpreter:

```text
1. Basic if
2. if with true
3. if with false
4. if / else
5. else if
6. Multiple else if branches
7. Equality
8. Inequality
9. Greater than
10. Greater than or equal
11. Less than
12. Less than or equal
13. Arithmetic condition
14. and
15. or
16. Combined logical conditions
17. Parenthesized conditions
18. null comparison
19. Non-null comparison
20. String comparison
21. Object property condition
22. Array length condition
23. Nested if
24. Nested if / else
25. Conditional inside function
26. Conditional return
27. Recursive conditional
28. Conditional inside while
29. Conditional inside for
30. Conditional inside for-in
31. break inside conditional
32. continue inside conditional
33. Conditional assignment
34. Ternary expression
35. Ternary with numbers
36. Ternary with strings
37. Ternary with booleans
38. Ternary with null
39. Nullish fallback
40. Multi-branch business logic
```