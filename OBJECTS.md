## 1. Overview

Objects are collections of named properties in Pulsar.

A basic object is created with `{}`:

```pulsar
define user = {
    name: "Puma"
};

show(user);
```

The supplied Pulsar examples use object literals with named properties and demonstrate property access, mutation, nesting, and object builtins. 

---

## 2. Object Literal

The basic syntax is:

```pulsar
define object = {
    key: value
};
```

For example:

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(user);
```

---

## 3. Empty Object

An object can contain no properties.

```pulsar
define data = {};

show(data);
```

The supplied examples explicitly demonstrate an empty object. 

---

## 4. Single Property

```pulsar
define user = {
    name: "Puma"
};

show(user);
```

---

## 5. Multiple Properties

```pulsar
define user = {
    name: "Puma",
    age: 20,
    active: true
};

show(user);
```

---

## 6. String Properties

```pulsar
define user = {
    name: "Pulsar",
    country: "Myanmar"
};

show(user.name);
show(user.country);
```

---

## 7. Number Properties

```pulsar
define product = {
    price: 1200,
    stock: 5
};

show(product.price);
show(product.stock);
```

---

## 8. Boolean Properties

```pulsar
define account = {
    active: true,
    verified: false
};

show(account.active);
show(account.verified);
```

---

## 9. Null Properties

```pulsar
define user = {
    name: "Pulsar",
    email: null
};

show(user.email);
```

---

## 10. Mixed Properties

Object properties can contain different value types.

```pulsar
define profile = {
    name: "Pulsar",
    age: 20,
    active: true,
    email: null
};

show(profile);
```

---

# 11. Dot Property Access

Properties can be accessed with dot notation.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(user.name);
show(user.age);
```

This syntax is directly demonstrated in the supplied examples. 

---

# 12. Bracket Property Access

Properties can also be accessed using brackets.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(user["name"]);
show(user["age"]);
```

The supplied examples explicitly demonstrate bracket-based property access. 

---

# 13. Property With a Hyphen

Bracket notation is useful for property names that are not convenient for dot notation.

```pulsar
define data = {
    "first-name": "Puma"
};

show(data["first-name"]);
```

This exact form is demonstrated in the supplied examples. 

---

# 14. Reading a Property

```pulsar
define point = {
    x: 10,
    y: 20
};

show(point.x);
show(point.y);
```

---

# 15. Using Properties in Expressions

Object properties can participate in expressions.

```pulsar
define point = {
    x: 10,
    y: 20
};

show(point.x + point.y);
```

The supplied examples demonstrate this exact pattern. 

---

# 16. Changing a Property

Object properties can be reassigned.

```pulsar
define user = {
    name: "Puma"
};

user.name = "Pulsar";

show(user.name);
```

Property assignment is explicitly demonstrated in the supplied examples. 

---

# 17. Changing a Number Property

```pulsar
define user = {
    score: 100
};

user.score = 150;

show(user.score);
```

---

# 18. Compound Property Assignment

Object properties support compound assignment.

```pulsar
define user = {
    score: 100
};

user.score += 10;

show(user.score);
```

The supplied examples explicitly demonstrate `+=` on an object property. 

---

# 19. Subtraction Assignment

```pulsar
define account = {
    balance: 100
};

account.balance -= 25;

show(account.balance);
```

---

# 20. Multiplication Assignment

```pulsar
define product = {
    price: 100
};

product.price *= 2;

show(product.price);
```

---

# 21. Division Assignment

```pulsar
define value = {
    amount: 100
};

value.amount /= 4;

show(value.amount);
```

---

# 22. Nested Objects

Objects can contain other objects.

```pulsar
define nested = {
    user: {
        name: "Puma"
    }
};

show(nested.user.name);
```

The supplied examples explicitly demonstrate nested property access. 

---

# 23. Multiple Nested Properties

```pulsar
define user = {
    profile: {
        name: "Pulsar",
        age: 20
    }
};

show(user.profile.name);
show(user.profile.age);
```

---

# 24. Nested Object Modification

```pulsar
define user = {
    profile: {
        name: "Puma"
    }
};

user.profile.name = "Pulsar";

show(user.profile.name);
```

---

# 25. Object Containing an Array

```pulsar
define user = {
    name: "Pulsar",
    scores: [
        90,
        85,
        95
    ]
};

show(user.scores);
```

---

# 26. Array Inside an Object

Array elements can be accessed through an object property.

```pulsar
define user = {
    scores: [
        90,
        85,
        95
    ]
};

show(user.scores[0]);
show(user.scores[1]);
```

---

# 27. Object Inside an Array

```pulsar
define users = [
    {
        name: "Alice"
    },
    {
        name: "Bob"
    }
];

show(users[0].name);
show(users[1].name);
```

---

# 28. Object Returned From a Function

Functions can construct and return objects.

```pulsar
func makePoint(x, y) {
    return {
        x: x,
        y: y
    };
}

define point = makePoint(10, 20);

