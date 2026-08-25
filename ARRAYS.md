## 1. Overview

Arrays are ordered collections of values in Pulsar.

An array can contain numbers, strings, booleans, objects, `null`, or other arrays.

```pulsar
define numbers = [
    10,
    20,
    30
];

show(numbers);
```

Arrays can also contain mixed values:

```pulsar
define values = [
    10,
    "Pulsar",
    true,
    null
];

show(values);
```

The supplied examples explicitly use arrays containing mixed values, including `true` and `null`. 

---

# 2. Empty Array

An empty array contains no elements.

```pulsar
define values = [];

show(values);
```

The interpreter's `isEmpty()` builtin recognizes an empty array by checking its length. 

---

# 3. Array Literal

The basic array syntax is:

```pulsar
[
    value1,
    value2,
    value3
]
```

For example:

```pulsar
define fruits = [
    "Apple",
    "Banana",
    "Orange"
];

show(fruits);
```

---

# 4. Number Array

```pulsar
define numbers = [
    10,
    20,
    30,
    40,
    50
];

show(numbers);
```

---

# 5. String Array

```pulsar
define names = [
    "Pulsar",
    "Dominex",
    "Developer"
];

show(names);
```

---

# 6. Boolean Array

```pulsar
define states = [
    true,
    false,
    true
];

show(states);
```

---

# 7. Null Array

```pulsar
define values = [
    null,
    null,
    "Pulsar"
];

show(values);
```

---

# 8. Mixed Array

```pulsar
define values = [
    10,
    "Pulsar",
    true,
    null
];

show(values);
```

---

# 9. Nested Array

Arrays can contain other arrays.

```pulsar
define matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

show(matrix);
```

---

# 10. Array of Objects

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

show(products);
```

---

# 11. Array Indexing

Array elements can be accessed with square brackets.

The supplied examples use zero-based indexing:

```pulsar
define values = [
    10,
    20
];

show(values[0]);
show(values[1]);
```

The supplied arrow-function example explicitly uses `x[0]` to retrieve the first array element. 

---

# 12. First Element

```pulsar
define fruits = [
    "Apple",
    "Banana",
    "Orange"
];

define first = fruits[0];

show(first);
```

---

# 13. Last Element

Using the array's length:

```pulsar
define fruits = [
    "Apple",
    "Banana",
    "Orange"
];

define last =
    fruits[fruits.length - 1];

show(last);
```

---

# 14. Assigning an Array Element

An existing array element can be replaced.

```pulsar
define numbers = [
    10,
    20,
    30
];

numbers[1] = 200;

show(numbers);
```

---

# 15. Changing a String Element

```pulsar
define names = [
    "Alice",
    "Bob",
    "Charlie"
];

names[0] = "Alex";

show(names);
```

---

# 16. Array Length

The array's `length` property can be accessed.

```pulsar
define numbers = [
    10,
    20,
    30
];

show(numbers.length);
```

---

# 17. Empty Array Length

```pulsar
define values = [];

show(values.length);
```

An empty array has a length of zero.

---

# 18. Adding With `push()`

Pulsar provides the `push()` builtin.

```pulsar
define numbers = [
    10,
    20
];

push(numbers, 30);

show(numbers);
```

The interpreter implementation requires the first argument to be an array, appends the value, and returns the new array length. 

---

# 19. `push()` Return Value

```pulsar
define numbers = [
    10,
    20
];

define length =
    push(numbers, 30);

show(length);
```

`push()` returns the resulting array length. 

---

# 20. Multiple `push()` Calls

```pulsar
define values = [];

push(values, 10);
push(values, 20);
push(values, 30);

show(values);
```

---

# 21. Pushing Objects

```pulsar
define users = [];

push(users, {
    name: "Pulsar",
    active: true
});

show(users);
```

---

# 22. Pushing Arrays

```pulsar
define values = [];

push(values, [1, 2, 3]);
push(values, [4, 5, 6]);

show(values);
```

---

# 23. Removing With `pop()`

`pop()` removes and returns the last array element.

```pulsar
define numbers = [
    10,
    20,
    30
];

define value =
    pop(numbers);

show(value);
show(numbers);
```

The evaluator directly implements `pop()` using the array's last-element removal operation. 

---

# 24. `pop()` From an Empty Array

```pulsar
define values = [];

define result =
    pop(values);

show(result);
```

The underlying array operation determines the resulting value.

---

# 25. Removing With `shift()`

`shift()` removes and returns the first element.

```pulsar
define numbers = [
    10,
    20,
    30
];

