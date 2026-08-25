## 1. Overview

Booleans represent logical values in Pulsar.

Pulsar has two boolean values:

```pulsar
true
```

and

```pulsar
false
```

The supplied examples explicitly demonstrate both values as standalone values and inside objects and arrays. 

---

# 2. `true`

`true` represents a true logical value.

```pulsar
define active = true;

show(active);
```

The supplied examples use this exact boolean-value pattern. 

---

# 3. `false`

`false` represents a false logical value.

```pulsar
define active = false;

show(active);
```

The supplied examples explicitly demonstrate `false`. 

---

# 4. Boolean Literals

Boolean values can be used directly.

```pulsar
show(true);
```

```pulsar
show(false);
```

---

# 5. Boolean Variables

Booleans can be stored in variables.

```pulsar
define loggedIn = true;

show(loggedIn);
```

Another example:

```pulsar
define enabled = false;

show(enabled);
```

---

# 6. Boolean Reassignment

A boolean variable can be reassigned.

```pulsar
define active = false;

active = true;

show(active);
```

And:

```pulsar
define active = true;

active = false;

show(active);
```

---

# 7. Boolean Equality

Booleans can be compared using `==`.

```pulsar
show(true == true);
```

```pulsar
show(false == false);
```

```pulsar
show(true == false);
```

---

# 8. Boolean Inequality

The `!=` operator can be used with boolean values.

```pulsar
show(true != false);
```

```pulsar
show(false != false);
```

The supplied comparison examples establish `==` and `!=` as equality operators in Pulsar. 

---

# 9. Booleans in `if`

A boolean can directly control an `if` statement.

```pulsar
define active = true;

if active {
    show("Active");
}
```

The evaluator explicitly converts an `if` test to a boolean before selecting the branch. 

---

# 10. Boolean `false` in `if`

```pulsar
define active = false;

if active {
    show("Active");
} else {
    show("Inactive");
}
```

Because the condition is `false`, the `else` branch is selected.

---

# 11. Boolean Conditions

A function can return a boolean.

```pulsar
func isReady() {
    return true;
}

if isReady() {
    show("Ready");
}
```

The supplied examples also demonstrate functions returning `true`. 

---

# 12. Boolean Functions

```pulsar
func isAdult(age) {
    return age >= 18;
}

show(isAdult(20));
```

This produces a boolean result from a numeric comparison.

---

# 13. Even Number Test

```pulsar
func isEven(value) {
    return value % 2 == 0;
}

show(isEven(8));
```

The supplied examples explicitly demonstrate a function returning the result of a numeric equality comparison. 

---

# 14. Boolean Results From Comparisons

Comparison expressions produce values that can be used as conditions.

```pulsar
define score = 80;

define passed = score >= 50;

show(passed);
```

---

# 15. Less-Than Boolean Expression

```pulsar
define result = 5 < 10;

show(result);
```

---

# 16. Greater-Than Boolean Expression

```pulsar
define result = 10 > 5;

show(result);
```

---

# 17. Less-Than-or-Equal Boolean Expression

```pulsar
define result = 10 <= 10;

show(result);
```

---

# 18. Greater-Than-or-Equal Boolean Expression

```pulsar
define result = 10 >= 10;

show(result);
```

The supplied comparison section explicitly tests `<`, `<=`, `>`, and `>=`. 

---

# 19. Logical `and`

Pulsar supports logical expressions using `and`.

```pulsar
define age = 20;

define valid =
    age >= 18 and age < 100;

show(valid);
```

Logical expressions are part of the supplied comparison-and-logic examples.

---

# 20. `and` With Booleans

```pulsar
show(true and true);
```

```pulsar
show(true and false);
```

```pulsar
show(false and true);
```

```pulsar
show(false and false);
```

The important property of `and` is that both conditions must evaluate truthily for the complete expression to be true.

---

# 21. `and` With Comparisons

```pulsar
define score = 85;

if score >= 50 and score <= 100 {
    show("Valid score");
}
```

---

# 22. Multiple `and` Conditions

