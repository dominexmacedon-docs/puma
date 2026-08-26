## 1. Overview

Functions allow Pulsar programs to group reusable instructions under a name.

A function can:

* accept parameters
* execute statements
* create local variables
* contain conditionals
* contain loops
* return a value
* be called multiple times

The basic syntax is:

```pulsar
func functionName(parameters) {
    statements;
}
```

---

## 2. Basic Function

```pulsar
func greet() {
    show("Hello, Pulsar");
}

greet();
```

Output:

```text
Hello, Pulsar
```

---

## 3. Function With a Parameter

```pulsar
func greet(name) {
    show("Hello, " + name);
}

greet("Alice");
```

Output:

```text
Hello, Alice
```

---

## 4. Multiple Parameters

```pulsar
func add(a, b) {
    return a + b;
}

show(add(10, 20));
```

Output:

```text
30
```

---

## 5. Returning a Value

A function can use `return` to send a value back to its caller.

```pulsar
func square(value) {
    return value * value;
}

define result = square(5);

show(result);
```

Output:

```text
25
```

---

## 6. Function Without `return`

A function does not have to explicitly return a value.

```pulsar
func message() {
    show("Pulsar");
}

message();
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

---

## 8. Arithmetic Function

```pulsar
func multiply(a, b) {
    return a * b;
}

show(multiply(6, 7));
```

Output:

```text
42
```

---

## 9. Subtraction Function

```pulsar
func subtract(a, b) {
    return a - b;
}

show(subtract(20, 8));
```

Output:

```text
12
```

---

## 10. Division Function

```pulsar
func divide(a, b) {
    return a / b;
}

show(divide(20, 4));
```

Output:

```text
5
```

---

## 11. Function With Local Variables

```pulsar
func calculateTotal(price, quantity) {
    define total = price * quantity;

    return total;
}

show(calculateTotal(50, 3));
```

The variable `total` is created inside the function.

---

## 12. Multiple Local Variables

```pulsar
func calculate(a, b) {
    define sum = a + b;
    define difference = a - b;
    define result = sum * difference;

    return result;
}

show(calculate(10, 4));
```

---

## 13. Function Calling Another Function

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

## 14. Function With Conditional Logic

```pulsar
func checkAge(age) {
    if age >= 18 {
        return "Adult";
    }

    return "Minor";
}

show(checkAge(20));
```

---

## 15. Multiple `return` Paths

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

## 16. Function With a Loop

```pulsar
func countTo(limit) {
    define i = 1;

    while i <= limit {
        show(i);
        i++;
    }
}

countTo(5);
```

---

## 17. Function With `for`

```pulsar
func countTo(limit) {
    for (define i = 1; i <= limit; i++) {
        show(i);
    }
}

countTo(5);
```

---

## 18. Function With `for ... in`

```pulsar
func printValues(values) {
    for value in values {
        show(value);
    }
}

define values = [
    10,
    20,
    30
];

printValues(values);
```

---

## 19. Function With `break`

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

---

## 20. Function With `continue`

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

---

## 21. Function Returning an Array

```pulsar
func createNumbers() {
    return [
        10,
        20,
        30
    ];
}

define numbers = createNumbers();

show(numbers);
```

---

## 22. Function Returning an Object

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

## 23. Function Accepting an Array

```pulsar
func sum(values) {
    define total = 0;

    for value in values {
        total += value;
    }

    return total;
}

define numbers = [
    10,
    20,
    30
];

show(sum(numbers));
```

Output:

```text
60
```

---

## 24. Function Accepting an Object

```pulsar
func getName(user) {
    return user.name;
}

define user = {
    name: "Alice",
    age: 20
};

show(getName(user));
```

---

## 25. Function Returning a Boolean

```pulsar
func isPositive(value) {
    return value > 0;
}

show(isPositive(10));
show(isPositive(-5));
```

---

## 26. Function for Validation

```pulsar
func isValidQuantity(quantity) {
    if quantity <= 0 {
        return false;
    }

    return true;
}

show(isValidQuantity(5));
```

---

## 27. Function With Multiple Conditions

```pulsar
func grade(score) {
    if score >= 90 {
        return "A";
    }

    if score >= 80 {
        return "B";
    }

    if score >= 70 {
        return "C";
    }

    return "F";
}

show(grade(85));
```

---

## 28. Function With String Processing

```pulsar
func welcome(name) {
    return "Welcome, " + name;
}

show(welcome("Pulsar"));
```

---

## 29. Function With a Counter

```pulsar
func countEven(limit) {
    define count = 0;
    define i = 1;

    while i <= limit {
        if i % 2 == 0 {
            count++;
        }

        i++;
    }

    return count;
}

show(countEven(10));
```

Output:

```text
5
```

---

## 30. Function for Maximum

```pulsar
func maximum(a, b) {
    if a > b {
        return a;
    }

    return b;
}

show(maximum(20, 10));
```

---

## 31. Function for Minimum

```pulsar
func minimum(a, b) {
    if a < b {
        return a;
    }

    return b;
}

show(minimum(20, 10));
```

---

## 32. Recursive Function

A function can call itself.

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

## 33. Recursive Countdown

```pulsar
func countdown(n) {
    if n <= 0 {
        return;
    }

    show(n);

    countdown(n - 1);
}

countdown(5);
```

---

## 34. Function With Calculations

```pulsar
func calculateDiscount(price, rate) {
    define discount = price * rate;
    return discount;
}

