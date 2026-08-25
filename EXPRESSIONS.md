## 1. Overview

An expression is a piece of Pulsar code that the interpreter evaluates to produce a runtime value.

For example:

```pulsar
10 + 20
```

produces:

```text
30
```

An expression can be as simple as a literal value or as complex as a function call containing nested expressions.

Pulsar's parser separates expressions into several levels, including logical expressions, equality expressions, comparison expressions, arithmetic expressions, unary expressions, postfix expressions, and primary expressions. 

---

# 2. Basic Expression

The simplest expressions are literal values.

```pulsar
10
```

```pulsar
"Pulsar"
```

```pulsar
true
```

```pulsar
null
```

Each expression evaluates directly to its corresponding runtime value.

---

# 3. Variable Expression

A variable name can itself be an expression.

```pulsar
define name = "Pulsar";

show(name);
```

The expression:

```pulsar
name
```

evaluates to:

```text
"Pulsar"
```

---

# 4. Numeric Expressions

Numeric values can participate in arithmetic expressions.

```pulsar
10 + 20
```

```pulsar
100 - 25
```

```pulsar
5 * 8
```

```pulsar
20 / 4
```

```pulsar
17 % 5
```

The supplied examples explicitly test these arithmetic expressions. 

---

# 5. String Expressions

Strings can be combined using `+`.

```pulsar
"Hello " + "Pulsar"
```

Variables can participate too:

```pulsar
define first = "Hello";
define second = "Pulsar";

first + " " + second
```

The supplied examples demonstrate string concatenation using `+`. 

---

# 6. Boolean Expressions

Boolean expressions produce `true` or `false`.

```pulsar
10 > 5
```

```pulsar
10 == 10
```

```pulsar
10 != 20
```

These values can then be used by conditional statements.

---

# 7. Parenthesized Expressions

Parentheses group an expression.

```pulsar
(10 + 20)
```

They can also change the order of evaluation:

```pulsar
(2 + 3) * 4
```

The supplied examples explicitly test parenthesized expressions. 

---

# 8. Arithmetic Expressions

Pulsar supports:

```text
+
-
*
/
%
```

Example:

```pulsar
define result = 10 + 5 * 2;
```

Multiplication is evaluated before addition according to the parser's expression hierarchy. 

---

# 9. Expression Precedence

Pulsar does not simply evaluate every expression from left to right.

The parser establishes separate levels:

```text
logical AND
    ↓
equality
    ↓
comparison
    ↓
term
    ↓
factor
    ↓
unary
    ↓
postfix
    ↓
primary
```

The supplied parser implements these levels through methods such as:

```text
logicalAnd()
equality()
comparison()
term()
factor()
unary()
postfix()
primary()
```



---

# 10. Multiplication Before Addition

For:

```pulsar
2 + 3 * 4
```

the multiplication expression is evaluated first.

Conceptually:

```text
3 * 4
  ↓
12

2 + 12
  ↓
14
```

The supplied examples explicitly test this behavior. 

---

# 11. Parentheses Override Precedence

```pulsar
(2 + 3) * 4
```

is evaluated as:

```text
2 + 3
  ↓
5

5 * 4
  ↓
20
```

---

# 12. Unary Expressions

Pulsar supports unary expressions using:

```text
+
-
!
```

Examples:

```pulsar
+10
```

```pulsar
-10
```

```pulsar
!true
```

The parser handles these in its unary-expression stage. 

---

# 13. Unary Plus

```pulsar
define value = +10;

show(value);
```

The supplied examples explicitly test unary positive values. 

---

# 14. Unary Minus

```pulsar
define value = 10;

show(-value);
```

This produces the negative form of the numeric value.

---

# 15. Logical NOT Expression

`!` produces the logical negation of an expression.

```pulsar
!false
```

produces:

```text
true
```

Example:

```pulsar
define active = true;

if (!active) {
    show("Inactive");
}
```

The supplied examples explicitly test `!false`. 

---

# 16. Comparison Expressions

Comparison expressions include:

```text
<
<=
>
>=
```

Examples:

```pulsar
10 < 20
```

