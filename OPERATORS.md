## 1. Overview

Operators allow Pulsar programs to calculate values, compare values, combine logical conditions, modify variables, and select between expressions.

The supplied Pulsar examples and parser define the following major operator groups:

```text
Arithmetic
Comparison
Logical
Unary
Update
Assignment
Compound Assignment
Ternary
Nullish
```

The parser implements arithmetic, comparison, equality, logical, unary, and update expressions as distinct expression levels. 

---

# 2. Arithmetic Operators

Pulsar supports the basic arithmetic operators:

| Operator | Operation      |
| -------- | -------------- |
| `+`      | Addition       |
| `-`      | Subtraction    |
| `*`      | Multiplication |
| `/`      | Division       |
| `%`      | Remainder      |

The supplied examples explicitly test all five. 

### Addition

```pulsar
show(2 + 3);
```

### Subtraction

```pulsar
show(10 - 4);
```

### Multiplication

```pulsar
show(6 * 7);
```

### Division

```pulsar
show(20 / 5);
```

### Remainder

```pulsar
show(17 % 5);
```

---

# 3. Addition With Variables

Operators can work with variables.

```pulsar
define a = 10;
define b = 20;

define result = a + b;

show(result);
```

Output:

```text
30
```

---

# 4. String Concatenation

The `+` operator can also combine strings.

```pulsar
show("Hello " + "Pulsar");
```

The supplied examples explicitly use `+` for string concatenation. 

Variables can also be combined:

```pulsar
define first = "Hello";
define second = "Pulsar";

show(first + " " + second);
```

---

# 5. Operator Precedence

Arithmetic operators follow normal precedence.

Multiplication, division, and remainder are evaluated before addition and subtraction.

```pulsar
show(2 + 3 * 4);
```

This is interpreted as:

```text
2 + (3 * 4)
```

rather than:

```text
(2 + 3) * 4
```

The supplied examples explicitly test this behavior. 

---

# 6. Parentheses

Parentheses can explicitly control evaluation order.

```pulsar
show((2 + 3) * 4);
```

The parser handles grouped expressions before returning them to the surrounding expression levels.

The supplied examples explicitly test parenthesized arithmetic. 

Another example:

```pulsar
define result = (10 + 20) / 5;
```

---

# 7. Unary Operators

Pulsar supports unary:

```text
+
-
!
```

The parser recognizes `NOT`, `MINUS`, and `PLUS` as unary operators. 

---

# 8. Unary Plus

Unary `+` indicates a positive numeric expression.

```pulsar
show(+25);
```

The supplied examples explicitly test unary plus. 

---

# 9. Unary Minus

Unary `-` negates a numeric value.

```pulsar
show(-25);
```

Variables can also be negated:

```pulsar
define value = 25;

show(-value);
```

---

# 10. Logical NOT

`!` negates a logical value.

```pulsar
show(!false);
```

Result:

```text
true
```

Another example:

```pulsar
define active = true;

if (!active) {
    show("Inactive");
}
```

The supplied examples explicitly test `!false`. 

---

# 11. Equality Operators

Pulsar supports:

```text
==
!=
```

The parser recognizes `EQEQ` and `NOTEQ` as equality operators. 

### Equal

```pulsar
show(10 == 10);
```

### Not equal

```pulsar
show(10 != 20);
```

The supplied examples explicitly test both. 

---

# 12. Less Than

The `<` operator tests whether the left value is less than the right value.

```pulsar
show(5 < 10);
```

---

# 13. Less Than or Equal

The `<=` operator tests whether the left value is less than or equal to the right value.

```pulsar
show(5 <= 5);
```

---

# 14. Greater Than

The `>` operator tests whether the left value is greater than the right value.

```pulsar
show(10 > 3);
```

---

# 15. Greater Than or Equal

The `>=` operator tests whether the left value is greater than or equal to the right value.

```pulsar
show(10 >= 10);
```

The supplied examples test all four comparison operators. 

---

# 16. Comparison Table