define value =
    shift(numbers);

show(value);
show(numbers);
```

The evaluator implements `shift()` directly on arrays. 

---

# 26. Adding With `unshift()`

`unshift()` adds a value to the beginning of an array.

```pulsar
define numbers = [
    20,
    30
];

unshift(numbers, 10);

show(numbers);
```

The builtin returns the resulting array length. 

---

# 27. `unshift()` Return Value

```pulsar
define numbers = [
    20,
    30
];

define length =
    unshift(numbers, 10);

show(length);
```

---

# 28. Queue Example

`push()` and `shift()` can be combined to create a simple queue.

```pulsar
define queue = [];

push(queue, "First");
push(queue, "Second");
push(queue, "Third");

define next =
    shift(queue);

show(next);
```

---

# 29. Stack Example

`push()` and `pop()` can be combined to create a stack.

```pulsar
define stack = [];

push(stack, "First");
push(stack, "Second");
push(stack, "Third");

define top =
    pop(stack);

show(top);
```

---

# 30. `indexOf()`

Pulsar provides `indexOf()` for searching an array.

```pulsar
define fruits = [
    "Apple",
    "Banana",
    "Orange"
];

define index =
    indexOf(fruits, "Banana");

show(index);
```

The interpreter implements `indexOf()` using the array's `indexOf` operation. 

---

# 31. Searching for a Missing Value

```pulsar
define fruits = [
    "Apple",
    "Banana"
];

define index =
    indexOf(fruits, "Orange");

show(index);
```

The underlying array search determines the returned index for a missing element.

---

# 32. `includesArr()`

`includesArr()` tests whether an array contains a value.

```pulsar
define fruits = [
    "Apple",
    "Banana",
    "Orange"
];

define exists =
    includesArr(fruits, "Banana");

show(exists);
```

The evaluator implements this with the array's `includes` operation. 

---

# 33. Missing Array Value

```pulsar
define fruits = [
    "Apple",
    "Banana"
];

show(
    includesArr(fruits, "Orange")
);
```

---

# 34. `unique()`

`unique()` removes duplicate values.

```pulsar
define numbers = [
    1,
    2,
    2,
    3,
    3,
    3
];

define result =
    unique(numbers);

show(result);
```

The interpreter implements `unique()` by constructing a `Set` and converting it back into an array. 

---

# 35. Unique Strings

```pulsar
define names = [
    "Pulsar",
    "Pulsar",
    "Dominex",
    "Pulsar"
];

show(unique(names));
```

---

# 36. `flatten()`

`flatten()` combines nested arrays into a single array.

```pulsar
define values = [
    [1, 2],
    [3, 4],
    [5, 6]
];

define result =
    flatten(values);

show(result);
```

The interpreter uses recursive array flattening. 

---

# 37. Deeply Nested Arrays

```pulsar
define values = [
    1,
    [2, [3, [4]]]
];

show(flatten(values));
```

The supplied implementation uses infinite-depth flattening, so nested arrays are flattened recursively. 

---

# 38. `randomChoice()`

`randomChoice()` returns an element selected from an array.

```pulsar
define colors = [
    "Red",
    "Green",
    "Blue"
];

define color =
    randomChoice(colors);

show(color);
```

The interpreter selects an array element using a random index. 

---

# 39. Random Item From Numbers

```pulsar
define numbers = [
    10,
    20,
    30,
    40,
    50
];

show(randomChoice(numbers));
```

---

# 40. `sort()`

Pulsar provides `sort()` for arrays.

```pulsar
define numbers = [
    5,
    2,
    8,
    1,
    3
];

define result =
    sort(numbers);

show(result);
```

The evaluator uses the array sorting operation when no comparator function is supplied. 

---

# 41. Sorting With a Function

The `sort()` builtin accepts an optional function.

```pulsar
define numbers = [
    5,
    2,
    8,
    1,
    3
];

define result =
    sort(numbers, (a, b) => a - b);

show(result);
```

The evaluator checks whether the second argument is a function and passes it to the underlying sort operation. 

---

# 42. `reverse()`

`reverse()` reverses an array.

```pulsar
define numbers = [
    1,
    2,
    3,
    4
];

define result =
    reverse(numbers);

show(result);
```

The interpreter implements `reverse()` directly using the array's reverse operation. 

---

# 43. Reverse Strings Array

```pulsar
define names = [
    "Alice",
    "Bob",
    "Charlie"
];

