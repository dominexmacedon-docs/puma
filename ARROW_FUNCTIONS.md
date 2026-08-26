## 1. Overview

Pulsar supports arrow functions as a compact way to create functions and assign them to variables.

The basic syntax is:

```pulsar
define functionName = parameter => expression;
```

For multiple parameters:

```pulsar
define functionName = (parameter1, parameter2) => expression;
```

The supplied Pulsar examples explicitly demonstrate single-parameter arrow functions, multiple-parameter arrow functions, expressions, array indexing, object properties, and use with `map`, `filter`, and `reduce`.  

---

## 2. Single Parameter

A single parameter does not require parentheses.

```pulsar
define double = x => x * 2;

show(double(5));
```

Output:

```text
10
```

---

## 3. Square

```pulsar
define square = x => x * x;

show(square(6));
```

Output:

```text
36
```

---

## 4. Multiple Parameters

Multiple parameters are enclosed in parentheses.

```pulsar
define add = (a, b) => a + b;

show(add(2, 8));
```

Output:

```text
10
```

---

## 5. String Return

```pulsar
define greet = name => "Hello " + name;

show(greet("Pulsar"));
```

Output:

```text
Hello Pulsar
```

---

## 6. Boolean Return

```pulsar
define isEven = x => x % 2 == 0;

show(isEven(10));
```

Output:

```text
true
```

---

## 7. Negative Values

```pulsar
define negate = x => -x;

show(negate(5));
```

Output:

```text
-5
```

---

## 8. Array Access

```pulsar
define first = x => x[0];

show(first([10, 20]));
```

The supplied examples use this exact arrow-function pattern. 

---

## 9. Object Property Access

```pulsar
define getName = user => user.name;

show(getName({
    name: "Pulsar"
}));
```

Output:

```text
Pulsar
```

---

## 10. Multiple Parameters With an Expression

```pulsar
define calculate = (a, b) => (a + b) * 2;

show(calculate(3, 4));
```

Output:

```text
14
```

---

## 11. Identity Function

An identity function returns its input unchanged.

```pulsar
define identity = x => x;

show(identity("Pulsar"));
```

Output:

```text
Pulsar
```

---

## 12. Assigning an Arrow Function

Arrow functions can be assigned to variables using `define`.

```pulsar
define multiply = (a, b) => a * b;

define result = multiply(6, 7);

show(result);
```

Output:

```text
42
```

---

## 13. Reusing an Arrow Function

```pulsar
define double = x => x * 2;

show(double(5));
show(double(10));
show(double(20));
```

Output:

```text
10
20
40
```

---

## 14. Arrow Function With a Variable

```pulsar
define factor = 10;

define multiply = x => x * factor;

show(multiply(5));
```

The supplied function-scope examples also demonstrate functions reading values from an outer scope. 

---

# 15. Arrow Functions With `map`

Arrow functions are particularly useful with `map`.

```pulsar
define values = [
    1,
    2,
    3
];

show(map(values, x => x * 2));
```

Output:

```text
[2, 4, 6]
```

The supplied examples explicitly use this form. 

---

## 16. Map and Square

```pulsar
define values = [
    2,
    3,
    4
];

show(map(values, x => x * x));
```

Output:

```text
[4, 9, 16]
```

---

## 17. Map and Strings

```pulsar
define names = [
    "alice",
    "bob",
    "charlie"
];

show(map(names, x => upper(x)));
```

---

## 18. Map and Object Properties

```pulsar
define users = [
    {
        name: "Alice"
    },
    {
        name: "Bob"
    },
    {
        name: "Charlie"
    }
];

show(map(users, user => user.name));
```

---

# 19. Arrow Functions With `filter`

Arrow functions can also be used to determine which values remain in an array.

```pulsar
define values = [
    1,
    2,
    3,
    4
];

show(filter(values, x => x % 2 == 0));
```

Output:

```text
[2, 4]
```

The supplied examples explicitly demonstrate `filter` with arrow functions. 

---

## 20. Filter Values Greater Than a Limit

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

show(filter(values, x => x > 3));
```

Output:

```text
[4, 5]
```

---

## 21. Filter Odd Numbers

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5,
    6
];

show(filter(values, x => x % 2 != 0));
```