| Operator | Meaning               | Example  |
| -------- | --------------------- | -------- |
| `==`     | Equal                 | `a == b` |
| `!=`     | Not equal             | `a != b` |
| `<`      | Less than             | `a < b`  |
| `<=`     | Less than or equal    | `a <= b` |
| `>`      | Greater than          | `a > b`  |
| `>=`     | Greater than or equal | `a >= b` |

---

# 17. Logical AND

Pulsar supports the word-form logical operator:

```text
and
```

Example:

```pulsar
show(true and true);
```

Another:

```pulsar
show(true and false);
```

The supplied examples use the word `and`, and the parser represents it internally as the `AND` logical operator.  

---

# 18. Logical OR

Pulsar supports:

```text
or
```

Example:

```pulsar
show(false or true);
```

The supplied examples explicitly test this form. 

---

# 19. Combining Conditions

Logical operators can combine comparisons.

```pulsar
define age = 20;
define verified = true;

if age >= 18 and verified {
    show("Allowed");
}
```

The supplied examples demonstrate multiple comparisons combined with `and`. 

---

# 20. Logical Expression Example

```pulsar
define a = 10;
define b = 20;

define result = a < b and b > 15;

show(result);
```

The comparison expressions are evaluated and then combined by the logical operator.

---

# 21. Assignment Operator

The basic assignment operator is:

```text
=
```

Example:

```pulsar
define x = 10;

x = 20;

show(x);
```

The first `=` initializes the variable.

The second `=` changes the variable's value.

The supplied examples explicitly demonstrate normal assignment. 

---

# 22. Compound Assignment

Pulsar supports compound assignment operators:

```text
+=
-=
*=
/=
%=
```

The supplied examples explicitly test all five. 

---

# 23. Addition Assignment

```pulsar
define x = 10;

x += 5;

show(x);
```

Conceptually:

```text
x = x + 5
```

---

# 24. Subtraction Assignment

```pulsar
define x = 10;

x -= 3;

show(x);
```

Conceptually:

```text
x = x - 3
```

---

# 25. Multiplication Assignment

```pulsar
define x = 10;

x *= 4;

show(x);
```

Conceptually:

```text
x = x * 4
```

---

# 26. Division Assignment

```pulsar
define x = 20;

x /= 5;

show(x);
```

Conceptually:

```text
x = x / 5
```

---

# 27. Remainder Assignment

```pulsar
define x = 17;

x %= 5;

show(x);
```

Conceptually:

```text
x = x % 5
```

---

# 28. Increment Operator

Pulsar supports:

```text
++
```

Example:

```pulsar
define x = 10;

x++;

show(x);
```

The supplied examples explicitly test increment. 

It is commonly used in loops:

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
}
```

---

# 29. Decrement Operator

Pulsar supports:

```text
--
```

Example:

```pulsar
define x = 10;

x--;

show(x);
```

The supplied examples explicitly test decrement. 

---

# 30. Prefix Increment

The parser also recognizes prefix update expressions.

```pulsar
define x = 10;

++x;

show(x);
```

Internally this is represented as an `UpdateExpression` with `prefix: true`. 

---

# 31. Prefix Decrement

Similarly:

```pulsar
define x = 10;

--x;

show(x);
```

The parser recognizes `MINUSMINUS` as a prefix update operator. 

---

# 32. Update Operators

The update operators are:

| Operator | Operation |
| -------- | --------- |
| `++`     | Increment |
| `--`     | Decrement |

They are update expressions rather than ordinary binary arithmetic expressions.

The parser explicitly creates `UpdateExpression` nodes for them. 

---

# 33. Property Assignment

Operators can be applied to object properties.

```pulsar
define user = {
    name: "Puma"
};

user.name = "Pulsar";

show(user.name);
```

The supplied examples explicitly test property assignment. 

---

# 34. Compound Property Assignment

Compound operators can also be used with object properties.

```pulsar
define user = {
    score: 100
};

user.score += 10;