show(point.x);
show(point.y);
```

The supplied examples use this same pattern. 

---

# 29. Object as a Function Argument

```pulsar
func showUser(user) {
    show(user.name);
}

define user = {
    name: "Pulsar"
};

showUser(user);
```

---

# 30. Function Modifying an Object

```pulsar
func activate(user) {
    user.active = true;
}

define user = {
    active: false
};

activate(user);

show(user.active);
```

---

# 31. Object Describing a Product

```pulsar
define product = {
    id: 1,
    name: "Laptop",
    price: 1200,
    stock: 5
};

show(product.name);
show(product.price);
```

---

# 32. Object Describing a Configuration

```pulsar
define config = {
    debug: true,
    version: 1
};

show(config.debug);
show(config.version);
```

The supplied examples explicitly use this configuration pattern. 

---

# 33. Object With a Null Property

```pulsar
define account = {
    username: "Pulsar",
    email: null
};

if account.email == null {
    show("Email is missing");
}
```

---

# 34. Object Property With an Expression

```pulsar
define price = 100;
define quantity = 3;

define order = {
    total: price * quantity
};

show(order.total);
```

---

# 35. Object Property Referencing Another Variable

```pulsar
define name = "Pulsar";
define age = 20;

define user = {
    name: name,
    age: age
};

show(user);
```

---

# 36. Shorthand-Like Construction

When explicit property names and variables are used, the resulting object stores those values.

```pulsar
define name = "Pulsar";
define score = 100;

define user = {
    name: name,
    score: score
};

show(user);
```

Use the explicit form above when documenting the language syntax.

---

# 37. `keys()`

`keys()` returns the keys of an object.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(keys(user));
```

The supplied object-builtin examples explicitly demonstrate `keys()`. 

---

# 38. `values()`

`values()` returns the object's values.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(values(user));
```

This is directly demonstrated in the supplied examples. 

---

# 39. `hasOwn()`

`hasOwn()` checks whether an object has a specified property.

```pulsar
define user = {
    name: "Puma"
};

show(hasOwn(user, "name"));
```

The supplied examples explicitly demonstrate this operation. 

---

# 40. Missing Property With `hasOwn()`

```pulsar
define user = {
    name: "Puma"
};

show(hasOwn(user, "email"));
```

The supplied examples demonstrate checking a missing property. 

---

# 41. `isEmpty()` With an Object

```pulsar
define user = {};

show(isEmpty(user));
```

The supplied interpreter treats an object with no keys as empty. 

---

# 42. Non-Empty Object

```pulsar
define user = {
    name: "Puma"
};

show(isEmpty(user));
```

The supplied examples demonstrate the non-empty case as well. 

---

# 43. `merge()`

Objects can be combined with `merge()`.

```pulsar
define a = {
    x: 1
};

define b = {
    y: 2
};

define result =
    merge(a, b);

show(result);
```

The supplied object-builtin examples explicitly demonstrate `merge()`. 

---

# 44. Merging Configuration

```pulsar
define defaults = {
    debug: false,
    port: 8080
};

define custom = {
    debug: true
};

define config =
    merge(defaults, custom);

show(config);
```

---

# 45. `entries()`

`entries()` returns an object's entries.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(entries(user));
```

The supplied examples explicitly demonstrate `entries()`. 

---

# 46. `getProp()`

`getProp()` retrieves a property by name.

```pulsar
define user = {
    name: "Puma"
};

show(getProp(user, "name"));
```

The supplied object-builtin examples demonstrate this operation. 

---

# 47. `getProp()` With a Variable Key

```pulsar
define user = {
    name: "Pulsar",
    age: 20
};

define key = "name";

show(getProp(user, key));
```

---

# 48. `setProp()`

`setProp()` assigns a property by name.

```pulsar
define user = {};

setProp(user, "name", "Puma");

show(user.name);
```

This exact operation is present in the supplied examples. 

---

# 49. `setProp()` With a Variable Key

```pulsar
define user = {};

define key = "name";
define value = "Pulsar";

setProp(user, key, value);

show(user.name);
```

---

# 50. Dynamic Object Properties

`getProp()` and `setProp()` allow property names to be handled dynamically.

```pulsar
define user = {};

define key = "username";

setProp(user, key, "Pulsar");

show(getProp(user, key));
```

---

# 51. Iterating Over Object Keys

Pulsar's `for ... in` syntax can iterate over object keys.

```pulsar
define user = {
    name: "Pulsar",
    age: 20
};

for key in user {
    show(key);
}
```

The interpreter's `ForInStatement` distinguishes arrays from objects; for objects it iterates through `Object.keys(iterable)`.

---

# 52. Iterating Over Object Keys and Reading Values

```pulsar
define user = {
    name: "Pulsar",
    age: 20
};

for key in user {
    show(key);
    show(getProp(user, key));
}
```

---

# 53. Object as a Dictionary

Objects can be used as key-value collections.

```pulsar
define prices = {
    laptop: 1200,
    keyboard: 80,
    mouse: 40
};

show(prices.laptop);
show(prices.keyboard);
show(prices.mouse);
```