show(calculateDiscount(1000, 0.10));
```

---

## 35. Shop Function

```pulsar
func calculateSubtotal(price, quantity) {
    return price * quantity;
}

define subtotal = calculateSubtotal(1200, 2);

show("Subtotal: $" + subtotal);
```

---

## 36. Product Lookup Function

```pulsar
define products = [
    {
        id: 1,
        name: "Laptop",
        price: 1200
    },
    {
        id: 2,
        name: "Keyboard",
        price: 80
    },
    {
        id: 3,
        name: "Mouse",
        price: 40
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

define product = findProduct(2);

if product == null {
    show("Product not found");
} else {
    show(product.name);
}
```

---

## 37. Function With a Local Search Variable

```pulsar
func findName(names, target) {
    define result = null;

    for name in names {
        if name == target {
            result = name;
            break;
        }
    }

    return result;
}

define names = [
    "Alice",
    "Bob",
    "Charlie"
];

show(findName(names, "Bob"));
```

---

## 38. Function Returning a Calculated Object

```pulsar
func createProduct(name, price) {
    return {
        name: name,
        price: price
    };
}

define product = createProduct("Mouse", 40);

show(product.name);
show(product.price);
```

---

## 39. Function With Multiple Calls

```pulsar
func square(value) {
    return value * value;
}

show(square(2));
show(square(3));
show(square(4));
show(square(5));
```

---

## 40. Reusing a Function

```pulsar
func calculateTotal(price, quantity) {
    return price * quantity;
}

define laptopTotal = calculateTotal(1200, 2);
define mouseTotal = calculateTotal(40, 3);

show(laptopTotal);
show(mouseTotal);
```

---

# 41. Function Scope

Variables created inside a function are local to that function's execution.

```pulsar
func test() {
    define value = 100;

    show(value);
}

test();
```

The supplied function examples use local variables inside function bodies, such as `total`, `i`, and `count`. 

---

# 42. Parameters

Parameters are names declared between the parentheses following the function name.

```pulsar
func add(a, b) {
    return a + b;
}
```

Here:

```text
a
b
```

are parameters.

When called:

```pulsar
add(10, 20);
```

the supplied arguments are used by the function.

---

# 43. Function Call

The general function-call form is:

```pulsar
functionName(arguments);
```

Example:

```pulsar
func greet(name) {
    show("Hello " + name);
}

greet("Alice");
```

---

# 44. Function Call Inside an Expression

A returned value can be used as part of another expression.

```pulsar
func add(a, b) {
    return a + b;
}

define result = add(10, 20) * 2;

show(result);
```

Output:

```text
60
```

---

# 45. Function Call Inside a Condition

```pulsar
func isAdult(age) {
    return age >= 18;
}

if isAdult(20) {
    show("Allowed");
} else {
    show("Not allowed");
}
```

---

# 46. Function Call Inside a Loop

```pulsar
func square(value) {
    return value * value;
}

for (define i = 1; i <= 5; i++) {
    show(square(i));
}
```

---

# 47. Function Calling Another Function

```pulsar
func add(a, b) {
    return a + b;
}

func calculate(a, b, multiplier) {
    define result = add(a, b);

    return result * multiplier;
}

show(calculate(10, 20, 2));
```

Output:

```text
60
```

---

# 48. Complete Shop Example

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
        show("Product does not exist");
        return;
    }

    if quantity <= 0 {
        show("Invalid quantity");
        return;
    }

    if product.stock < quantity {
        show("Insufficient stock");
        return;
    }

    cart.push({
        product: product,
        quantity: quantity
    });

    product.stock = product.stock - quantity;
}

func calculateSubtotal() {
    define subtotal = 0;

    for item in cart {
        subtotal =
            subtotal +
            item.product.price * item.quantity;
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

func checkout() {
    define subtotal = calculateSubtotal();
    define discount = calculateDiscount(subtotal);
    define total = subtotal - discount;

    show("=== CHECKOUT ===");
    show("Subtotal: $" + subtotal);
    show("Discount: $" + discount);
    show("Total: $" + total);
}

addProduct(1, 1);
addProduct(2, 2);
addProduct(3, 2);

checkout();
```

This example combines the major function concepts:

* function declarations
* parameters
* return values
* local variables
* function calls
* nested function calls
* loops
* `break`
* conditionals
* arrays
* objects
* mutation
* `null`
* arithmetic

---

# 49. Function Structure

The general structure is:

```pulsar
func name(parameters) {
    statements;
    return value;
}
```

For example:

```pulsar
func calculate(a, b) {
    define result = a + b;

    return result;
}
```

---

# 50. Recommended Function Tests

```text
1. Function without parameters
2. Function with one parameter
3. Function with multiple parameters
4. Function returning a number
5. Function returning a string
6. Function returning a boolean
7. Function returning null
8. Function returning an array
9. Function returning an object
10. Function with local variables
11. Function with if
12. Function with if/else
13. Function with while
14. Function with for
15. Function with for-in
16. Function with break
17. Function with continue
18. Function calling another function
19. Function called multiple times
20. Function used in an expression
21. Function used in a condition
22. Function used inside a loop
23. Recursive function
24. Search function
25. Calculation function
26. Validation function
27. Product lookup function
28. Cart calculation function
29. Discount function
30. Complete shop program
```
