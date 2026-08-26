## 1. Overview

Pulsar provides `entity` declarations for creating structured, reusable objects with:

* properties
* methods
* initialization
* instance state
* inheritance
* method overriding

An entity declaration defines the structure and behavior of an entity. Instances are created with `new`.

The interpreter represents an entity definition with a name, a collection of methods, an optional parent entity, and its defining environment. 

---

## 2. Basic Entity

The basic syntax is:

```pulsar
entity Person {
    greet() {
        return "Hello";
    }
}
```

This creates an entity named `Person`.

An entity can contain methods that define its behavior.

---

## 3. Creating an Entity Instance

An instance is created using `new`.

```pulsar
entity Person {
    greet() {
        return "Hello";
    }
}

define person = new Person();

show(person.greet());
```

The `new` expression creates an instance from the entity definition.

---

## 4. Entity Initialization

Entities can define an `init()` method.

```pulsar
entity Person {
    init(name) {
        self.name = name;
    }
}
```

The `init()` method receives values when an instance is created.

```pulsar
define person = new Person("Alice");

show(person.name);
```

The supplied examples use this pattern for entity initialization. 

---

## 5. `self`

`self` refers to the current entity instance.

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

When called on an instance:

```pulsar
define person = new Person("Alice");

show(person.greet());
```

`self.name` refers to the `name` property belonging to that particular instance.

---

## 6. Entity Properties

Properties can be created through `self`.

```pulsar
entity Product {
    init(name, price) {
        self.name = name;
        self.price = price;
    }
}
```

Creating an instance:

```pulsar
define product = new Product(
    "Laptop",
    1200
);

show(product.name);
show(product.price);
```

Conceptually:

```text
Product instance
├── name  → "Laptop"
└── price → 1200
```

---

## 7. Entity Methods

Methods define behavior belonging to an entity.

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

The method can be called through an instance:

```pulsar
define person = new Person("Alice");

show(person.greet());
```

The interpreter stores entity methods with their name, parameters, body, and defining environment. 

---

## 8. Multiple Methods

An entity can contain multiple methods.

```pulsar
entity Calculator {
    add(a, b) {
        return a + b;
    }

    subtract(a, b) {
        return a - b;
    }

    multiply(a, b) {
        return a * b;
    }
}
```

Usage:

```pulsar
define calculator = new Calculator();

show(calculator.add(10, 5));
show(calculator.subtract(10, 5));
show(calculator.multiply(10, 5));
```

---

## 9. Entity State

Entity instances can maintain state.

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }

    increment() {
        self.value++;
        return self.value;
    }
}
```

Usage:

```pulsar
define counter = new Counter(0);

show(counter.increment());
show(counter.increment());
show(counter.increment());
```

The supplied examples use this exact stateful pattern. 

---

## 10. Changing Entity State

Entity methods can modify instance properties.

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }

    increment() {
        self.value++;
    }

    reset() {
        self.value = 0;
    }
}
```

Usage:

```pulsar
define counter = new Counter(10);

counter.increment();

show(counter.value);

counter.reset();

show(counter.value);
```

---

## 11. Reading Entity State

Properties can be accessed directly from an instance.

```pulsar
entity User {
    init(name) {
        self.name = name;
    }
}

define user = new User("Alice");

show(user.name);
```

---

## 12. Multiple Instances

Each call to `new` creates a separate instance.

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }

    increment() {
        self.value++;
    }
}

define first = new Counter(0);
define second = new Counter(100);

first.increment();

show(first.value);
show(second.value);
```

The two instances maintain their own state.

---

## 13. Entity Methods With Parameters

Methods can accept parameters.

```pulsar
entity Calculator {
    multiply(a, b) {
        return a * b;
    }
}

define calculator = new Calculator();

show(calculator.multiply(5, 4));
```

---

## 14. Methods Returning Values

```pulsar
entity Rectangle {
    init(width, height) {
        self.width = width;
        self.height = height;
    }

    area() {
        return self.width * self.height;
    }
}

define rectangle = new Rectangle(10, 5);

show(rectangle.area());
```

Output:

```text
50
```

---

## 15. Methods Using Instance Properties

```pulsar
entity Product {
    init(price, quantity) {
        self.price = price;
        self.quantity = quantity;
    }

    total() {
        return self.price * self.quantity;
    }
}

