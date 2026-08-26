## 1. Overview

Pulsar provides the `return` statement for ending the current function execution and optionally sending a value back to the code that called the function.

The basic forms are:

```pulsar
return;
```

and:

```pulsar
return value;
```

A returned value can be stored in a variable, used in an expression, passed to another function, or used as a condition.

---

## 2. Basic `return`

```pulsar
func greet() {
    return;
}

greet();
```

A function can return without providing a value.

---

## 3. Returning a Value

```pulsar
func add(a, b) {
    return a + b;
}

define result = add(10, 20);

show(result);
```

Output:

```text
30
```

---

## 4. Returning a Number

```pulsar
func square(value) {
    return value * value;
}

show(square(5));
```

Output:

```text
25
```

---

## 5. Returning a String

```pulsar
func getMessage() {
    return "Hello, Pulsar";
}

show(getMessage());
```

---

## 6. Returning a Boolean

```pulsar
func isPositive(value) {
    return value > 0;
}

show(isPositive(10));
```

Output:

```text
true
```

---

## 7. Returning `null`

```pulsar
func findNothing() {
    return null;
}

define result = findNothing();

show(result);
```

`null` can be useful when a function cannot produce a meaningful result.

---

## 8. Returning an Array

```pulsar
func getNumbers() {
    return [
        10,
        20,
        30
    ];
}

define numbers = getNumbers();

show(numbers);
```

---

## 9. Returning an Object

```pulsar
func createUser() {
    return {
        name: "Alice",
        age: 20
    };
}

define user = createUser();

show(user.name);
```

---

## 10. Returning a Variable

```pulsar
func calculate(a, b) {
    define result = a * b;

    return result;
}

show(calculate(5, 4));
```

---

# 11. `return` From a Conditional

```pulsar
func check(value) {
    if value > 10 {
        return "large";
    }

    return "small";
}

show(check(20));
```

Output:

```text
large
```

---

# 12. Multiple `return` Statements

A function can contain several possible return paths.

```pulsar
func classify(value) {
    if value > 0 {
        return "positive";
    }

    if value < 0 {
        return "negative";
    }

    return "zero";
}

show(classify(10));
show(classify(-5));
show(classify(0));
```

Output:

```text
positive
negative
zero
```

---

# 13. Early Return

`return` immediately stops the current function.

```pulsar
func validate(value) {
    if value == null {
        return false;
    }

    return true;
}

show(validate(null));
```

Once `return false` executes, the remaining statements in that function are not executed.

---

# 14. Return From a Function

```pulsar
func test() {
    show("Before");

    return;

    show("After");
}

test();
```

Output:

```text
Before
```

The statement after `return` is not reached.

---

# 15. Return From a Function Inside a Loop

```pulsar
func findValue(values, target) {
    for value in values {
        if value == target {
            return value;
        }
    }

    return null;
}

define values = [
    10,
    20,
    30
];

show(findValue(values, 20));
```

The `return` ends the function immediately when the target is found.

---

# 16. Search Function

```pulsar
func findName(names, target) {
    for name in names {
        if name == target {
            return name;
        }
    }

    return null;
}

define names = [
    "Alice",
    "Bob",
    "Charlie"
];

show(findName(names, "Bob"));
```

---

# 17. Return From `while`

```pulsar
func findNumber(values, target) {
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

show(findNumber(values, 30));
```

---

# 18. Return From `for`

```pulsar
func findNumber(values, target) {
    for (define i = 0; i < values.length; i++) {
        if values[i] == target {
            return values[i];
        }
    }

    return null;
}

show(findNumber([10, 20, 30], 20));
```

---

# 19. Return From `for ... in`

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
    }
];

define product = findProduct(products, 2);

show(product.name);
```

---

# 20. `return` vs `break`

`return` exits the **function**.

`break` exits the **current loop**.

Example:

```pulsar
func search(values, target) {
    for value in values {
        if value == target {
            return value;
        }
    }

    return null;
}
```

Here, finding the value exits the function completely.

By contrast:

```pulsar
define found = null;

for value in values {
    if value == target {
        found = value;
        break;
    }
}

show(found);
```

Here, `break` exits only the loop.

---

# 21. `return` vs `continue`

`continue` skips the current loop iteration.

`return` ends the function.

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

In this example:

* negative values are skipped
* `100` ends the function
* other values continue normally

---

# 22. Return From Nested Loops

```pulsar
func findValue(groups, target) {
    for group in groups {
        for value in group {
            if value == target {
                return value;
            }
        }
    }

    return null;
}

define groups = [
    [1, 2, 3],
    [4, 5, 6]
];

show(findValue(groups, 5));
```

The `return` exits the function, not merely the inner loop.

---

# 23. Returning a Calculation

```pulsar
func calculateTotal(price, quantity) {
    define total = price * quantity;

    return total;
}