reverse(names);

show(names);
```

---

# 44. `isEmpty()` With Arrays

```pulsar
define values = [];

show(isEmpty(values));
```

The supplied interpreter checks `Array.isArray(arg)` and then uses the array's length to determine whether it is empty. 

---

# 45. Non-Empty Array

```pulsar
define values = [
    10
];

show(isEmpty(values));
```

---

# 46. Looping Through an Array

Pulsar supports `for ... in` iteration over arrays.

```pulsar
define numbers = [
    10,
    20,
    30
];

for number in numbers {
    show(number);
}
```

The interpreter's `ForInStatement` handling detects arrays and iterates through their values.

---

# 47. Array of Names

```pulsar
define names = [
    "Alice",
    "Bob",
    "Charlie"
];

for name in names {
    show(name);
}
```

---

# 48. Array of Objects

```pulsar
define products = [
    {
        name: "Laptop",
        price: 1200
    },
    {
        name: "Mouse",
        price: 40
    }
];

for product in products {
    show(product.name);
}
```

---

# 49. Nested Array Iteration

```pulsar
define matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
];

for row in matrix {
    show(row);
}
```

---

# 50. Array Accumulation

```pulsar
define numbers = [
    10,
    20,
    30
];

define total = 0;

for number in numbers {
    total = total + number;
}

show(total);
```

---

# 51. Array Search

```pulsar
define products = [
    {
        id: 1,
        name: "Laptop"
    },
    {
        id: 2,
        name: "Mouse"
    }
];

define found = null;

for product in products {
    if product.id == 2 {
        found = product;
        break;
    }
}

show(found);
```

---

# 52. Array Filtering With `filter()`

The supplied interpreter's examples use arrow functions as boolean predicates for array processing.

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

The supplied examples explicitly demonstrate the boolean arrow-function pattern used for predicates. 

---

# 53. Filtering Positive Numbers

```pulsar
define numbers = [
    -3,
    -1,
    0,
    2,
    5
];

define positive =
    filter(numbers, x => x > 0);

show(positive);
```

---

# 54. Mapping an Array

A mapping operation can transform every array element.

```pulsar
define numbers = [
    1,
    2,
    3
];

define doubled =
    map(numbers, x => x * 2);

show(doubled);
```

---

# 55. Mapping to Booleans

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

# 56. Mapping Objects

```pulsar
define users = [
    {
        name: "Alice"
    },
    {
        name: "Bob"
    }
];

define names =
    map(users, user => user.name);

show(names);
```

---

# 57. Reducing an Array

An array can be reduced to a single value.

```pulsar
define numbers = [
    10,
    20,
    30
];

define total =
    reduce(numbers, (sum, value) => sum + value, 0);

show(total);
```

Use the exact `reduce()` signature implemented by the interpreter version being documented.

---

# 58. Array With Arrow Functions

The supplied examples explicitly demonstrate array indexing from an arrow function:

```pulsar
define first = x => x[0];

show(first([10, 20]));
```

This demonstrates that arrays can be passed directly to functions and indexed inside them. 

---

# 59. Array Function

```pulsar
func first(values) {
    return values[0];
}

define numbers = [
    100,
    200,
    300
];

show(first(numbers));
```

---

# 60. Returning an Array

Functions can return arrays.

```pulsar
func makeNumbers() {
    return [
        10,
        20,
        30
    ];
}

define values =
    makeNumbers();

show(values);
```

---

# 61. Passing an Array to a Function

```pulsar
func printAll(values) {
    for value in values {
        show(value);
    }
}

printAll([
    "A",
    "B",
    "C"
]);
```

---

# 62. Array Parameter Mutation

Because arrays are mutable values, functions can modify an array passed to them.

```pulsar
func addValue(values, value) {
    push(values, value);
}

define numbers = [
    1,
    2
];

addValue(numbers, 3);

show(numbers);
```

---

# 63. Array of Arrays

```pulsar
define table = [
    ["A", "B"],
    ["C", "D"]
];

show(table[0]);
show(table[1]);
```

---

# 64. Nested Indexing

```pulsar
define matrix = [
    [10, 20],
    [30, 40]
];

show(matrix[0][1]);
```

---

# 65. Array of Records

```pulsar
define users = [
    {
        id: 1,
        name: "Alice"
    },
    {
        id: 2,
        name: "Bob"
    }
];