```pulsar
10 <= 10
```

```pulsar
20 > 10
```

```pulsar
20 >= 20
```

The supplied examples test these comparison forms. 

---

# 17. Equality Expressions

Equality expressions use:

```text
==
!=
```

Examples:

```pulsar
10 == 10
```

```pulsar
10 != 20
```

The parser represents these through its equality-expression stage. 

---

# 18. Logical Expressions

Pulsar supports logical expressions using:

```text
and
or
```

Example:

```pulsar
true and true
```

Example:

```pulsar
false or true
```

The supplied examples explicitly demonstrate both forms. 

---

# 19. Combined Logical Expression

Expressions can be combined:

```pulsar
define age = 20;
define verified = true;

age >= 18 and verified
```

This produces a boolean result.

The supplied examples use comparisons combined with `and`. 

---

# 20. Equality and Logical Expressions

A comparison can be combined with equality and logical operators.

```pulsar
define result =
    10 > 5 and 20 == 20;
```

Conceptually:

```text
10 > 5
  ↓
true

20 == 20
   ↓
true

true and true
     ↓
true
```

The parser processes the lower-level comparison/equality expressions before the logical level. 

---

# 21. Assignment Expressions

Assignment changes the value associated with a variable.

```pulsar
define value = 10;

value = 20;
```

The supplied examples explicitly test assignment after declaration. 

---

# 22. Compound Assignment Expressions

Pulsar supports:

```text
+=
-=
*=
/=
%=
```

Example:

```pulsar
define value = 10;

value += 5;
```

Conceptually:

```text
value = value + 5
```

The supplied examples test all five compound assignments. 

---

# 23. Update Expressions

Pulsar supports:

```text
++
--
```

Example:

```pulsar
define counter = 0;

counter++;
```

and:

```pulsar
counter--;
```

The parser represents these as update expressions. 

---

# 24. Prefix Update Expressions

Prefix increment:

```pulsar
++counter
```

Prefix decrement:

```pulsar
--counter
```

The parser explicitly records prefix update expressions with `prefix: true`. 

---

# 25. Postfix Update Expressions

Postfix increment:

```pulsar
counter++
```

Postfix decrement:

```pulsar
counter--
```

These are commonly used in loops:

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
}
```

The supplied loop examples use this pattern. 

---

# 26. Property Access Expressions

The dot operator produces a property-access expression.

```pulsar
define user = {
    name: "Pulsar"
};

user.name
```

Nested property access is possible:

```pulsar
user.profile.name
```

The supplied examples explicitly demonstrate nested property access. 

---

# 27. Bracket Access Expressions

Square brackets can access an array element:

```pulsar
define numbers = [10, 20, 30];

numbers[0]
```

They can also access object properties:

```pulsar
define user = {
    name: "Pulsar"
};

user["name"]
```

The supplied examples demonstrate bracket property access. 

---

# 28. Nested Access Expressions

Property access and indexing can be combined.

```pulsar
define users = [
    {
        name: "Pulsar"
    }
];

users[0].name
```

Another example:

```pulsar
define data = {
    users: [
        {
            name: "Pulsar"
        }
    ]
};

data.users[0].name
```

These expressions are evaluated through the postfix-expression stage.

---

# 29. Function Call Expressions

Calling a function is an expression.

```pulsar
func add(a, b) {
    return a + b;
}

add(10, 20)
```

The result is the value returned by the function.

For example:

```pulsar
define result = add(10, 20);
```

The supplied evaluator checks that the call target is callable before performing the call. 

---

# 30. Nested Function Calls

Function calls can contain other expressions:

```pulsar
add(10 + 5, 20 * 2)
```

They can also contain other function calls:

```pulsar
add(10, add(5, 5))
```

This demonstrates that function-call arguments are themselves expressions.

---

# 31. Arrow Function Expressions

Arrow functions are expressions that produce callable values.

```pulsar
x => x * 2
```

Example:

```pulsar
define double = x => x * 2;