define product = new Product(100, 3);

show(product.total());
```

The method accesses the current instance through `self`.

---

# 16. Inheritance

An entity can inherit from another entity using `inherits`.

```pulsar
entity Animal {
    speak() {
        return "sound";
    }
}

entity Dog inherits Animal {
}
```

`Dog` is derived from `Animal`.

The interpreter evaluates the parent entity through the inheritance node and verifies that the parent has the required entity method structure. 

---

## 17. Inheriting Initialization

```pulsar
entity Animal {
    init(name) {
        self.name = name;
    }

    speak() {
        return "sound";
    }
}

entity Dog inherits Animal {
}
```

An instance can be created from the child entity:

```pulsar
define dog = new Dog("Buddy");

show(dog.name);
show(dog.speak());
```

The supplied examples demonstrate inherited initialization and behavior. 

---

## 18. Inheriting Methods

```pulsar
entity Animal {
    speak() {
        return "sound";
    }
}

entity Dog inherits Animal {
}

define dog = new Dog();

show(dog.speak());
```

`Dog` inherits the behavior defined by `Animal`.

---

## 19. Method Overriding

A child entity can define a method with the same name as a parent method.

```pulsar
entity Animal {
    speak() {
        return "sound";
    }
}

entity Dog inherits Animal {
    speak() {
        return "bark";
    }
}
```

Now:

```pulsar
define dog = new Dog();

show(dog.speak());
```

returns:

```text
bark
```

The supplied `DoubleCounter` example demonstrates this overriding pattern. 

---

## 20. Complete Inheritance Example

```pulsar
entity Animal {
    init(name) {
        self.name = name;
    }

    speak() {
        return "sound";
    }
}

entity Dog inherits Animal {
    speak() {
        return "bark";
    }
}

define dog = new Dog("Buddy");

show(dog.name);
show(dog.speak());
```

The supplied examples use this same entity/inheritance structure. 

---

## 21. Entity With Mutable State

```pulsar
entity BankAccount {
    init(balance) {
        self.balance = balance;
    }

    deposit(amount) {
        self.balance += amount;
    }

    withdraw(amount) {
        self.balance -= amount;
    }

    getBalance() {
        return self.balance;
    }
}

define account = new BankAccount(1000);

account.deposit(500);

show(account.getBalance());

account.withdraw(200);

show(account.getBalance());
```

The instance maintains its own `balance`.

---

## 22. Entity With Multiple Properties

```pulsar
entity User {
    init(name, age, active) {
        self.name = name;
        self.age = age;
        self.active = active;
    }

    describe() {
        return self.name + " " + self.age;
    }
}

define user = new User(
    "Alice",
    20,
    true
);

show(user.name);
show(user.age);
show(user.active);
show(user.describe());
```

---

## 23. Entity Method Calling Another Method

```pulsar
entity Person {
    init(name) {
        self.name = name;
    }

    getName() {
        return self.name;
    }

    greet() {
        return "Hello " + self.getName();
    }
}

define person = new Person("Alice");

show(person.greet());
```

---

## 24. Entity for a Product

```pulsar
entity Product {
    init(name, price, stock) {
        self.name = name;
        self.price = price;
        self.stock = stock;
    }

    buy(quantity) {
        self.stock -= quantity;
    }

    value() {
        return self.price * self.stock;
    }
}

define product = new Product(
    "Laptop",
    1200,
    5
);

product.buy(1);

show(product.stock);
show(product.value());
```

---

## 25. Entity for a Shop Item

```pulsar
entity Item {
    init(name, price) {
        self.name = name;
        self.price = price;
    }

    getPrice() {
        return self.price;
    }
}

define item = new Item(
    "Keyboard",
    80
);

show(item.name);
show(item.getPrice());
```

---

## 26. Entity Inheritance With State

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }

    increment() {
        self.value++;
        return self.value;
    }
}

entity DoubleCounter inherits Counter {
    increment() {
        self.value += 2;
        return self.value;
    }
}

define counter = new DoubleCounter(0);

show(counter.increment());
show(counter.increment());
```

