## 1. Overview

Numbers are one of the fundamental value types in Pulsar.

They can be used for:

* arithmetic
* comparisons
* variables
* function arguments
* return values
* loop counters
* array indexes
* object properties
* calculations
* conditional expressions

Examples:

```pulsar
10
```

```pulsar
3.14
```

```pulsar
-25
```

---

# 2. Integer Numbers

An integer is a number without a fractional component.

```pulsar
define age = 20;

show(age);
```

Other examples:

```pulsar
define zero = 0;
define negative = -10;
define large = 1000000;
```

---

# 3. Decimal Numbers

Pulsar supports decimal numeric values.

```pulsar
define price = 19.99;

show(price);
```

Another example:

```pulsar
define pi = 3.14159;

show(pi);
```

Decimal values can participate in the same arithmetic expressions as other numeric values.

---

# 4. Positive Numbers

A positive number can be written normally:

```pulsar
define value = 100;
```

Unary `+` can also be used:

```pulsar
define value = +100;
```

The parser supports unary `PLUS`. 

---

# 5. Negative Numbers

Negative values can be written using unary `-`.

```pulsar
define temperature = -10;

show(temperature);
```

A variable can also be negated:

```pulsar
define value = 25;

show(-value);
```

The parser handles unary `MINUS` expressions. 

---

# 6. Zero

Zero is a normal numeric value.

```pulsar
define count = 0;

show(count);
```

It is commonly useful for counters:

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
}
```

The supplied loop examples use zero as the initial counter value. 

---

# 7. Basic Addition

The `+` operator performs addition.

```pulsar
show(10 + 20);
```

Result:

```text
30
```

The supplied examples explicitly test addition. 

---

# 8. Basic Subtraction

The `-` operator performs subtraction.

```pulsar
show(50 - 20);
```

Result:

```text
30
```

---

# 9. Basic Multiplication

The `*` operator performs multiplication.

```pulsar
show(6 * 7);
```

Result:

```text
42
```

---

# 10. Basic Division

The `/` operator performs division.

```pulsar
show(20 / 5);
```

Result:

```text
4
```

---

# 11. Remainder

The `%` operator calculates the remainder.

```pulsar
show(17 % 5);
```

Result:

```text
2
```

The supplied examples explicitly test the modulo operator. 

---

# 12. Arithmetic With Variables

Numbers can be stored and combined through variables.

```pulsar
define a = 10;
define b = 20;

define result = a + b;

show(result);
```

---

# 13. Multiple Arithmetic Operations

```pulsar
define a = 10;
define b = 5;
define c = 2;

define result = a + b * c;

show(result);
```

Multiplication has higher precedence than addition. The parser implements multiplication/division/modulo in the `factor()` level and addition/subtraction in `term()`. 

---

# 14. Parentheses

Parentheses can change the order of numeric evaluation.

```pulsar
define result = (10 + 5) * 2;

show(result);
```

Without the parentheses:

```pulsar
define result = 10 + 5 * 2;

show(result);
```

The supplied examples explicitly test arithmetic precedence and parentheses. 

---

# 15. Decimal Arithmetic

Decimal values can be used in calculations.

```pulsar
define price = 19.99;
define quantity = 3;

define total = price * quantity;

show(total);
```

---

# 16. Percentages

Numeric expressions can represent percentages.

```pulsar
define price = 1000;
define discount = price * 0.15;

show(discount);
```

The result can then be used in another expression:

```pulsar
define total = price - discount;

show(total);
```

---

# 17. Numeric Comparisons

Numbers can be compared using:

```text
<
<=
>
>=
```

Examples:

```pulsar
show(10 < 20);
```

```pulsar
show(10 <= 10);
```

```pulsar
show(20 > 10);
```

```pulsar
show(20 >= 20);
```

The supplied examples explicitly test all four comparison operators. 

---

# 18. Numeric Equality

Numbers can be compared using:

```text
==
!=
```

Example:

```pulsar
show(10 == 10);
```

```pulsar
show(10 != 20);
```

The supplied examples explicitly test both equality operators. 

---

# 19. Numbers in Conditions

Numeric comparisons are commonly used in `if`.

```pulsar
define score = 85;