Output:

```text
[1, 3, 5]
```

---

## 22. Filter Objects

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
        stock: 20
    }
];

define available = filter(
    products,
    product => product.stock > 0
);

show(available);
```

---

# 23. Arrow Functions With `reduce`

Arrow functions can be used with `reduce` to combine array values.

```pulsar
define values = [
    1,
    2,
    3,
    4
];

show(reduce(
    values,
    (a, b) => a + b,
    0
));
```

Output:

```text
10
```

The supplied examples demonstrate `reduce` with a two-parameter arrow function and an initial value. 

---

## 24. Reduce Product

```pulsar
define values = [
    2,
    3,
    4
];

show(reduce(
    values,
    (a, b) => a * b,
    1
));
```

Output:

```text
24
```

---

# 25. Map, Filter, and Reduce Together

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

define doubled = map(
    values,
    x => x * 2
);

define large = filter(
    doubled,
    x => x > 5
);

define total = reduce(
    large,
    (a, b) => a + b,
    0
);

show(total);
```

---

# 26. Arrow Function Compared With `func`

Traditional function:

```pulsar
func double(x) {
    return x * 2;
}
```

Arrow function:

```pulsar
define double = x => x * 2;
```

Both express reusable function behavior, but the arrow form is more compact for a single expression.

The supplied examples establish the traditional `func` form separately from the arrow-function form.  

---

# 27. Arithmetic Arrow Functions

```pulsar
define add = (a, b) => a + b;
define subtract = (a, b) => a - b;
define multiply = (a, b) => a * b;
define divide = (a, b) => a / b;

show(add(10, 5));
show(subtract(10, 5));
show(multiply(10, 5));
show(divide(10, 5));
```

---

# 28. Comparison Arrow Functions

```pulsar
define greater = (a, b) => a > b;
define smaller = (a, b) => a < b;
define equal = (a, b) => a == b;

show(greater(10, 5));
show(smaller(10, 5));
show(equal(10, 10));
```

---

# 29. Boolean Arrow Functions

```pulsar
define isPositive = x => x > 0;
define isNegative = x => x < 0;
define isZero = x => x == 0;

show(isPositive(10));
show(isNegative(-10));
show(isZero(0));
```

---

# 30. String Arrow Functions

```pulsar
define makeGreeting = name => "Hello, " + name;

show(makeGreeting("Developer"));
```

---

# 31. Array Arrow Functions

```pulsar
define lengthOf = values => len(values);

show(lengthOf([
    10,
    20,
    30
]));
```

---

# 32. Object Arrow Functions

```pulsar
define getPrice = product => product.price;

define product = {
    name: "Laptop",
    price: 1200
};

show(getPrice(product));
```

---

# 33. Nested Property Access

```pulsar
define getCity = user => user.address.city;

define user = {
    address: {
        city: "Mandalay"
    }
};

show(getCity(user));
```

---

# 34. Arrow Function Returning an Array

```pulsar
define makePair = x => [
    x,
    x * 2
];

show(makePair(10));
```

---

# 35. Arrow Function Returning an Object

```pulsar
define makePoint = (x, y) => {
    x: x,
    y: y
};

show(makePoint(10, 20));
```

If object-return syntax is ambiguous in a particular parser version, use an ordinary `func` form instead. The supplied arrow-function examples specifically document expression-bodied arrows rather than a block-bodied object-return form. 

---

# 36. Arrow Function in a Variable Calculation

```pulsar
define tax = price => price * 0.10;

define price = 100;

show(tax(price));
```

---

# 37. Arrow Function for Discounts

```pulsar
define discount = price => price * 0.15;

show(discount(1000));
```

---

# 38. Arrow Function for Final Price

```pulsar
define finalPrice = (price, discount) =>
    price - discount;

show(finalPrice(1000, 100));
```

---

# 39. Arrow Function for Product Price

```pulsar
define subtotal = item =>
    item.price * item.quantity;

define item = {
    price: 50,
    quantity: 3
};

show(subtotal(item));
```

---

# 40. Arrow Function for Product Availability