show(user.score);
```

The supplied examples explicitly test this behavior. 

---

# 35. Array Indexing

Indexing uses brackets:

```text
[]
```

Example:

```pulsar
define values = [10, 20, 30];

show(values[0]);
```

Indexing is parsed as a postfix operation.

The parser handles bracket indexing and slicing in the postfix stage. 

---

# 36. Object Bracket Access

Objects can also be accessed using brackets:

```pulsar
define user = {
    name: "Pulsar"
};

show(user["name"]);
```

The supplied examples explicitly demonstrate bracket property access. 

---

# 37. Property Access

The dot operator accesses object properties.

```pulsar
define user = {
    name: "Pulsar"
};

show(user.name);
```

Nested property access:

```pulsar
define data = {
    user: {
        name: "Pulsar"
    }
};

show(data.user.name);
```

The supplied examples demonstrate nested dot access. 

---

# 38. Function Call Operator

Parentheses are used to call functions.

```pulsar
func add(a, b) {
    return a + b;
}

show(add(10, 20));
```

Function calls can be nested:

```pulsar
show(add(10, add(5, 5)));
```

The evaluator checks that the resulting value is callable before invoking it. 

---

# 39. Ternary Operator

Pulsar supports the ternary conditional operator:

```text
? :
```

Basic example:

```pulsar
show(true ? "yes" : "no");
```

The supplied examples include a dedicated Ternary and Nullish section and explicitly demonstrate ternary expressions. 

---

# 40. Ternary With Variables

```pulsar
define age = 20;

define status =
    age >= 18
        ? "adult"
        : "minor";

show(status);
```

The ternary expression produces one of two values.

---

# 41. Nested Ternary

Ternary expressions can be used inside larger expressions.

```pulsar
define score = 85;

define grade =
    score >= 90
        ? "A"
        : score >= 80
            ? "B"
            : "C";

show(grade);
```

For readability, ordinary `if` statements may be preferable for complicated conditions.

---

# 42. Nullish Operator

The supplied examples include a dedicated **Ternary and Nullish** section. 

Where the interpreter supports the nullish operator, it is used to provide a fallback when a value is `null`.

Example:

```pulsar
define name = null;

define result = name ?? "Unknown";

show(result);
```

Conceptually:

```text
name is null
     |
     v
"Unknown"
```

Only use `??` if the installed interpreter version contains the corresponding parser/evaluator support.

---

# 43. Operator Precedence

The parser establishes the expression hierarchy in the following general order, from lower-level operands toward higher-level expression combinations:

```text
Logical AND
    |
Equality
    |
Comparison
    |
Addition / Subtraction
    |
Multiplication / Division / Modulo
    |
Unary
    |
Postfix
    |
Primary
```

The parser explicitly implements:

```text
logicalAnd()
equality()
comparison()
term()
factor()
unary()
postfix()
```

in this structure. 

---

# 44. Arithmetic Precedence Example

```pulsar
define result = 2 + 3 * 4;

show(result);
```

The multiplication is evaluated before addition:

```text
3 * 4
  |
  v
12

2 + 12
  |
  v
14
```

The supplied examples explicitly test this precedence. 

---

# 45. Parentheses Override Precedence

```pulsar
define result = (2 + 3) * 4;

show(result);
```

Evaluation:

```text
2 + 3
  |
  v
5

5 * 4
  |
  v
20
```

---

# 46. Comparison Precedence

Arithmetic is evaluated before comparison.

```pulsar
define result = 2 + 3 > 4;

show(result);
```

Conceptually:

```text
2 + 3
  |
  v
5

5 > 4
  |
  v
true
```

The parser places comparison above the arithmetic expression levels. 

---

# 47. Equality Precedence

Equality is evaluated after comparison.

```pulsar
define result = 5 > 3 == true;

show(result);
```

The parser processes comparison expressions before equality expressions. 

For complex expressions, parentheses are recommended when readability matters.

---

# 48. Logical Precedence

Logical `and` is evaluated after equality/comparison expressions.

```pulsar
define result = 10 > 5 and 20 > 10;