if score >= 50 {
    show("Pass");
}
```

---

# 20. Multiple Numeric Conditions

```pulsar
define age = 20;

if age >= 18 and age < 100 {
    show("Valid age");
}
```

This combines:

```text
>=
and
<
```

The parser evaluates logical expressions above the equality/comparison levels. 

---

# 21. Numeric Variables Can Be Reassigned

```pulsar
define score = 50;

score = 75;

show(score);
```

The supplied examples explicitly demonstrate assignment to an existing variable. 

---

# 22. Addition Assignment

```pulsar
define score = 50;

score += 10;

show(score);
```

Conceptually:

```text
score = score + 10
```

---

# 23. Subtraction Assignment

```pulsar
define score = 50;

score -= 10;

show(score);
```

Conceptually:

```text
score = score - 10
```

---

# 24. Multiplication Assignment

```pulsar
define value = 10;

value *= 5;

show(value);
```

---

# 25. Division Assignment

```pulsar
define value = 100;

value /= 4;

show(value);
```

---

# 26. Remainder Assignment

```pulsar
define value = 17;

value %= 5;

show(value);
```

Pulsar's supplied examples test `+=`, `-=`, `*=`, `/=`, and `%=`. 

---

# 27. Increment

The `++` operator increases a numeric value.

```pulsar
define count = 0;

count++;

show(count);
```

The supplied examples explicitly test increment. 

---

# 28. Decrement

The `--` operator decreases a numeric value.

```pulsar
define count = 10;

count--;

show(count);
```

The supplied examples explicitly test decrement. 

---

# 29. Prefix Increment

```pulsar
define count = 10;

++count;

show(count);
```

The parser represents prefix updates as `UpdateExpression` nodes. 

---

# 30. Prefix Decrement

```pulsar
define count = 10;

--count;

show(count);
```

---

# 31. Numbers in Loops

Numbers are frequently used as loop counters.

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
}
```

The supplied examples demonstrate this exact numeric loop pattern. 

---

# 32. Numeric `for` Loop

```pulsar
for (define i = 0; i < 10; i++) {
    show(i);
}
```

The supplied examples explicitly test standard numeric `for` loops. 

---

# 33. Numbers as Function Arguments

Numbers can be passed to functions.

```pulsar
func add(a, b) {
    return a + b;
}

show(add(10, 20));
```

The supplied function examples demonstrate numeric parameters and arithmetic. 

---

# 34. Returning Numbers

Functions can return numeric expressions.

```pulsar
func square(value) {
    return value * value;
}

define result = square(8);

show(result);
```

---

# 35. Numeric Functions

```pulsar
func calculateTotal(price, quantity) {
    return price * quantity;
}

show(calculateTotal(25, 4));
```

---

# 36. Even and Odd Numbers

The remainder operator can be used to test whether a number is even.

```pulsar
func isEven(value) {
    return value % 2 == 0;
}

show(isEven(8));
```

The supplied function examples explicitly demonstrate this pattern. 

For odd numbers:

```pulsar
func isOdd(value) {
    return value % 2 != 0;
}

show(isOdd(7));
```

---

# 37. Numeric Expressions in Arrays

Numbers can be stored in arrays.

```pulsar
define numbers = [
    10,
    20,
    30,
    40
];

show(numbers);
```

The supplied examples demonstrate arrays containing numeric values. 

---

# 38. Numeric Expressions Inside Arrays

Array elements can themselves be expressions.

```pulsar
define values = [
    10 + 5,
    20 * 2,
    100 / 4
];

show(values);
```

---

# 39. Numeric Array Indexing

```pulsar
define numbers = [
    10,
    20,
    30
];

show(numbers[0]);
```

The index expression is numeric.

---

# 40. Numbers in Objects

Numbers can be stored as object properties.

```pulsar
define product = {
    price: 1200,
    stock: 5
};

show(product.price);
```

The supplied examples demonstrate numeric object properties and property access. 

---

# 41. Numeric Object Calculations

```pulsar
define product = {
    price: 100,
    quantity: 3
};

define total =
    product.price * product.quantity;

show(total);
```

---

# 42. Updating Numeric Object Properties

```pulsar
define product = {
    stock: 10
};

product.stock -= 2;

show(product.stock);
```

The supplied examples demonstrate compound assignment on object properties. 