```pulsar
define age = 25;
define active = true;

if age >= 18 and age < 100 and active {
    show("Accepted");
}
```

---

# 23. Logical `or`

The supplied Pulsar comparison/logic feature set includes logical alternatives.

A typical form is:

```pulsar
define admin = false;
define owner = true;

if admin or owner {
    show("Access granted");
}
```

Use the logical operator spelling implemented by the current interpreter.

---

# 24. Boolean `or` Logic

Conceptually:

```pulsar
true or true
```

```pulsar
true or false
```

```pulsar
false or true
```

```pulsar
false or false
```

`or` succeeds when at least one side is truthy.

---

# 25. Combining `and` and `or`

```pulsar
define age = 20;
define active = true;
define admin = false;

if active and age >= 18 or admin {
    show("Allowed");
}
```

For complicated logical expressions, parentheses should be used when the intended grouping needs to be explicit.

---

# 26. Parenthesized Boolean Expressions

```pulsar
define age = 20;
define active = true;

define result =
    active and (age >= 18);

show(result);
```

Parentheses allow the expression structure to be explicit.

---

# 27. Boolean Ternary

A boolean can be used directly as the condition of a ternary expression.

```pulsar
show(true ? "yes" : "no");
```

The supplied examples explicitly demonstrate this. 

---

# 28. False Ternary

```pulsar
show(false ? "yes" : "no");
```

The `false` branch is selected. 

---

# 29. Comparison Ternary

A comparison can produce the boolean condition.

```pulsar
define age = 20;

show(age >= 18 ? "adult" : "minor");
```

The supplied examples explicitly demonstrate this pattern. 

---

# 30. Boolean Variable With Ternary

```pulsar
define active = true;

define message =
    active ? "Online" : "Offline";

show(message);
```

---

# 31. Boolean Object Property

Booleans can be stored inside objects.

```pulsar
define config = {
    debug: true,
    version: 1
};

show(config.debug);
```

The supplied object examples explicitly demonstrate a boolean `debug` property. 

---

# 32. Multiple Boolean Properties

```pulsar
define user = {
    active: true,
    verified: false,
    admin: false
};

show(user.active);
show(user.verified);
show(user.admin);
```

---

# 33. Changing a Boolean Object Property

```pulsar
define user = {
    active: false
};

user.active = true;

show(user.active);
```

---

# 34. Boolean Values in Arrays

Booleans can be elements of arrays.

```pulsar
define values = [
    true,
    false,
    true
];

show(values);
```

The supplied examples demonstrate mixed arrays containing `true` and `null` alongside other value types. 

---

# 35. Mixed Values

```pulsar
define values = [
    1,
    "two",
    true,
    null
];

show(values);
```

The supplied examples explicitly demonstrate this mixed-value structure. 

---

# 36. Boolean Array Indexing

```pulsar
define values = [
    true,
    false
];

show(values[0]);
show(values[1]);
```

---

# 37. Boolean Function Parameter

Booleans can be passed to functions.

```pulsar
func status(active) {
    if active {
        return "Active";
    }

    return "Inactive";
}

show(status(true));
show(status(false));
```

---

# 38. Boolean Return Value

```pulsar
func alwaysReady() {
    return true;
}

define ready = alwaysReady();

show(ready);
```

---

# 39. Boolean Arrow Function

A boolean can be returned from an arrow function.

```pulsar
define isPositive = x => x > 0;

show(isPositive(10));
```

The supplied arrow-function examples demonstrate boolean-returning predicates such as `isEven`. 

---

# 40. Boolean Arrow Predicate

```pulsar
define isEven =
    x => x % 2 == 0;

show(isEven(10));
```

---

# 41. Boolean With `filter`

Boolean-returning functions are useful as filtering predicates.

```pulsar
define numbers = [
    1,
    2,
    3,
    4,
    5
];

define even =
    filter(numbers, x => x % 2 == 0);

show(even);
```

The arrow function supplies the boolean decision for each value.

---

# 42. Boolean With `map`