define total = calculateTotal(50, 4);

show(total);
```

Output:

```text
200
```

---

# 24. Returning an Expression

A return statement can directly contain an expression.

```pulsar
func calculate(a, b) {
    return (a + b) * 2;
}

show(calculate(10, 5));
```

Output:

```text
30
```

---

# 25. Returning a Function Result

```pulsar
func double(value) {
    return value * 2;
}

func quadruple(value) {
    return double(double(value));
}

show(quadruple(5));
```

Output:

```text
20
```

---

# 26. Function Calls Using Returned Values

```pulsar
func add(a, b) {
    return a + b;
}

define result = add(10, 20);

show(result * 2);
```

Output:

```text
60
```

---

# 27. Return in a Conditional Expression

```pulsar
func maximum(a, b) {
    if a > b {
        return a;
    }

    return b;
}

show(maximum(50, 20));
```

---

# 28. Validation Function

```pulsar
func validQuantity(quantity) {
    if quantity <= 0 {
        return false;
    }

    return true;
}

if validQuantity(5) {
    show("Valid");
}
```

---

# 29. Validation With Multiple Conditions

```pulsar
func validProduct(product) {
    if product == null {
        return false;
    }

    if product.stock <= 0 {
        return false;
    }

    if product.price <= 0 {
        return false;
    }

    return true;
}
```

---

# 30. Product Lookup

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
    }
];

func findProduct(id) {
    for product in products {
        if product.id == id {
            return product;
        }
    }

    return null;
}

define product = findProduct(1);

if product == null {
    show("Product not found");
} else {
    show(product.name);
}
```

---

# 31. Returning From a Shop Function

```pulsar
func calculateDiscount(subtotal) {
    if subtotal >= 1000 {
        return subtotal * 0.15;
    }

    if subtotal >= 500 {
        return subtotal * 0.10;
    }

    if subtotal >= 200 {
        return subtotal * 0.05;
    }

    return 0;
}

show(calculateDiscount(1200));
```

---

# 32. Returning a Cart Subtotal

```pulsar
func calculateSubtotal(cart) {
    define subtotal = 0;

    for item in cart {
        subtotal =
            subtotal +
            item.price * item.quantity;
    }

    return subtotal;
}

define cart = [
    {
        price: 100,
        quantity: 2
    },
    {
        price: 50,
        quantity: 3
    }
];

show(calculateSubtotal(cart));
```

---

# 33. Complete Checkout Function

```pulsar
func calculateDiscount(subtotal) {
    if subtotal >= 1000 {
        return subtotal * 0.15;
    }

    if subtotal >= 500 {
        return subtotal * 0.10;
    }

    if subtotal >= 200 {
        return subtotal * 0.05;
    }

    return 0;
}

func checkout(subtotal) {
    define discount = calculateDiscount(subtotal);
    define total = subtotal - discount;

    return total;
}

show(checkout(1200));
```

---

# 34. Recursive `return`

A recursive function must eventually reach a condition that returns without making another recursive call.

```pulsar
func factorial(n) {
    if n <= 1 {
        return 1;
    }

    return n * factorial(n - 1);
}

show(factorial(5));
```

Output:

```text
120
```

---

# 35. Recursive Countdown

```pulsar
func countdown(n) {
    if n <= 0 {
        return;
    }

    show(n);

    return countdown(n - 1);
}

countdown(5);
```

---

# 36. Return an Array After Processing

```pulsar
func createValues() {
    define values = [];

    values.push(10);
    values.push(20);
    values.push(30);

    return values;
}

define result = createValues();

show(result);
```

---

# 37. Return an Object After Processing

```pulsar
func createProduct(name, price, stock) {
    define product = {
        name: name,
        price: price,
        stock: stock
    };

    return product;
}

define product = createProduct(
    "Mouse",
    40,
    20
);

show(product.name);
```

---

# 38. Returning From Nested Conditions

```pulsar
func classifyScore(score) {
    if score >= 90 {
        if score == 100 {
            return "Perfect";
        }

        return "A";
    }

    if score >= 80 {
        return "B";
    }

    return "Below B";
}

show(classifyScore(100));
```

---

# 39. Return and Local Variables

```pulsar
func calculate(a, b) {
    define sum = a + b;
    define product = a * b;

    return sum + product;
}

show(calculate(2, 3));
```

Output:

```text
11
```

---

# 40. Return From an Error Check

```pulsar
func divide(a, b) {
    if b == 0 {
        return null;
    }

    return a / b;
}

define result = divide(10, 2);

show(result);
```

---

# 41. Multiple Return Types

A function can return different kinds of values depending on its logic.

```pulsar
func result(value) {
    if value < 0 {
        return null;
    }

    if value == 0 {
        return false;
    }

    return value;
}
```

The exact runtime handling of different returned values depends on the corresponding Pulsar value semantics.

---