show(double(10));
```

Multiple parameters:

```pulsar
define add = (a, b) => a + b;
```

The supplied examples demonstrate arrow-function expressions and calls. 

---

# 32. Arrow Functions With Blocks

An arrow function can contain a block:

```pulsar
define calculate = (a, b) => {
    define result = a * b;
    return result;
};
```

The arrow function expression itself produces a callable value.

---

# 33. Array Expressions

An array literal is an expression.

```pulsar
[1, 2, 3]
```

It can be assigned:

```pulsar
define numbers = [1, 2, 3];
```

Array elements can themselves be expressions:

```pulsar
define values = [
    10 + 5,
    20 * 2,
    100 / 4
];
```

---

# 34. Object Expressions

An object literal is also an expression.

```pulsar
{
    name: "Pulsar",
    version: 1
}
```

Properties can contain expressions:

```pulsar
define price = 100;
define quantity = 3;

define product = {
    price: price,
    total: price * quantity
};
```

The supplied examples demonstrate object literals and computed object properties. 

---

# 35. Nested Object Expressions

```pulsar
define user = {
    profile: {
        name: "Pulsar",
        active: true
    }
};
```

The nested object itself is an expression contained inside another object expression.

---

# 36. Ternary Expressions

Pulsar supports the conditional expression:

```text
condition ? valueIfTrue : valueIfFalse
```

Example:

```pulsar
define status =
    true
        ? "yes"
        : "no";
```

The supplied examples include ternary expressions in the Ternary and Nullish section. 

---

# 37. Ternary Expression With Comparison

```pulsar
define age = 20;

define status =
    age >= 18
        ? "adult"
        : "minor";
```

The condition itself is an expression:

```pulsar
age >= 18
```

and each branch is also an expression.

---

# 38. Nullish Expressions

The supplied examples include nullish expressions as part of the Ternary and Nullish feature set. 

Where supported by the installed interpreter:

```pulsar
define name = null;

define result = name ?? "Unknown";
```

The expression selects the fallback when the left-hand value is `null`.

---

# 39. Expression Statements

An expression can appear as a standalone statement.

For example:

```pulsar
show("Hello");
```

or:

```pulsar
counter++;
```

The expression is evaluated for its effect even when its resulting value is not assigned to a variable.

---

# 40. Expressions Inside `if`

The condition of an `if` statement is an expression.

```pulsar
define score = 90;

if score >= 80 {
    show("Pass");
}
```

Here:

```pulsar
score >= 80
```

is the condition expression.

---

# 41. Expressions Inside `while`

The condition of a `while` loop is also an expression.

```pulsar
define i = 0;

while i < 5 {
    show(i);
    i++;
}
```

Here:

```pulsar
i < 5
```

is evaluated repeatedly.

The supplied examples explicitly use comparison expressions in `while` conditions. 

---

# 42. Expressions Inside `for`

Standard `for` loops contain expression components.

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

The three important components are:

```text
Initialization:
define i = 0

Test:
i < 5

Update:
i++
```

The supplied examples explicitly test standard `for` loops. 

---

# 43. Expressions Inside Function Arguments

Function arguments are expressions.

```pulsar
show(10 + 20);
```

Multiple expressions:

```pulsar
add(
    10 + 5,
    20 * 2
);
```

The interpreter evaluates those argument expressions before invoking the function.

---

# 44. Expressions Inside Arrays

```pulsar
define values = [
    10 + 5,
    20 * 2,
    100 / 4
];
```

The resulting array contains:

```text
15
40
25
```

---

# 45. Expressions Inside Objects

```pulsar
define price = 100;
define quantity = 5;

define order = {
    price: price,
    quantity: quantity,
    total: price * quantity
};
```

The property:

```pulsar
price * quantity
```

is evaluated before the resulting object is produced.

---

# 46. Expressions and Return

A `return` statement can return any expression.

```pulsar
func calculate(a, b) {
    return a + b;
}
```

Another example:

```pulsar
func getStatus(score) {
    return score >= 50 ? "pass" : "fail";
}
```

The supplied function examples demonstrate returning calculated expressions. 

---

# 47. Expressions and Variables

Expressions can be chained through variables.

```pulsar
define price = 100;
define quantity = 3;