show(users[0].name);
```

---

# 66. Array Mutation Through an Object

```pulsar
define users = [
    {
        name: "Alice",
        active: true
    }
];

users[0].active = false;

show(users[0].active);
```

---

# 67. Array Used as a Shopping Cart

```pulsar
define cart = [];

push(cart, {
    product: "Laptop",
    quantity: 1
});

push(cart, {
    product: "Mouse",
    quantity: 2
});

show(cart);
```

---

# 68. Removing a Cart Item

```pulsar
define cart = [
    {
        product: "Laptop"
    },
    {
        product: "Mouse"
    }
];

define removed =
    pop(cart);

show(removed);
show(cart);
```

---

# 69. Product Search

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

func findProduct(id) {
    for product in products {
        if product.id == id {
            return product;
        }
    }

    return null;
}

show(findProduct(2));
```

---

# 70. Array Validation

```pulsar
define values = [
    10,
    20,
    30
];

if isEmpty(values) {
    show("No values");
} else {
    show("Values available");
}
```

---

# 71. Array Type Errors

Array-specific builtins validate their arguments.

For example:

```pulsar
push("hello", 10);
```

is invalid because `push()` expects an array.

The evaluator explicitly throws:

```text
push() expects an array
```

when its first argument is not an array. 

Likewise, `pop()`, `shift()`, `unshift()`, `sort()`, `reverse()`, `unique()`, `indexOf()`, `includesArr()`, `flatten()`, and `randomChoice()` validate that their array argument is actually an array.  

---

# 72. Array Utility Reference

| Function                  | Purpose                       |
| ------------------------- | ----------------------------- |
| `push(arr, value)`        | Add value to the end          |
| `pop(arr)`                | Remove and return last value  |
| `shift(arr)`              | Remove and return first value |
| `unshift(arr, value)`     | Add value to the beginning    |
| `sort(arr)`               | Sort array                    |
| `sort(arr, fn)`           | Sort using a function         |
| `reverse(arr)`            | Reverse array                 |
| `unique(arr)`             | Remove duplicate values       |
| `indexOf(arr, value)`     | Find value index              |
| `includesArr(arr, value)` | Test whether value exists     |
| `flatten(arr)`            | Flatten nested arrays         |
| `randomChoice(arr)`       | Select a random element       |
| `isEmpty(arr)`            | Test whether array is empty   |

These functions are directly represented in the supplied evaluator.  

---

# 73. Array Property Reference

| Syntax           | Meaning                                  |
| ---------------- | ---------------------------------------- |
| `values[0]`      | First element                            |
| `values[index]`  | Element at an index                      |
| `values.length`  | Number of elements                       |
| `values[0][1]`   | Nested array access                      |
| `values[0].name` | Property of an object stored in an array |

The supplied examples explicitly demonstrate zero-based array indexing and accessing object properties from array elements. 

---

# 74. Array Processing Pattern

A common Pulsar pattern is:

```pulsar
define values = [
    1,
    2,
    3,
    4,
    5
];

define result =
    filter(
        values,
        x => x % 2 == 0
    );

show(result);
```

The array supplies values, while the arrow function determines which values are selected.

---

# 75. Complete Array Example

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
        return;
    }

    if product.stock < quantity {
        return;
    }

    push(cart, {
        product: product,
        quantity: quantity
    });

    product.stock =
        product.stock - quantity;
}

addProduct(1, 1);
addProduct(2, 2);

for item in cart {
    show(item.product.name);
    show(item.quantity);
}
```

This combines the documented array capabilities: array literals, arrays of objects, `for ... in`, indexing/property access, `push()`, mutation, functions, and `null` search results.

---

# 76. Recommended Array Tests

For testing the Pulsar interpreter:

```text
1. Empty array
2. Number array
3. String array
4. Boolean array
5. Null array
6. Mixed array
7. Nested array
8. Array of objects
9. Array indexing
10. Array assignment
11. Array length
12. push()
13. push() return value
14. pop()
15. shift()
16. unshift()
17. indexOf()
18. includesArr()
19. unique()
20. flatten()
21. randomChoice()
22. sort()
23. sort() with function
24. reverse()
25. isEmpty()
26. for ... in
27. Nested iteration
28. Array function parameter
29. Array return value
30. Array mutation inside function
31. filter()
32. map()
33. reduce()
34. Array of objects
35. Object property mutation
36. Queue
37. Stack
38. Shopping cart
39. Product search
40. Array type errors
```