# 42. Return Used in an Assignment

```pulsar
func getPrice() {
    return 1200;
}

define price = getPrice();

show(price);
```

---

# 43. Return Used in Arithmetic

```pulsar
func price() {
    return 100;
}

define total = price() * 3;

show(total);
```

Output:

```text
300
```

---

# 44. Return Used in a Condition

```pulsar
func isLarge(value) {
    return value > 100;
}

if isLarge(200) {
    show("Large");
}
```

---

# 45. Return Used as a Function Argument

```pulsar
func add(a, b) {
    return a + b;
}

func double(value) {
    return value * 2;
}

show(double(add(10, 20)));
```

Output:

```text
60
```

---

# 46. Return From a Search

```pulsar
func findFirstPositive(values) {
    for value in values {
        if value > 0 {
            return value;
        }
    }

    return null;
}

define values = [
    -5,
    -10,
    20,
    30
];

show(findFirstPositive(values));
```

Output:

```text
20
```

---

# 47. Return From a `while` Search

```pulsar
func findFirstPositive(values) {
    define i = 0;

    while i < values.length {
        if values[i] > 0 {
            return values[i];
        }

        i++;
    }

    return null;
}

show(findFirstPositive([
    -10,
    -20,
    30
]));
```

---

# 48. Return After a Loop

```pulsar
func sum(values) {
    define total = 0;

    for value in values {
        total += value;
    }

    return total;
}

show(sum([
    10,
    20,
    30
]));
```

The loop completes first, then the function returns the accumulated value.

---

# 49. Return Before a Loop

```pulsar
func process(value) {
    if value == null {
        return null;
    }

    while value > 0 {
        show(value);
        value--;
    }

    return value;
}
```

The initial validation can prevent the loop from executing.

---

# 50. Complete Function Example

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

define cart = [];

func findProduct(id) {
    for product in products {
        if product.id == id {
            return product;
        }
    }

    return null;
}

func addProduct(id, quantity) {
    define product = findProduct(id);

    if product == null {
        return false;
    }

    if quantity <= 0 {
        return false;
    }

    if product.stock < quantity {
        return false;
    }

    cart.push({
        product: product,
        quantity: quantity
    });

    product.stock = product.stock - quantity;

    return true;
}

func calculateSubtotal() {
    define subtotal = 0;

    for item in cart {
        subtotal +=
            item.product.price *
            item.quantity;
    }

    return subtotal;
}

func calculateDiscount(subtotal) {
    if subtotal >= 1000 {
        return subtotal * 0.15;
    }

    if subtotal >= 500 {
        return subtotal * 0.10;
    }

    if subtotal >= 200 {
        return subtotal * 0.05;
    }

    return 0;
}

func calculateTotal() {
    define subtotal = calculateSubtotal();
    define discount = calculateDiscount(subtotal);

    return subtotal - discount;
}

addProduct(1, 1);
addProduct(2, 2);
addProduct(3, 2);

define subtotal = calculateSubtotal();
define total = calculateTotal();

show("Subtotal: $" + subtotal);
show("Total: $" + total);
```

This example demonstrates `return` throughout a realistic Pulsar program:

* returning objects
* returning `null`
* returning booleans
* returning numbers
* returning calculated expressions
* returning from loops
* returning from conditional branches
* using returned values in other function calls

---

# 51. `return` Control Flow

Conceptually:

```text
function starts
     |
     v
execute statements
     |
     v
return encountered?
   /       \
 yes        no
 |           |
 v           v
exit      continue
function   execution
 |
 v
caller receives value
```

`return` therefore has two effects when a value is supplied:

1. It terminates the current function.
2. It provides the value to the caller.

---

# 52. `return` Compared With Other Control Statements

| Statement       | Purpose                                            |
| --------------- | -------------------------------------------------- |
| `return value;` | End the current function and provide a value       |
| `return;`       | End the current function without an explicit value |
| `break;`        | End the current loop                               |
| `continue;`     | Skip to the next loop iteration                    |

Example:

```pulsar
func process(values) {
    for value in values {
        if value < 0 {
            continue;
        }

        if value == 0 {
            break;
        }

        if value == 100 {
            return value;
        }

        show(value);
    }

    return null;
}
```

---

# 53. Recommended Return Tests

```text
1. return without a value
2. return a number
3. return a string
4. return a boolean
5. return null
6. return an array
7. return an object
8. return a variable
9. return an expression
10. return from if
11. return from multiple branches
12. early return
13. return from while
14. return from for
15. return from for-in
16. return from nested loops
17. return from a search
18. return from validation
19. return from calculation
20. return from recursive function
21. return a function result
22. use return value in assignment
23. use return value in arithmetic
24. use return value in condition
25. pass return value to another function
26. return after processing an array
27. return an object from a function
28. return null when not found
29. return boolean for validation
30. complete shop program using return
```