---

# 54. Dynamic Dictionary Lookup

```pulsar
define prices = {
    laptop: 1200,
    keyboard: 80,
    mouse: 40
};

define product = "keyboard";

show(getProp(prices, product));
```

---

# 55. Object-Based Counter

```pulsar
define counter = {
    value: 0
};

counter.value += 1;
counter.value += 1;
counter.value += 1;

show(counter.value);
```

---

# 56. Object-Based Configuration

```pulsar
define config = {
    host: "localhost",
    port: 8080,
    debug: true
};

if config.debug {
    show("Debug enabled");
}

show(config.host);
show(config.port);
```

---

# 57. Object With Nested Configuration

```pulsar
define config = {
    server: {
        host: "localhost",
        port: 8080
    },
    debug: true
};

show(config.server.host);
show(config.server.port);
```

---

# 58. Object Search Result

Objects work naturally with `null` when a lookup does not find a result.

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

func findUser(id) {
    for user in users {
        if user.id == id {
            return user;
        }
    }

    return null;
}

define user = findUser(3);

if user == null {
    show("User not found");
}
```

---

# 59. Object With Arrays and Nested Objects

```pulsar
define company = {
    name: "Pulsar",
    owner: {
        name: "Dominex"
    },
    products: [
        "Compiler",
        "Interpreter",
        "CLI"
    ]
};

show(company.name);
show(company.owner.name);
show(company.products[0]);
```

---

# 60. Complete Object Example

```pulsar
define product = {
    id: 1,
    name: "Laptop",
    price: 1200,
    stock: 5,
    specifications: {
        cpu: "Processor",
        memory: 16
    }
};

show(product.name);
show(product.price);
show(product.stock);
show(product.specifications.cpu);
show(product.specifications.memory);

product.stock -= 1;

show(product.stock);
```

---

# 61. Object Builtin Reference

| Builtin                       | Purpose                          |
| ----------------------------- | -------------------------------- |
| `keys(object)`                | Get object keys                  |
| `values(object)`              | Get object values                |
| `hasOwn(object, key)`         | Check whether a property exists  |
| `isEmpty(object)`             | Check whether an object is empty |
| `merge(a, b)`                 | Merge objects                    |
| `entries(object)`             | Get object entries               |
| `getProp(object, key)`        | Read a property dynamically      |
| `setProp(object, key, value)` | Set a property dynamically       |

These object builtins are explicitly represented in the supplied examples. 

---

# 62. Object Access Reference

| Syntax               | Purpose                          |
| -------------------- | -------------------------------- |
| `user.name`          | Dot property access              |
| `user["name"]`       | Bracket property access          |
| `user["first-name"]` | Property with special characters |
| `user.profile.name`  | Nested property access           |
| `users[0].name`      | Object property through an array |
| `user.scores[0]`     | Array element through an object  |

The supplied examples demonstrate each of these general access patterns. 

---

# 63. Object Mutation Reference

```pulsar
define user = {
    name: "Puma",
    score: 100
};

user.name = "Pulsar";
user.score += 10;

show(user);
```

Direct property mutation and compound property assignment are supported in the supplied examples.  

---

# 64. Object and Functions

Objects can be:

* created inside functions
* returned from functions
* passed to functions
* modified by functions
* stored inside arrays
* nested inside other objects

For example:

```pulsar
func createUser(name, age) {
    return {
        name: name,
        age: age,
        active: true
    };
}

define user =
    createUser("Pulsar", 20);

show(user.name);
show(user.age);
show(user.active);
```

The supplied examples explicitly demonstrate functions returning object literals. 

---

# 65. Objects Versus Entities

A plain object:

```pulsar
define user = {
    name: "Pulsar"
};
```

is different from an `entity` instance.

Entities support declarations such as:

```pulsar
entity Person {
    init(name) {
        self.name = name;
    }

    greet() {
        return "Hello " + self.name;
    }
}
```

and can be instantiated with:

```pulsar
define person = new Person("Puma");
```

The supplied examples document `entity`, `self`, initialization, methods, and `new` separately from ordinary object literals. 

---

# 66. Recommended Object Tests

Use these as interpreter tests:

```text
1. Empty object
2. Single-property object
3. Multiple-property object
4. String properties
5. Number properties
6. Boolean properties
7. Null properties
8. Mixed properties
9. Dot property access
10. Bracket property access
11. Property with a hyphen
12. Property assignment
13. Compound property assignment
14. Nested objects
15. Nested property access
16. Nested property mutation
17. Object containing an array
18. Array containing objects
19. Object as function argument
20. Object returned from a function
21. keys()
22. values()
23. hasOwn()
24. isEmpty()
25. merge()
26. entries()
27. getProp()
28. setProp()
29. Dynamic property lookup
30. Dynamic property assignment
31. Object iteration
32. Dictionary-style objects
33. Object-based counters
34. Configuration objects
35. Nested configuration
36. Object search result
37. Null object result
38. Object inside an array
39. Object inside another object
40. Object and function interaction
```