define subtotal = price * quantity;
define discount = subtotal * 0.10;
define total = subtotal - discount;
```

The value flow is:

```text
price
  +
quantity
  ↓
subtotal
  ↓
discount
  ↓
total
```

---

# 48. Complex Expression

A complete expression can combine many operators:

```pulsar
define price = 100;
define quantity = 3;

define total =
    price * quantity
    - (price * quantity * 0.10);
```

This expression contains:

```text
*
-
()
```

---

# 49. Complex Conditional Expression

```pulsar
define age = 20;
define verified = true;

define allowed =
    age >= 18
    and verified
    and age < 100;
```

This combines:

```text
>=
and
<
```

into one boolean expression.

---

# 50. Expression Evaluation Model

Conceptually, Pulsar evaluates expressions through a hierarchy:

```text
Source
  |
  v
Parser
  |
  v
Expression Tree
  |
  v
Evaluator
  |
  v
Runtime Value
```

For example:

```pulsar
2 + 3 * 4
```

is parsed according to the expression hierarchy, then evaluated into:

```text
14
```

The supplied parser explicitly builds binary, logical, unary, update, call, member, index, and other expression nodes. 

---

# 51. Expression Categories

A practical classification of Pulsar expressions is:

```text
Primary Expressions
├── Literals
├── Identifiers
├── Parenthesized expressions
├── Array expressions
└── Object expressions

Unary Expressions
├── +expression
├── -expression
└── !expression

Binary Expressions
├── +
├── -
├── *
├── /
├── %
├── <
├── <=
├── >
├── >=
├── ==
└── !=

Logical Expressions
├── and
└── or

Update Expressions
├── ++
└── --

Postfix Expressions
├── property access
├── index access
├── slicing
└── function calls

Conditional Expressions
└── ? :

Nullish Expressions
└── ??
```

The parser structure directly supports the major expression layers above. 

---

# 52. Primary Expressions

Primary expressions form the basic building blocks from which larger expressions are constructed.

Examples:

```pulsar
10
```

```pulsar
"Pulsar"
```

```pulsar
true
```

```pulsar
null
```

```pulsar
name
```

The parser's primary-expression stage handles literals, identifiers, grouped expressions, arrays, objects, and other primary constructs. 

---

# 53. Expressions Can Be Nested

Expressions can contain other expressions at many levels.

```pulsar
show(
    add(
        10 + 5,
        20 * 2
    )
);
```

The interpreter must evaluate the nested expressions before producing the final result.

---

# 54. Complete Expression Example

```pulsar
define price = 120;
define quantity = 4;
define member = true;

define subtotal = price * quantity;

define discount =
    member and subtotal >= 400
        ? subtotal * 0.15
        : 0;

define total = subtotal - discount;

show(total);
```

This program uses:

```text
*
and
>=
?
:
-
```

and demonstrates how several expression types can work together.

---

# 55. Expression Testing Order

When testing the Pulsar expression evaluator, a useful progression is:

```text
1. Literals
2. Identifiers
3. Parentheses
4. Addition
5. Subtraction
6. Multiplication
7. Division
8. Modulo
9. Unary +
10. Unary -
11. Logical !
12. Comparisons
13. Equality
14. and
15. or
16. Assignment
17. Compound assignment
18. ++ / --
19. Property access
20. Array indexing
21. Function calls
22. Arrow functions
23. Array expressions
24. Object expressions
25. Ternary
26. Nullish
27. Nested expressions
```

This follows the progression represented by the supplied interpreter examples and parser structure. 

---

# 56. Final Example

```pulsar
func calculate(price, quantity, member) {
    define subtotal = price * quantity;

    define discount =
        member and subtotal >= 500
            ? subtotal * 0.10
            : 0;

    return subtotal - discount;
}

define price = 120;
define quantity = 5;
define member = true;

define total = calculate(
    price,
    quantity,
    member
);

show(total);
```

This single program combines:

```text
Variables
Arithmetic expressions
Comparison expressions
Logical expressions
Ternary expressions
Function-call expressions
Return expressions
Nested expressions
```

Expressions are therefore the central mechanism through which Pulsar transforms source code into runtime values.