A boolean-producing expression can also be mapped across an array.

```pulsar
define numbers = [
    1,
    2,
    3
];

define results =
    map(numbers, x => x > 1);

show(results);
```

---

# 43. Boolean in a `while`

A boolean expression controls whether a `while` loop continues.

```pulsar
define running = true;
define count = 0;

while running {
    count++;

    if count == 3 {
        running = false;
    }
}
```

The supplied evaluator converts each `while` test to a boolean before deciding whether to continue. 

---

# 44. `while true`

An unconditional loop can use `true`.

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

The supplied examples explicitly demonstrate `while true` combined with `break`. 

---

# 45. Boolean Loop State

```pulsar
define running = true;

while running {
    show("running");

    running = false;
}
```

---

# 46. Boolean With `break`

```pulsar
define running = true;
define i = 0;

while running {
    i++;

    if i >= 5 {
        running = false;
        break;
    }

    show(i);
}
```

---

# 47. Boolean With `continue`

```pulsar
define values = [
    1,
    2,
    3,
    4
];

for value in values {
    if value % 2 == 0 {
        continue;
    }

    show(value);
}
```

The supplied examples use boolean comparison results to decide whether `continue` should execute. 

---

# 48. Boolean With `null`

Boolean values and `null` are separate values.

```pulsar
define value = null;

show(value ?? "default");
```

A boolean can also be used with nullish coalescing:

```pulsar
define value = false;

show(value ?? true);
```

The supplied examples explicitly demonstrate that `false` remains the value when using `??`; it is not replaced merely because it is false. 

---

# 49. Boolean Nullish Example

```pulsar
define enabled = false;

define result =
    enabled ?? true;

show(result);
```

The important distinction is:

```text
false
```

is a boolean value, while:

```text
null
```

represents the absence of a value.

The supplied nullish examples distinguish the two. 

---

# 50. Boolean Configuration

```pulsar
define config = {
    debug: true,
    production: false,
    logging: true
};

if config.debug {
    show("Debug mode");
}
```

---

# 51. Boolean Permission

```pulsar
define user = {
    loggedIn: true,
    admin: false
};

if user.loggedIn {
    show("User is logged in");
}
```

---

# 52. Multiple Permissions

```pulsar
define user = {
    loggedIn: true,
    admin: false
};

if user.loggedIn and user.admin {
    show("Admin access");
} else {
    show("Normal access");
}
```

---

# 53. Boolean Validation

```pulsar
func validScore(score) {
    return score >= 0 and score <= 100;
}

define valid = validScore(85);

if valid {
    show("Valid score");
}
```

---

# 54. Boolean Status Function

```pulsar
func isValidAge(age) {
    return age >= 18 and age <= 100;
}

define age = 25;

if isValidAge(age) {
    show("Valid");
} else {
    show("Invalid");
}
```

---

# 55. Boolean From Multiple Comparisons

```pulsar
define score = 85;

define passed =
    score >= 50 and
    score <= 100;

show(passed);
```

---

# 56. Boolean With String Operations

String builtins can produce boolean results.

```pulsar
define name = "Pulsar";

define valid =
    startsWith(name, "Pul");

show(valid);
```

Similarly:

```pulsar
define filename = "main.pulsar";

define valid =
    endsWith(filename, ".pulsar");

show(valid);
```

These string operations are part of the supplied interpreter examples.

---

# 57. Boolean With Object Data

```pulsar
define account = {
    username: "Pulsar",
    active: true
};

if account.active {
    show("Account active");
}
```

---

# 58. Boolean in Entity Methods

The supplied entity examples demonstrate methods returning boolean values.

```pulsar
entity Admin {
    isAdmin() {
        return true;
    }
}

define admin = new Admin();

show(admin.isAdmin());
```

The supplied entity inheritance examples explicitly use `return true` from `isAdmin()`. 

---

# 59. Boolean Entity State

```pulsar
entity User {
    init(active) {
        self.active = active;
    }

    isActive() {
        return self.active;
    }
}

define user = new User(true);

show(user.isActive());
```