This is directly based on the supplied entity inheritance example. 

---

## 27. Entity Parent Relationship

Internally, the interpreter represents an entity with:

```text
name
methods
parent
env
```

The relevant evaluator code constructs:

```text
entity = {
    name,
    methods: {},
    parent: null,
    env
}
```

and assigns the evaluated parent when inheritance is present. 

---

## 28. Entity Methods Internally

For every method in an entity, the interpreter stores:

```text
method name
parameters
body
environment
```

This is built by the entity evaluator. 

Conceptually:

```text
Entity
├── name
├── parent
├── env
└── methods
    ├── init
    │   ├── params
    │   ├── body
    │   └── env
    │
    └── greet
        ├── params
        ├── body
        └── env
```

---

## 29. Entity and Environment

An entity keeps the environment in which it was defined.

```text
Entity
├── name
├── methods
├── parent
└── env
```

This is different from an ordinary object literal.

The interpreter explicitly assigns `env` to the entity definition and to each stored method. 

---

## 30. Entity vs Object

An object literal is data:

```pulsar
define user = {
    name: "Alice",
    age: 20
};
```

An entity defines reusable behavior:

```pulsar
entity User {
    init(name, age) {
        self.name = name;
        self.age = age;
    }

    greet() {
        return "Hello " + self.name;
    }
}
```

An entity can then produce instances:

```pulsar
define user = new User("Alice", 20);
```

The important distinction is:

```text
Object
    → data

Entity
    → reusable structure + methods + optional inheritance
```

---

## 31. Entity Instances

The normal workflow is:

```text
Entity declaration
        |
        v
Entity definition
        |
        v
new Entity(...)
        |
        v
Instance
        |
        +---- properties
        |
        +---- methods
```

Example:

```pulsar
entity Person {
    init(name) {
        self.name = name;
    }

    greet() {
        return "Hello " + self.name;
    }
}

define person = new Person("Alice");

show(person.greet());
```

---

## 32. Complete Entity Example

```pulsar
entity Person {
    init(name, age) {
        self.name = name;
        self.age = age;
    }

    greet() {
        return "Hello " + self.name;
    }

    birthday() {
        self.age++;
        return self.age;
    }
}

define person = new Person(
    "Alice",
    20
);

show(person.name);
show(person.age);
show(person.greet());

person.birthday();

show(person.age);
```

---

## 33. Complete Inheritance Example

```pulsar
entity Animal {
    init(name) {
        self.name = name;
    }

    speak() {
        return "sound";
    }
}

entity Dog inherits Animal {
    speak() {
        return "bark";
    }
}

entity Cat inherits Animal {
    speak() {
        return "meow";
    }
}

define dog = new Dog("Buddy");
define cat = new Cat("Mimi");

show(dog.name);
show(dog.speak());

show(cat.name);
show(cat.speak());
```

---

## 34. Entity Syntax

The general structure is:

```pulsar
entity EntityName {
    init(parameters) {
        // initialization
    }

    methodName(parameters) {
        // method body
    }

    anotherMethod(parameters) {
        // method body
    }
}
```

An inherited entity uses:

```pulsar
entity ChildEntity inherits ParentEntity {
    methodName(parameters) {
        // overridden behavior
    }
}
```

An instance is created with:

```pulsar
define instance = new EntityName(arguments);
```

---

## 35. Entity Checklist

A valid entity example should test:

```text
1. Entity declaration
2. Empty entity
3. Entity method
4. init method
5. init parameters
6. self property
7. Multiple properties
8. Multiple methods
9. Method parameters
10. Method return value
11. Method state mutation
12. Multiple instances
13. Entity inheritance
14. Inherited init
15. Inherited method
16. Method overriding
17. Child-specific methods
18. Nested entity state
19. Entity method calling another method
20. Multi-level inheritance
```

---

## 36. Entity Summary

Pulsar's `entity` construct provides a way to define reusable types with state and behavior.

The core syntax is:

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

Instances are created with:

```pulsar
define person = new Person("Alice");
```

Inheritance is declared with:

```pulsar
entity Student inherits Person {
}
```

And methods can be overridden:

```pulsar
entity Student inherits Person {
    greet() {
        return "Hello from Student";
    }
}
```