show(result);
```

Conceptually:

```text
10 > 5
   |
   v
true

20 > 10
   |
   v
true

true and true
      |
      v
true
```

The parser's `logicalAnd()` consumes equality expressions. 

---

# 49. Operator Precedence Example

```pulsar
define a = 10;
define b = 20;
define c = 30;

define result =
    a + b * c > 100
    and c != 0;

show(result);
```

The expression is evaluated through the parser's expression hierarchy rather than simply from left to right.

---

# 50. Operators in Conditions

Operators are commonly used in `if` statements.

```pulsar
define score = 95;

if score >= 90 {
    show("A");
}
```

The supplied examples use comparison operators extensively in conditional statements. 

---

# 51. Operators in Loops

Operators are also fundamental to loops.

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
}
```

This combines:

```text
<
++
```

The supplied loop examples demonstrate this exact pattern. 

---

# 52. Operators in Functions

```pulsar
func isEven(value) {
    return value % 2 == 0;
}

show(isEven(8));
```

This combines:

```text
%
==
```

The supplied function examples explicitly use this pattern. 

---

# 53. Operators With Objects

```pulsar
define point = {
    x: 10,
    y: 20
};

show(point.x + point.y);
```

The supplied examples demonstrate arithmetic performed on object properties. 

---

# 54. Operators With Arrays

```pulsar
define values = [10, 20, 30];

define total = values[0] + values[1];

show(total);
```

Indexing happens first, then arithmetic operates on the resulting values.

---

# 55. Operators and `null`

Comparison with `null` is supported by the supplied examples:

```pulsar
define value = null;

if value == null {
    show("empty");
}
```

The examples explicitly use this pattern. 

---

# 56. Complete Operator Example

```pulsar
define price = 100;
define quantity = 3;

define subtotal = price * quantity;

define discount =
    subtotal >= 200
        ? subtotal * 0.10
        : 0;

define total = subtotal - discount;

if total > 200 and quantity > 0 {
    show("Order accepted");
}

show(total);
```

This example combines:

```text
*
>=
?
:
*
-
>
and
>
```

---

# 57. Operator Summary

| Category            | Operators                    |
| ------------------- | ---------------------------- |
| Arithmetic          | `+`, `-`, `*`, `/`, `%`      |
| Comparison          | `<`, `<=`, `>`, `>=`         |
| Equality            | `==`, `!=`                   |
| Logical             | `and`, `or`, `!`             |
| Assignment          | `=`                          |
| Compound assignment | `+=`, `-=`, `*=`, `/=`, `%=` |
| Update              | `++`, `--`                   |
| Unary               | `+`, `-`, `!`                |
| Ternary             | `? :`                        |
| Nullish             | `??`                         |
| Property access     | `.`                          |
| Index access        | `[]`                         |
| Function call       | `()`                         |

The arithmetic, comparison, equality, logical, unary, and update operators above are directly represented in the supplied parser and examples.  

---

# 58. Recommended Testing Order

When testing operators in a fresh Pulsar interpreter, use this progression:

```text
1. Addition
2. Subtraction
3. Multiplication
4. Division
5. Modulo
6. Parentheses
7. Unary + and -
8. Equality
9. Comparison
10. and
11. or
12. !
13. Assignment
14. Compound assignment
15. ++
16. --
17. Property assignment
18. Array/object access
19. Ternary
20. Nullish
```

The supplied example collection follows the same progression from arithmetic through comparison, logic, assignment, and later expression features. 

---

# 59. Important Implementation Note

The operator names shown in Pulsar source code are not always identical to the token names used internally.

For example:

```text
Pulsar source       Parser token
---------------------------------
+                   PLUS
-                   MINUS
*                   STAR
/                   SLASH
%                   MOD
==                  EQEQ
!=                  NOTEQ
<                   LT
<=                  LTE
>                   GT
>=                  GTE
and                 AND
```

The parser converts source tokens into expression nodes such as `BinaryExpression`, `LogicalExpression`, `UnaryExpression`, and `UpdateExpression`. 
