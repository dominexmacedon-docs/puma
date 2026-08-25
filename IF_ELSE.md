## 1. Overview

Pulsar uses `if`, `else if`, and `else` to control which block of code executes based on a condition.

The basic structure is:

```pulsar
if condition {
    // statements
} else {
    // statements
}
```

The supplied Pulsar examples use this structure for comparisons, grading, classification, `null` checks, and other decisions. 

---

## 2. Basic `if`

```pulsar
define age = 20;

if age >= 18 {
    show("adult");
}
```

If `age >= 18` is true, the body executes.

---

## 3. `if` With `else`

```pulsar
define age = 16;

if age >= 18 {
    show("adult");
} else {
    show("minor");
}
```

Only one of the two branches executes.

The supplied examples explicitly demonstrate this pattern. 

---

## 4. `else if`

Use `else if` when there are multiple possible conditions.

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

The supplied examples explicitly demonstrate `else if`. 

---

## 5. Multiple `else if` Branches

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

The branches are checked from top to bottom.

Once a matching branch is selected, the remaining branches are skipped.

---

## 6. Equality

```pulsar
define name = "Puma";

if name == "Puma" {
    show("matched");
} else {
    show("not matched");
}
```

Equality comparisons are used directly in the supplied conditional examples. 

---

## 7. Inequality

```pulsar
define value = 10;

if value != 20 {
    show("different");
} else {
    show("same");
}
```

---

## 8. Greater Than

```pulsar
define score = 95;

if score > 90 {
    show("high");
} else {
    show("normal");
}
```

---

## 9. Greater Than or Equal

```pulsar
define age = 18;

if age >= 18 {
    show("adult");
} else {
    show("minor");
}
```

---

## 10. Less Than

```pulsar
define temperature = 15;

if temperature < 20 {
    show("cold");
} else {
    show("warm");
}
```

---

## 11. Less Than or Equal

```pulsar
define age = 17;

if age <= 17 {
    show("under 18");
} else {
    show("18 or older");
}
```

---

# Comparison-Based `if / else`

## 12. Even or Odd

```pulsar
define n = 12;

if n % 2 == 0 {
    show("even");
} else {
    show("odd");
}
```

This exact conditional pattern is included in the supplied examples. 

---

## 13. Positive, Negative, or Zero

```pulsar
define n = -5;

if n > 0 {
    show("positive");
} else if n < 0 {
    show("negative");
} else {
    show("zero");
}
```

---

## 14. Temperature Classification

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

This is directly represented in the supplied examples. 

---

## 15. Score Classification

```pulsar
define score = 95;

if score >= 90 {
    show("A");
} else {
    show("not A");
}
```

This pattern is directly included in the supplied examples. 

---

# Logical Conditions

## 16. `and`

Multiple conditions can be combined with `and`.

```pulsar
define a = 10;
define b = 20;

if a < b and b > 15 {
    show("both conditions are true");
} else {
    show("condition failed");
}
```

The supplied examples explicitly use `and` inside an `if`. 

---

## 17. Multiple `and` Conditions

```pulsar
define age = 25;
define active = true;
define verified = true;

if age >= 18 and active and verified {
    show("accepted");
} else {
    show("rejected");
}
```

---

## 18. `or`

```pulsar
define day = "Saturday";

if day == "Saturday" or day == "Sunday" {
    show("weekend");
} else {
    show("weekday");
}
```

---

## 19. Combined Conditions

```pulsar
define age = 20;
define active = true;

if age >= 18 and active {
    show("active adult");
} else {
    show("not eligible");
}
```

---

# `null` With `if / else`

## 20. Checking `null`

```pulsar
define value = null;

if value == null {
    show("empty");
} else {
    show("not empty");
}
```

This exact pattern appears in the supplied examples. 

---

## 21. Checking for a Value

```pulsar
define value = "Pulsar";

if value != null {
    show("value exists");
} else {
    show("value is missing");
}
```

---

## 22. Function Returning `null`

```pulsar
func findUser(id) {
    if id == 1 {
        return {
            name: "Pulsar"
        };
    }

    return null;
}

define user = findUser(2);

if user == null {
    show("User not found");
} else {
    show(user.name);
}
```

---

# Nested `if / else`

## 23. Basic Nested Conditional

```pulsar
define age = 20;
define active = true;

if age >= 18 {
    if active {
        show("active adult");
    } else {
        show("inactive adult");
    }
} else {
    show("minor");
}
```

---

## 24. Nested Permission Check

```pulsar
define loggedIn = true;
define admin = false;

if loggedIn {
    if admin {
        show("admin panel");
    } else {
        show("user panel");
    }
} else {
    show("login required");
}
```

---

## 25. Nested Product Check

```pulsar
define stock = 10;
define price = 500;

if stock > 0 {
    if price >= 500 {
        show("available premium product");
    } else {
        show("available product");
    }
} else {
    show("out of stock");
}
```