---

# 43. Numbers and Ternary Expressions

Numbers can be used as ternary conditions and results.

```pulsar
define score = 80;

define result =
    score >= 50
        ? 1
        : 0;

show(result);
```

The supplied examples include ternary expressions as part of the expression feature set. 

---

# 44. Numeric Calculations With Ternary

```pulsar
define price = 1000;

define discount =
    price >= 500
        ? price * 0.10
        : 0;

show(discount);
```

---

# 45. Numbers and Logical Expressions

```pulsar
define value = 25;

define valid =
    value > 0 and value < 100;

show(valid);
```

---

# 46. Numbers in Nested Expressions

```pulsar
define a = 10;
define b = 20;
define c = 5;

define result =
    (a + b) * c;

show(result);
```

Nested expressions are evaluated according to the parser's precedence hierarchy. 

---

# 47. Numbers in String Expressions

Numbers can participate in expressions involving strings.

```pulsar
define age = 20;

show("Age: " + age);
```

The precise runtime conversion behavior should follow the interpreter's value/coercion implementation.

---

# 48. Numbers and `str()`

The supplied Pulsar builtins include `str()` for converting a value to a string.

```pulsar
define age = 20;

define text = str(age);

show(text);
```

This is useful when explicit string conversion is desired.

---

# 49. Numbers and `num()`

The supplied examples also use `num()` to convert input into a numeric value.

```pulsar
define value = num(ask("Enter a number: "));

show(value);
```

The supplied examples demonstrate `num(ask(...))` for numeric input. 

---

# 50. Numeric Input

A common input pattern is:

```pulsar
define age = num(ask("Enter your age: "));

show(age);
```

This separates:

```text
input text
    ↓
num()
    ↓
numeric value
```

---

# 51. Calculator Example

```pulsar
define a = num(ask("First number: "));
define b = num(ask("Second number: "));

show("Sum: " + (a + b));
show("Difference: " + (a - b));
show("Product: " + (a * b));
show("Quotient: " + (a / b));
```

---

# 52. Average Calculation

```pulsar
define a = 80;
define b = 90;
define c = 100;

define average =
    (a + b + c) / 3;

show(average);
```

---

# 53. Percentage Calculation

```pulsar
define obtained = 85;
define maximum = 100;

define percentage =
    obtained / maximum * 100;

show(percentage);
```

---

# 54. Discount Calculation

```pulsar
define price = 1200;
define discountRate = 0.15;

define discount =
    price * discountRate;

define total =
    price - discount;

show(total);
```

---

# 55. Compound Numeric Calculation

```pulsar
define price = 100;
define quantity = 5;
define taxRate = 0.05;

define subtotal =
    price * quantity;

define tax =
    subtotal * taxRate;

define total =
    subtotal + tax;

show(total);
```

---

# 56. Numeric Comparison Function

```pulsar
func isGreater(a, b) {
    return a > b;
}

show(isGreater(20, 10));
```

---

# 57. Maximum Value

```pulsar
func max(a, b) {
    return a > b ? a : b;
}

show(max(10, 20));
```

---

# 58. Minimum Value

```pulsar
func min(a, b) {
    return a < b ? a : b;
}

show(min(10, 20));
```

---

# 59. Numeric Mapping

Numbers can be processed using `map()`.

```pulsar
define numbers = [
    1,
    2,
    3,
    4
];

define doubled =
    map(numbers, x => x * 2);

show(doubled);
```

The supplied examples establish `map()` as an array-processing builtin. 

---

# 60. Numeric Filtering

Numbers can be filtered using `filter()`.

```pulsar
define numbers = [
    1,
    2,
    3,
    4,
    5,
    6
];

define even =
    filter(numbers, x => x % 2 == 0);

show(even);
```

---

# 61. Numeric Reduction

Numbers can be combined using `reduce()`.

```pulsar
define numbers = [
    10,
    20,
    30
];

define total =
    reduce(numbers, (a, b) => a + b, 0);

show(total);
```

The supplied examples establish `reduce()` for combining array values. 

---

# 62. Range Generation

The supplied Pulsar builtin set includes `range()`.

A typical numeric use is:

```pulsar
define numbers = range(1, 6);

show(numbers);
```