```pulsar
define available =
    product => product.stock > 0;

define product = {
    name: "Mouse",
    stock: 20
};

show(available(product));
```

---

# 41. Product Filtering

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

define cheap = filter(
    products,
    product => product.price < 100
);

show(cheap);
```

---

# 42. Product Mapping

```pulsar
define products = [
    {
        name: "Laptop",
        price: 1200
    },
    {
        name: "Keyboard",
        price: 80
    }
];

define prices = map(
    products,
    product => product.price
);

show(prices);
```

---

# 43. Product Total

```pulsar
define products = [
    {
        price: 100
    },
    {
        price: 200
    },
    {
        price: 300
    }
];

define total = reduce(
    products,
    (sum, product) => sum + product.price,
    0
);

show(total);
```

---

# 44. Transforming Data

```pulsar
define values = [
    10,
    20,
    30
];

define result = map(
    values,
    x => x + 5
);

show(result);
```

Output:

```text
[15, 25, 35]
```

---

# 45. Filtering Then Mapping

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5,
    6
];

define even = filter(
    values,
    x => x % 2 == 0
);

define doubled = map(
    even,
    x => x * 2
);

show(doubled);
```

---

# 46. Mapping Then Reducing

```pulsar
define values = [
    1,
    2,
    3,
    4
];

define squares = map(
    values,
    x => x * x
);

define total = reduce(
    squares,
    (a, b) => a + b,
    0
);

show(total);
```

Output:

```text
30
```

---

# 47. Arrow Function as a Callback

```pulsar
define values = [
    1,
    2,
    3
];

define result = map(
    values,
    x => x * 10
);

show(result);
```

Here:

```pulsar
x => x * 10
```

is passed as a function value to `map`.

---

# 48. Multiple Arrow Functions

```pulsar
define double = x => x * 2;
define square = x => x * x;
define cube = x => x * x * x;

show(double(5));
show(square(5));
show(cube(5));
```

---

# 49. Passing an Arrow Function Through a Variable

```pulsar
define operation = x => x * 3;

define values = [
    1,
    2,
    3
];

show(map(values, operation));
```

---

# 50. Complete Arrow Function Example

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
        stock: 0
    },
    {
        name: "Monitor",
        price: 300,
        stock: 3
    }
];

define available =
    filter(
        products,
        product => product.stock > 0
    );

define prices =
    map(
        available,
        product => product.price
    );

define total =
    reduce(
        prices,
        (a, b) => a + b,
        0
    );

show(available);
show(prices);
show(total);
```

---

# 51. Syntax Summary

### One parameter

```pulsar
define double = x => x * 2;
```

### Multiple parameters

```pulsar
define add = (a, b) => a + b;
```

### String expression

```pulsar
define greet = name => "Hello " + name;
```

### Boolean expression

```pulsar
define isEven = x => x % 2 == 0;
```

### Array access

```pulsar
define first = x => x[0];
```

### Object property access

```pulsar
define getName = user => user.name;
```

### Complex expression

```pulsar
define calculate = (a, b) => (a + b) * 2;
```

These forms are directly represented in the supplied Pulsar examples. 

---

# 52. Arrow Functions With Collection Operations

The most important practical use in the supplied language examples is combining arrow functions with collection operations:

```pulsar
define values = [
    1,
    2,
    3,
    4
];

define doubled = map(
    values,
    x => x * 2
);

define even = filter(
    doubled,
    x => x % 2 == 0
);

define total = reduce(
    even,
    (a, b) => a + b,
    0
);

show(total);
```

The supplied examples explicitly establish arrow functions as callbacks for `map`, `filter`, and `reduce`. 

---

# 53. Recommended Tests

```text
1. Single-parameter arrow function
2. Multiple-parameter arrow function
3. Arithmetic expression
4. String expression
5. Boolean expression
6. Negative expression
7. Array indexing
8. Object property access
9. Identity function
10. Function stored in a variable
11. Function called multiple times
12. Arrow function with outer variable
13. Arrow function with map
14. Arrow function with filter
15. Arrow function with reduce
16. Map and object properties
17. Filter objects
18. Reduce objects
19. Multiple arrow functions
20. Arrow functions in a complete program
```