---

# `if / else` Inside Functions

## 26. Returning One of Two Values

```pulsar
func maxValue(a, b) {
    if a > b {
        return a;
    } else {
        return b;
    }
}

show(maxValue(10, 20));
```

The supplied examples demonstrate conditional logic inside functions. 

---

## 27. Boolean Function

```pulsar
func isAdult(age) {
    if age >= 18 {
        return true;
    } else {
        return false;
    }
}

show(isAdult(20));
```

---

## 28. Multiple Return Branches

```pulsar
func grade(score) {
    if score >= 90 {
        return "A";
    } else if score >= 80 {
        return "B";
    } else if score >= 70 {
        return "C";
    } else {
        return "F";
    }
}

show(grade(85));
```

---

# `if / else` Inside Loops

## 29. `while`

```pulsar
define i = 1;

while i <= 10 {
    if i % 2 == 0 {
        show(i);
    }

    i++;
}
```

The supplied examples demonstrate `if` inside `while`. 

---

## 30. `for`

```pulsar
for (define i = 1; i <= 10; i++) {
    if i % 2 == 0 {
        show(i);
    }
}
```

---

## 31. `for ... in`

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

# Objects and `if / else`

## 32. Object Property

```pulsar
define user = {
    active: true
};

if user.active {
    show("active");
} else {
    show("inactive");
}
```

---

## 33. Object Property Comparison

```pulsar
define user = {
    age: 20
};

if user.age >= 18 {
    show("adult");
} else {
    show("minor");
}
```

---

## 34. Object `null` Check

```pulsar
define user = {
    email: null
};

if user.email == null {
    show("email missing");
} else {
    show(user.email);
}
```

---

# Arrays and `if / else`

## 35. Array Length

```pulsar
define values = [
    10,
    20,
    30
];

if values.length > 0 {
    show("values exist");
} else {
    show("empty");
}
```

---

## 36. Array Search

```pulsar
define fruits = [
    "Apple",
    "Banana",
    "Orange"
];

if includesArr(fruits, "Banana") {
    show("found");
} else {
    show("not found");
}
```

---

# Practical Examples

## 37. Login

```pulsar
define loggedIn = true;

if loggedIn {
    show("Welcome");
} else {
    show("Please log in");
}
```

---

## 38. Account Status

```pulsar
define active = false;

if active {
    show("Account active");
} else {
    show("Account inactive");
}
```

---

## 39. Permission

```pulsar
define role = "admin";

if role == "admin" {
    show("Full access");
} else if role == "user" {
    show("Normal access");
} else {
    show("Access denied");
}
```

---

## 40. Inventory

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

## 41. Shopping Quantity

```pulsar
define stock = 10;
define quantity = 3;

if quantity <= 0 {
    show("Invalid quantity");
} else if quantity > stock {
    show("Insufficient stock");
} else {
    show("Purchase accepted");
}
```

---

## 42. Discount

```pulsar
define subtotal = 850;

if subtotal >= 1000 {
    show("15% discount");
} else if subtotal >= 500 {
    show("10% discount");
} else if subtotal >= 200 {
    show("5% discount");
} else {
    show("No discount");
}
```

---

## 43. Complete Shop Decision

```pulsar
define stock = 10;
define quantity = 2;
define subtotal = 850;

if stock <= 0 {
    show("Out of stock");
} else if quantity <= 0 {
    show("Invalid quantity");
} else if quantity > stock {
    show("Insufficient stock");
} else if subtotal >= 1000 {
    show("Purchase accepted with 15% discount");
} else if subtotal >= 500 {
    show("Purchase accepted with 10% discount");
} else if subtotal >= 200 {
    show("Purchase accepted with 5% discount");
} else {
    show("Purchase accepted without discount");
}
```

---

# Conditional Syntax Reference

## 44. `if`

```pulsar
if condition {
    statements;
}
```

## 45. `if / else`

```pulsar
if condition {
    statements;
} else {
    statements;
}
```

## 46. `if / else if / else`

```pulsar
if condition1 {
    statements;
} else if condition2 {
    statements;
} else {
    statements;
}
```

## 47. Nested `if`

```pulsar
if condition1 {
    if condition2 {
        statements;
    } else {
        statements;
    }
} else {
    statements;
}
```

---

# 48. Recommended Tests

```text
1. Basic if
2. if with true
3. if with false
4. if / else
5. else if
6. Multiple else if branches
7. ==
8. !=
9. >
10. >=
11. <
12. <=
13. Arithmetic comparison
14. and
15. or
16. Multiple logical conditions
17. null comparison
18. String comparison
19. Object property condition
20. Array condition
21. Nested if
22. Nested if / else
23. Conditional function
24. Conditional return
25. Conditional while loop
26. Conditional for loop
27. Conditional for-in loop
28. Multiple branch decision
29. Shop validation
30. Permission validation
```