---

# 60. Boolean Configuration Example

```pulsar
define settings = {
    debug: true,
    logging: false,
    cache: true
};

if settings.debug {
    show("Debug enabled");
}

if settings.cache {
    show("Cache enabled");
}
```

---

# 61. Boolean Decision Function

```pulsar
func canEnter(age, hasTicket) {
    return age >= 18 and hasTicket;
}

define allowed =
    canEnter(20, true);

if allowed {
    show("Allowed");
} else {
    show("Denied");
}
```

---

# 62. Boolean State Machine

```pulsar
define running = true;
define finished = false;

if running and !finished {
    show("Program is running");
}
```

Use this form only if the current interpreter's unary logical-not syntax is enabled. The supplied evaluator materials confirm boolean coercion in conditions, but the retrieved source does not establish a separate unary `!` operator strongly enough to document it as guaranteed syntax.

---

# 63. Truthiness in Conditions

The evaluator explicitly performs boolean coercion for `if` conditions:

```javascript
test = !!test;
```

and for `while` conditions:

```javascript
test = !!test;
```

Therefore, condition evaluation is based on the runtime's truthiness behavior rather than requiring the test expression itself to literally be `true` or `false`. 

For example, the language examples commonly use comparison expressions:

```pulsar
define score = 80;

if score >= 50 {
    show("Pass");
}
```

Here `score >= 50` produces the logical result used by the condition.

---

# 64. Boolean Operator Reference

| Expression          | Purpose                          |
| ------------------- | -------------------------------- |
| `true`              | Boolean true                     |
| `false`             | Boolean false                    |
| `a == b`            | Equality comparison              |
| `a != b`            | Inequality comparison            |
| `a < b`             | Less-than comparison             |
| `a <= b`            | Less-than-or-equal comparison    |
| `a > b`             | Greater-than comparison          |
| `a >= b`            | Greater-than-or-equal comparison |
| `a and b`           | Logical conjunction              |
| `a or b`            | Logical alternative              |
| `condition ? a : b` | Conditional expression           |

The supplied examples establish `true`, `false`, comparison expressions, logical expressions, and ternary conditions as part of the language.  

---

# 65. Complete Boolean Example

```pulsar
func canAccess(user) {
    return user.active and
           user.verified and
           user.age >= 18;
}

define user = {
    active: true,
    verified: true,
    age: 21
};

define allowed = canAccess(user);

if allowed {
    show("Access granted");
} else {
    show("Access denied");
}
```

---

# 66. Boolean Feature Summary

Pulsar booleans can be used for:

```text
true
false
Boolean variables
Variable reassignment
Equality comparisons
Inequality comparisons
Numeric comparisons
Logical conditions
if / else
while loops
Ternary expressions
Function return values
Function arguments
Arrow-function predicates
Array elements
Object properties
Entity state
Entity methods
filter() predicates
map() boolean results
Nullish expressions
Configuration flags
Permission checks
Validation
Program state
```

The supplied Pulsar examples directly demonstrate `true` and `false`, boolean object properties, boolean values in mixed arrays, boolean-returning functions, boolean ternaries, boolean loop conditions, and boolean/nullish behavior.  

---

# 67. Recommended Boolean Tests

For testing the Pulsar interpreter:

```text
1. true literal
2. false literal
3. Boolean variable
4. Boolean reassignment
5. true == true
6. true == false
7. true != false
8. Numeric comparison
9. String comparison
10. Boolean if condition
11. Boolean if/else
12. and
13. or
14. Multiple logical conditions
15. Boolean function return
16. Boolean function parameter
17. Boolean arrow function
18. Boolean array value
19. Boolean object property
20. Boolean object mutation
21. Boolean while condition
22. while true
23. Boolean ternary
24. Boolean nullish expression
25. Boolean filter predicate
26. Boolean entity method
27. Boolean configuration
28. Boolean validation
29. Boolean permission check
30. Boolean state management
```

These tests stay within the boolean behavior represented by the supplied Pulsar examples and interpreter materials.