Use the exact argument behavior implemented by the installed interpreter when relying on `range()`.

---

# 63. Random Numbers

The supplied interpreter includes `random()`.

```pulsar
define value = random();

show(value);
```

The exact range/argument semantics should follow the installed runtime implementation.

---

# 64. Numbers in Object Data

```pulsar
define player = {
    score: 100,
    level: 5,
    coins: 250
};

show(player.score);
show(player.level);
show(player.coins);
```

---

# 65. Numeric Object Mutation

```pulsar
define player = {
    score: 100
};

player.score += 25;

show(player.score);
```

---

# 66. Numeric Loop With Accumulator

```pulsar
define total = 0;
define i = 1;

while i <= 10 {
    total += i;
    i++;
}

show(total);
```

This combines:

```text
<=
+=
++
```

---

# 67. Multiplication Table

```pulsar
define number = 5;
define i = 1;

while i <= 10 {
    show(number * i);
    i++;
}
```

---

# 68. Countdown

```pulsar
define i = 10;

while i > 0 {
    show(i);
    i--;
}
```

---

# 69. Numeric Validation

```pulsar
define value = 75;

if value >= 0 and value <= 100 {
    show("Valid");
} else {
    show("Invalid");
}
```

---

# 70. Complete Numeric Example

```pulsar
func calculateGrade(score) {
    if score >= 90 {
        return 5;
    }

    if score >= 80 {
        return 4;
    }

    if score >= 70 {
        return 3;
    }

    if score >= 60 {
        return 2;
    }

    return 1;
}

define score = 85;
define grade = calculateGrade(score);

show("Score: " + score);
show("Grade: " + grade);
```

---

# 71. Numeric Operator Reference

| Operator | Purpose              | Example  |
| -------- | -------------------- | -------- |
| `+`      | Addition             | `10 + 5` |
| `-`      | Subtraction          | `10 - 5` |
| `*`      | Multiplication       | `10 * 5` |
| `/`      | Division             | `10 / 5` |
| `%`      | Remainder            | `10 % 3` |
| `++`     | Increment            | `x++`    |
| `--`     | Decrement            | `x--`    |
| `+=`     | Add and assign       | `x += 5` |
| `-=`     | Subtract and assign  | `x -= 5` |
| `*=`     | Multiply and assign  | `x *= 5` |
| `/=`     | Divide and assign    | `x /= 5` |
| `%=`     | Remainder and assign | `x %= 5` |
| `<`      | Less than            | `x < 5`  |
| `<=`     | Less than/equal      | `x <= 5` |
| `>`      | Greater than         | `x > 5`  |
| `>=`     | Greater than/equal   | `x >= 5` |
| `==`     | Equal                | `x == 5` |
| `!=`     | Not equal            | `x != 5` |

The arithmetic, comparison, equality, assignment, compound-assignment, and update operators above are represented in the supplied parser/examples.  

---

# 72. Numeric Feature Summary

Pulsar numbers can be used for:

```text
Integer values
Decimal values
Positive values
Negative values
Arithmetic
Comparisons
Equality
Assignments
Compound assignments
Increment/decrement
Loop counters
Function arguments
Function return values
Array values
Array indexes
Object properties
Object calculations
Conditional expressions
Input conversion
Map/filter/reduce operations
Random-number operations
Range generation
```

The supplied interpreter examples establish numeric arithmetic, comparison, assignment, update, function, loop, collection, and conversion use cases.  

---

# 73. Recommended Numeric Tests

For testing the Pulsar interpreter, use this progression:

```text
1. Integer literal
2. Decimal literal
3. Zero
4. Negative number
5. Addition
6. Subtraction
7. Multiplication
8. Division
9. Modulo
10. Parentheses
11. Operator precedence
12. Numeric variables
13. Numeric reassignment
14. Comparisons
15. Equality
16. Compound assignment
17. Increment
18. Decrement
19. Numeric functions
20. Numeric return values
21. Numeric loops
22. Numeric arrays
23. Numeric indexing
24. Numeric objects
25. Numeric object mutation
26. num()
27. map()
28. filter()
29. reduce()
30. range()
31. random()
```

This keeps the documentation aligned with the numeric behavior demonstrated by the supplied Pulsar interpreter materials.
