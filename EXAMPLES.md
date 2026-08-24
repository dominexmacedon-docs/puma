## Contents

1. Basic Values\n2. Arithmetic\n3. Comparison and Logic\n4. Variables and Assignment\n5. If / Else\n6. While Loops\n7. Standard For Loops\n8. For-In\n9. Arrays\n10. Objects\n11. Functions\n12. Function Scope and Closures\n13. Arrow Functions\n14. Map / Filter / Reduce\n15. Strings\n16. JSON\n17. Slicing\n18. Break and Continue\n19. Ternary and Nullish\n20. Sldeploy / Deploy\n21. Entities\n22. Entity Inheritance\n23. Do / Track\n24. Math Builtins\n25. Object Builtins\n26. Array Builtins\n27. Files\n28. Environment\n
---

## 01 — Basic Values

### Example 1

```pulsar
show("Hello, Puma!");
```

### Example 2

```pulsar
show("Hello " + "World");
```

### Example 3

```pulsar
define name = "Puma";
show(name);
```

### Example 4

```pulsar
define version = 1;
show(version);
```

### Example 5

```pulsar
define pi = 3.14159;
show(pi);
```

### Example 6

```pulsar
define active = true;
show(active);
```

### Example 7

```pulsar
define inactive = false;
show(inactive);
```

### Example 8

```pulsar
define empty = null;
show(empty);
```

### Example 9

```pulsar
define mixed = [1, "two", true, null];
show(mixed);
```

### Example 10

```pulsar
define user = { name: "Dominex", active: true };
show(user);
```

## 02 — Arithmetic

### Example 1

```pulsar
show(2 + 3);
```

### Example 2

```pulsar
show(10 - 4);
```

### Example 3

```pulsar
show(6 * 7);
```

### Example 4

```pulsar
show(20 / 5);
```

### Example 5

```pulsar
show(17 % 5);
```

### Example 6

```pulsar
show(2 + 3 * 4);
```

### Example 7

```pulsar
show((2 + 3) * 4);
```

### Example 8

```pulsar
define a = 25;
define b = 4;
show(a / b);
```

### Example 9

```pulsar
show(-25);
```

### Example 10

```pulsar
show(+25);
```

## 03 — Comparison and Logic

### Example 1

```pulsar
show(10 == 10);
```

### Example 2

```pulsar
show(10 != 20);
```

### Example 3

```pulsar
show(5 < 10);
```

### Example 4

```pulsar
show(5 <= 5);
```

### Example 5

```pulsar
show(10 > 3);
```

### Example 6

```pulsar
show(10 >= 10);
```

### Example 7

```pulsar
show(true and true);
```

### Example 8

```pulsar
show(true and false);
```

### Example 9

```pulsar
show(false or true);
```

### Example 10

```pulsar
show(!false);
```

## 04 — Variables and Assignment

### Example 1

```pulsar
define x = 10;
show(x);
```

### Example 2

```pulsar
define name = "Puma";
name = "Pulsar";
show(name);
```

### Example 3

```pulsar
define x = 10;
x += 5;
show(x);
```

### Example 4

```pulsar
define x = 10;
x -= 3;
show(x);
```

### Example 5

```pulsar
define x = 10;
x *= 4;
show(x);
```

### Example 6

```pulsar
define x = 20;
x /= 5;
show(x);
```

### Example 7

```pulsar
define x = 17;
x %= 5;
show(x);
```

### Example 8

```pulsar
define x = 10;
x++;
show(x);
```

### Example 9

```pulsar
define x = 10;
x--;
show(x);
```

### Example 10

```pulsar
define user = { name: "Puma" };
user.name = "Pulsar";
show(user.name);
```

## 05 — If / Else

### Example 1

```pulsar
if true {
    show("true");
}
```

### Example 2

```pulsar
if false {
    show("wrong");
} else {
    show("else branch");
}
```

### Example 3

```pulsar
define age = 20;
if age >= 18 {
    show("adult");
} else {
    show("minor");
}
```

### Example 4

```pulsar
define score = 95;
if score >= 90 {
    show("A");
} else {
    show("not A");
}
```

### Example 5

```pulsar
define score = 85;
if score >= 90 {
    show("A");
} else if score >= 80 {
    show("B");
} else {
    show("C");
}
```

### Example 6

```pulsar
define n = 12;
if n % 2 == 0 {
    show("even");
} else {
    show("odd");
}
```

### Example 7

```pulsar
define name = "Puma";
if name == "Puma" {
    show("matched");
}
```

### Example 8

```pulsar
define a = 10;
define b = 20;
if a < b and b > 15 {
    show("both conditions are true");
}
```

### Example 9

```pulsar
define value = null;
if value == null {
    show("empty");
} else {
    show("not empty");
}
```

### Example 10

```pulsar
define temperature = 30;
if temperature > 35 {
    show("hot");
} else if temperature >= 20 {
    show("warm");
} else {
    show("cold");
}
```

## 06 — While Loops

### Example 1

```pulsar
define i = 0;
while i < 5 {
    show(i);
    i++;
}
```

### Example 2

```pulsar
define i = 5;
while i > 0 {
    show(i);
    i--;
}
```

### Example 3

```pulsar
define total = 0;
define i = 1;
while i <= 10 {
    total += i;
    i++;
}
show(total);
```

### Example 4

```pulsar
define i = 1;
while i <= 10 {
    if i % 2 == 0 {
        show(i);
    }
    i++;
}
```

### Example 5

```pulsar
define i = 1;
while i <= 10 {
    if i % 2 != 0 {
        show(i);
    }
    i++;
}
```

### Example 6

```pulsar
define n = 1;
while n < 100 {
    n *= 2;
}
show(n);
```

### Example 7

```pulsar
define i = 0;
while i < 3 {
    show("loop");
    i++;
}
```

### Example 8

```pulsar
define count = 3;
while count {
    show(count);
    count--;
}
```

### Example 9

```pulsar
define i = 1;
define product = 1;
while i <= 5 {
    product *= i;
    i++;
}
show(product);
```

### Example 10

```pulsar
define i = 10;
while i >= 1 {
    show(i);
    i--;
}
```

## 07 — Standard For Loops

### Example 1

```pulsar
for (define i = 0; i < 5; i++) {
    show(i);
}
```

### Example 2

```pulsar
for (define i = 1; i <= 5; i++) {
    show(i);
}
```

### Example 3

```pulsar
for (define i = 5; i > 0; i--) {
    show(i);
}
```

### Example 4

```pulsar
define total = 0;
for (define i = 1; i <= 10; i++) {
    total += i;
}
show(total);
```

### Example 5

```pulsar
for (define i = 0; i < 10; i++) {
    if i % 2 == 0 {
        show(i);
    }
}
```

### Example 6

```pulsar
for (define i = 1; i <= 10; i++) {
    if i % 2 != 0 {
        show(i);
    }
}
```

### Example 7

```pulsar
for (define i = 0; i < 3; i++) {
    show("iteration");
}
```

### Example 8

```pulsar
for (define i = 2; i <= 20; i += 2) {
    show(i);
}
```

### Example 9

```pulsar
for (define i = 10; i >= 0; i -= 2) {
    show(i);
}
```

### Example 10

```pulsar
define product = 1;
for (define i = 1; i <= 5; i++) {
    product *= i;
}
show(product);
```

## 08 — For-In

### Example 1

```pulsar
define values = [10, 20, 30];
for item in values {
    show(item);
}
```

### Example 2

```pulsar
define names = ["A", "B", "C"];
for name in names {
    show(name);
}
```

### Example 3

```pulsar
define values = [1, 2, 3, 4, 5];
for value in values {
    show(value * 2);
}
```

### Example 4

```pulsar
define values = [1, 2, 3, 4, 5];
for value in values {
    if value > 3 {
        show(value);
    }
}
```

### Example 5

```pulsar
define user = { name: "Puma", age: 20 };
for key in user {
    show(key);
}
```

### Example 6

```pulsar
define scores = { math: 90, english: 85, science: 95 };
for subject in scores {
    show(subject);
}
```

### Example 7

```pulsar
define letters = ["a", "b", "c"];
for letter in letters {
    show(upper(letter));
}
```

### Example 8

```pulsar
define values = [2, 4, 6];
define total = 0;
for value in values {
    total += value;
}
show(total);
```

### Example 9

```pulsar
define values = ["one", "two", "three"];
for value in values {
    show("value=" + value);
}
```

### Example 10

```pulsar
define data = { first: 1, second: 2 };
for key in data {
    show(key);
}
```

## 09 — Arrays

### Example 1

```pulsar
define values = [1, 2, 3];
show(values);
```

### Example 2

```pulsar
define values = ["a", "b", "c"];
show(values[0]);
```

### Example 3

```pulsar
define values = [10, 20, 30];
show(values[2]);
```

### Example 4

```pulsar
define values = [1, 2, 3];
values[1] = 99;
show(values);
```

### Example 5

```pulsar
define nested = [[1, 2], [3, 4]];
show(nested[1]);
```

### Example 6

```pulsar
define mixed = [1, "two", true, null];
show(mixed);
```

### Example 7

```pulsar
define empty = [];
show(empty);
```

### Example 8

```pulsar
define values = [1, 2, 3, 4, 5];
show(values[0:3]);
```

### Example 9

```pulsar
define values = [1, 2, 3, 4, 5];
show(values[1:5:2]);
```

### Example 10

```pulsar
define values = [1, 2, 3];
push(values, 4);
show(values);
```

## 10 — Objects

### Example 1

```pulsar
define user = { name: "Puma" };
show(user);
```

### Example 2

```pulsar
define user = { name: "Puma", age: 20 };
show(user.name);
```

### Example 3

```pulsar
define user = { name: "Puma", age: 20 };
show(user["name"]);
```

### Example 4

```pulsar
define user = { name: "Puma" };
user.name = "Pulsar";
show(user.name);
```

### Example 5

```pulsar
define point = { x: 10, y: 20 };
show(point.x + point.y);
```

### Example 6

```pulsar
define nested = { user: { name: "Puma" } };
show(nested.user.name);
```

### Example 7

```pulsar
define config = { debug: true, version: 1 };
show(config.debug);
```

### Example 8

```pulsar
define empty = {};
show(empty);
```

### Example 9

```pulsar
define data = { "first-name": "Puma" };
show(data["first-name"]);
```

### Example 10

```pulsar
define user = { name: "Puma", score: 100 };
user.score += 10;
show(user.score);
```

## 11 — Functions

### Example 1

```pulsar
func add(a, b) {
    return a + b;
}
show(add(2, 3));
```

### Example 2

```pulsar
func greet(name) {
    return "Hello " + name;
}
show(greet("Puma"));
```

### Example 3

```pulsar
func square(x) {
    return x * x;
}
show(square(5));
```

### Example 4

```pulsar
func isEven(x) {
    return x % 2 == 0;
}
show(isEven(8));
```

### Example 5

```pulsar
func maxValue(a, b) {
    if a > b {
        return a;
    }
    return b;
}
show(maxValue(10, 20));
```

### Example 6

```pulsar
func factorial(n) {
    if n <= 1 {
        return 1;
    }
    return n * factorial(n - 1);
}
show(factorial(5));
```

### Example 7

```pulsar
func repeatMessage(message, count) {
    define i = 0;
    while i < count {
        show(message);
        i++;
    }
}
repeatMessage("Hello", 3);
```

### Example 8

```pulsar
func makePoint(x, y) {
    return { x: x, y: y };
}
show(makePoint(10, 20));
```

### Example 9

```pulsar
func addOne(x) {
    return x + 1;
}
define value = addOne(10);
show(value);
```

### Example 10

```pulsar
func noResult() {
    show("inside");
}
define result = noResult();
show(result);
```

## 12 — Function Scope and Closures

### Example 1

```pulsar
define outside = 100;
func test() {
    return outside;
}
show(test());
```

### Example 2

```pulsar
define x = 10;
func readX() {
    return x;
}
show(readX());
```

### Example 3

```pulsar
define x = 10;
func change() {
    x = 20;
}
change();
show(x);
```

### Example 4

```pulsar
define prefix = "Hello ";
func greet(name) {
    return prefix + name;
}
show(greet("Puma"));
```

### Example 5

```pulsar
func outer(value) {
    func inner() {
        return value * 2;
    }
    return inner();
}
show(outer(10));
```

### Example 6

```pulsar
define base = 5;
func multiply(x) {
    return x * base;
}
show(multiply(4));
```

### Example 7

```pulsar
define message = "outer";
func test() {
    define message = "inner";
    return message;
}
show(test());
show(message);
```

### Example 8

```pulsar
define factor = 3;
func calculate(x) {
    return x * factor + 1;
}
show(calculate(5));
```

### Example 9

```pulsar
func makeValue(x) {
    define y = x + 10;
    return y;
}
show(makeValue(5));
```

### Example 10

```pulsar
define language = "Puma";
func identify() {
    return language;
}
show(identify());
```

## 13 — Arrow Functions

### Example 1

```pulsar
define double = x => x * 2;
show(double(5));
```

### Example 2

```pulsar
define square = x => x * x;
show(square(6));
```

### Example 3

```pulsar
define add = (a, b) => a + b;
show(add(2, 8));
```

### Example 4

```pulsar
define greet = name => "Hello " + name;
show(greet("Puma"));
```

### Example 5

```pulsar
define isEven = x => x % 2 == 0;
show(isEven(10));
```

### Example 6

```pulsar
define negate = x => -x;
show(negate(5));
```

### Example 7

```pulsar
define first = x => x[0];
show(first([10, 20]));
```

### Example 8

```pulsar
define getName = user => user.name;
show(getName({ name: "Puma" }));
```

### Example 9

```pulsar
define calculate = (a, b) => (a + b) * 2;
show(calculate(3, 4));
```

### Example 10

```pulsar
define identity = x => x;
show(identity("Puma"));
```

## 14 — Map / Filter / Reduce

### Example 1

```pulsar
define values = [1, 2, 3];
show(map(values, x => x * 2));
```

### Example 2

```pulsar
define values = [1, 2, 3, 4];
show(filter(values, x => x % 2 == 0));
```

### Example 3

```pulsar
define values = [1, 2, 3, 4];
show(reduce(values, (a, b) => a + b, 0));
```

### Example 4

```pulsar
define values = [2, 3, 4];
show(map(values, x => x * x));
```

### Example 5

```pulsar
define values = [1, 2, 3, 4, 5];
show(filter(values, x => x > 3));
```

### Example 6

```pulsar
define values = [10, 20, 30];
show(reduce(values, (a, b) => a + b, 0));
```

### Example 7

```pulsar
define names = ["a", "b", "c"];
show(map(names, x => upper(x)));
```

### Example 8

```pulsar
define values = [1, 2, 3, 4, 5, 6];
show(filter(values, x => x % 2 != 0));
```

### Example 9

```pulsar
define values = [1, 2, 3];
show(reduce(values, (a, b) => a * b, 1));
```

### Example 10

```pulsar
define values = [5, 10, 15];
define doubled = map(values, x => x * 2);
define large = filter(doubled, x => x > 15);
show(large);
```

## 15 — Strings

### Example 1

```pulsar
show(lower("HELLO"));
```

### Example 2

```pulsar
show(upper("hello"));
```

### Example 3

```pulsar
show(trim("   Puma   "));
```

### Example 4

```pulsar
show(startsWith("Hello Puma", "Hello"));
```

### Example 5

```pulsar
show(endsWith("Hello Puma", "Puma"));
```

### Example 6

```pulsar
show(includes("Hello Puma", "Puma"));
```

### Example 7

```pulsar
show(replace("Hello Puma", "Puma", "World"));
```

### Example 8

```pulsar
show(reverseStr("Puma"));
```

### Example 9

```pulsar
show(repeatStr("ha", 3));
```

### Example 10

```pulsar
show(split("a,b,c", ","));
```

## 16 — JSON

### Example 1

```pulsar
define data = { name: "Puma" };
show(JSONStringify(data));
```

### Example 2

```pulsar
define text = "{"name":"Puma"}";
show(JSONParse(text));
```

### Example 3

```pulsar
define data = { version: 1, active: true };
define text = JSONStringify(data);
show(text);
```

### Example 4

```pulsar
define text = "{"value":42}";
define data = JSONParse(text);
show(data.value);
```

### Example 5

```pulsar
define data = [1, 2, 3];
show(JSONStringify(data));
```

### Example 6

```pulsar
define text = "[1,2,3]";
define data = JSONParse(text);
show(data[1]);
```

### Example 7

```pulsar
define data = { user: { name: "Puma" } };
define text = JSONStringify(data);
show(text);
```

### Example 8

```pulsar
define text = "{"items":[1,2,3]}";
define data = JSONParse(text);
show(data.items);
```

### Example 9

```pulsar
define data = { ok: true, value: null };
define text = JSONStringify(data);
show(JSONParse(text));
```

### Example 10

```pulsar
define data = { name: "Puma", scores: [90, 95] };
define encoded = JSONStringify(data);
define decoded = JSONParse(encoded);
show(decoded.name);
show(decoded.scores);
```

## 17 — Slicing

### Example 1

```pulsar
define values = [0, 1, 2, 3, 4];
show(values[0:3]);
```

### Example 2

```pulsar
define values = [0, 1, 2, 3, 4];
show(values[2:5]);
```

### Example 3

```pulsar
define values = [0, 1, 2, 3, 4];
show(values[:3]);
```

### Example 4

```pulsar
define values = [0, 1, 2, 3, 4];
show(values[2:]);
```

### Example 5

```pulsar
define values = [0, 1, 2, 3, 4, 5];
show(values[0:6:2]);
```

### Example 6

```pulsar
define values = [0, 1, 2, 3, 4, 5];
show(values[1:6:2]);
```

### Example 7

```pulsar
define text = "Puma";
show(text[0:2]);
```

### Example 8

```pulsar
define values = [10, 20, 30, 40, 50];
show(values[-3:]);
```

### Example 9

```pulsar
define values = [10, 20, 30, 40, 50];
show(values[:2]);
```

### Example 10

```pulsar
define values = [1, 2, 3, 4, 5, 6];
show(values[1:5:2]);
```

## 18 — Break and Continue

### Example 1

```pulsar
define i = 0;
while i < 10 {
    i++;
    if i == 5 {
        break;
    }
    show(i);
}
```

### Example 2

```pulsar
define i = 0;
while i < 5 {
    i++;
    if i == 3 {
        continue;
    }
    show(i);
}
```

### Example 3

```pulsar
for (define i = 0; i < 10; i++) {
    if i == 4 {
        break;
    }
    show(i);
}
```

### Example 4

```pulsar
for (define i = 0; i < 6; i++) {
    if i % 2 == 0 {
        continue;
    }
    show(i);
}
```

### Example 5

```pulsar
define i = 1;
while i <= 10 {
    if i > 7 {
        break;
    }
    show(i);
    i++;
}
```

### Example 6

```pulsar
define i = 0;
while i < 5 {
    i++;
    if i == 2 {
        continue;
    }
    if i == 4 {
        break;
    }
    show(i);
}
```

### Example 7

```pulsar
for (define i = 1; i <= 10; i++) {
    if i == 8 {
        break;
    }
    if i % 2 == 0 {
        continue;
    }
    show(i);
}
```

### Example 8

```pulsar
define values = [1, 2, 3, 4, 5];
for value in values {
    if value == 4 {
        break;
    }
    show(value);
}
```

### Example 9

```pulsar
define values = [1, 2, 3, 4, 5];
for value in values {
    if value % 2 == 0 {
        continue;
    }
    show(value);
}
```

### Example 10

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

## 19 — Ternary and Nullish

### Example 1

```pulsar
show(true ? "yes" : "no");
```

### Example 2

```pulsar
show(false ? "yes" : "no");
```

### Example 3

```pulsar
define age = 20;
show(age >= 18 ? "adult" : "minor");
```

### Example 4

```pulsar
define score = 80;
define grade = score >= 80 ? "good" : "bad";
show(grade);
```

### Example 5

```pulsar
define value = null;
show(value ?? "default");
```

### Example 6

```pulsar
define value = "Puma";
show(value ?? "default");
```

### Example 7

```pulsar
define a = null;
define b = null;
define c = "fallback";
show(a ?? b ?? c);
```

### Example 8

```pulsar
define value = 0;
show(value ?? 100);
```

### Example 9

```pulsar
define value = false;
show(value ?? true);
```

### Example 10

```pulsar
define n = 5;
show(n > 3 ? n * 2 : n / 2);
```

## 20 — Sldeploy / Deploy

### Example 1

```pulsar
define message = "hello";
sldeploy message;
```

### Example 2

```pulsar
define version = 1;
sldeploy version;
```

### Example 3

```pulsar
define data = [1, 2, 3];
sldeploy data;
```

### Example 4

```pulsar
define user = { name: "Puma" };
sldeploy user;
```

### Example 5

```pulsar
sldeploy "direct value";
```

### Example 6

```pulsar
func add(a, b) {
    return a + b;
}
sldeploy add(2, 3);
```

### Example 7

```pulsar
define value = 10;
define doubled = value * 2;
sldeploy doubled;
```

### Example 8

```pulsar
define name = "Puma";
sldeploy "Hello " + name;
```

### Example 9

```pulsar
define active = true;
sldeploy active;
```

### Example 10

```pulsar
define result = [1, 2, 3];
sldeploy JSONStringify(result);
```

## 21 — Entities

### Example 1

```pulsar
entity Person {
    init(name) {
        self.name = name;
    }

    greet() {
        return "Hello " + self.name;
    }
}

define person = new Person("Puma");
show(person.name);
show(person.greet());
```

### Example 2

```pulsar
entity Counter {
    init(value) {
        self.value = value;
    }

    get() {
        return self.value;
    }
}

define counter = new Counter(10);
show(counter.get());
```

### Example 3

```pulsar
entity Point {
    init(x, y) {
        self.x = x;
        self.y = y;
    }

    sum() {
        return self.x + self.y;
    }
}

define p = new Point(3, 4);
show(p.sum());
```

### Example 4

```pulsar
entity User {
    init(name, age) {
        self.name = name;
        self.age = age;
    }

    label() {
        return self.name + ":" + self.age;
    }
}

define user = new User("Puma", 20);
show(user.label());
```

### Example 5

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

define r = new Rectangle(5, 4);
show(r.area());
```

### Example 6

```pulsar
entity Greeter {
    init(prefix) {
        self.prefix = prefix;
    }

    greet(name) {
        return self.prefix + name;
    }
}

define g = new Greeter("Hello ");
show(g.greet("Puma"));
```

### Example 7

```pulsar
entity Box {
    init(value) {
        self.value = value;
    }

    double() {
        self.value *= 2;
        return self.value;
    }
}

define b = new Box(5);
show(b.double());
show(b.double());
```

### Example 8

```pulsar
entity Account {
    init(balance) {
        self.balance = balance;
    }

    deposit(amount) {
        self.balance += amount;
        return self.balance;
    }
}

define account = new Account(100);
show(account.deposit(50));
```

### Example 9

```pulsar
entity Animal {
    init(name) {
        self.name = name;
    }

    speak() {
        return self.name;
    }
}

define animal = new Animal("Fox");
show(animal.speak());
```

### Example 10

```pulsar
entity Config {
    init(version) {
        self.version = version;
        self.active = true;
    }

    info() {
        return self.version;
    }
}

define config = new Config(1);
show(config.info());
show(config.active);
```

## 22 — Entity Inheritance

### Example 1

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

### Example 2

```pulsar
entity Person {
    init(name) {
        self.name = name;
    }
}

entity Student inherits Person {
    init(name, grade) {
        self.name = name;
        self.grade = grade;
    }
}

define student = new Student("Puma", 10);
show(student.name);
show(student.grade);
```

### Example 3

```pulsar
entity Shape {
    init(value) {
        self.value = value;
    }

    get() {
        return self.value;
    }
}

entity DoubleShape inherits Shape {
    get() {
        return self.value * 2;
    }
}

define shape = new DoubleShape(5);
show(shape.get());
```

### Example 4

```pulsar
entity Animal {
    init(name) {
        self.name = name;
    }

    speak() {
        return self.name + " sound";
    }
}

entity Cat inherits Animal {
    speak() {
        return self.name + " meow";
    }
}

define cat = new Cat("Mimi");
show(cat.speak());
```

### Example 5

```pulsar
entity Vehicle {
    init(name) {
        self.name = name;
    }
}

entity Car inherits Vehicle {
    init(name, wheels) {
        self.name = name;
        self.wheels = wheels;
    }
}

define car = new Car("Car", 4);
show(car.name);
show(car.wheels);
```

### Example 6

```pulsar
entity Base {
    init(value) {
        self.value = value;
    }

    get() {
        return self.value;
    }
}

entity Child inherits Base {
    get() {
        return self.value + 10;
    }
}

define child = new Child(5);
show(child.get());
```

### Example 7

```pulsar
entity User {
    init(name) {
        self.name = name;
    }
}

entity Admin inherits User {
    isAdmin() {
        return true;
    }
}

define admin = new Admin("Puma");
show(admin.name);
show(admin.isAdmin());
```

### Example 8

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

define c = new DoubleCounter(0);
show(c.increment());
show(c.increment());
```

### Example 9

```pulsar
entity A {
    init(value) {
        self.value = value;
    }
}

entity B inherits A {
    value2() {
        return self.value * 2;
    }
}

define b = new B(7);
show(b.value2());
```

### Example 10

```pulsar
entity Message {
    init(text) {
        self.text = text;
    }

    get() {
        return self.text;
    }
}

entity LoudMessage inherits Message {
    get() {
        return upper(self.text);
    }
}

define m = new LoudMessage("hello");
show(m.get());
```

## 23 — Do / Track

### Example 1

```pulsar
do {
    show("normal");
} track {
    show("error");
}
```

### Example 2

```pulsar
do {
    define x = 10 / 0;
    show(x);
} track {
    show(error);
}
```

### Example 3

```pulsar
do {
    define x = missingVariable;
    show(x);
} track {
    show("caught");
}
```

### Example 4

```pulsar
do {
    show("before");
    define x = 10 / 0;
    show("after");
} track {
    show("tracked");
}
```

### Example 5

```pulsar
do {
    define data = JSONParse("invalid");
    show(data);
} track {
    show("JSON error tracked");
}
```

### Example 6

```pulsar
do {
    define value = 10;
    show(value);
} track {
    show("should not run");
}
```

### Example 7

```pulsar
do {
    define x = 5;
    x = x + 5;
    show(x);
} track {
    show("not reached");
}
```

### Example 8

```pulsar
do {
    show(missingVariable);
} track {
    show("runtime error handled");
}
```

### Example 9

```pulsar
do {
    define x = [1, 2, 3];
    show(x[0]);
} track {
    show("not reached");
}
```

### Example 10

```pulsar
do {
    define x = 10 / 0;
} track {
    show("recovered");
}
show("after track");
```

## 24 — Math Builtins

### Example 1

```pulsar
show(abs(-10));
```

### Example 2

```pulsar
show(floor(4.8));
```

### Example 3

```pulsar
show(ceil(4.2));
```

### Example 4

```pulsar
show(round(4.6));
```

### Example 5

```pulsar
show(sqrt(25));
```

### Example 6

```pulsar
show(pow(2, 5));
```

### Example 7

```pulsar
show(min(10, 20));
```

### Example 8

```pulsar
show(max(10, 20));
```

### Example 9

```pulsar
show(clamp(150, 0, 100));
```

### Example 10

```pulsar
show(sign(-42));
```

## 25 — Object Builtins

### Example 1

```pulsar
define user = { name: "Puma", age: 20 };
show(keys(user));
```

### Example 2

```pulsar
define user = { name: "Puma", age: 20 };
show(values(user));
```

### Example 3

```pulsar
define user = { name: "Puma" };
show(hasOwn(user, "name"));
```

### Example 4

```pulsar
define user = { name: "Puma" };
show(hasOwn(user, "missing"));
```

### Example 5

```pulsar
define user = {};
show(isEmpty(user));
```

### Example 6

```pulsar
define user = { name: "Puma" };
show(isEmpty(user));
```

### Example 7

```pulsar
define a = { x: 1 };
define b = { y: 2 };
show(merge(a, b));
```

### Example 8

```pulsar
define user = { name: "Puma", age: 20 };
show(entries(user));
```

### Example 9

```pulsar
define user = { name: "Puma" };
show(getProp(user, "name"));
```

### Example 10

```pulsar
define user = {};
setProp(user, "name", "Puma");
show(user.name);
```

## 26 — Array Builtins

### Example 1

```pulsar
define values = [1, 2, 3];
push(values, 4);
show(values);
```

### Example 2

```pulsar
define values = [1, 2, 3];
show(pop(values));
show(values);
```

### Example 3

```pulsar
define values = [1, 2, 3];
unshift(values, 0);
show(values);
```

### Example 4

```pulsar
define values = [1, 2, 3];
show(shift(values));
show(values);
```

### Example 5

```pulsar
define values = [3, 1, 2];
show(sort(values));
```

### Example 6

```pulsar
define values = [1, 2, 3];
show(reverse(values));
```

### Example 7

```pulsar
define values = [1, 2, 2, 3, 3];
show(unique(values));
```

### Example 8

```pulsar
define values = [1, 2, 3];
show(indexOf(values, 2));
```

### Example 9

```pulsar
define values = [1, 2, 3];
show(includesArr(values, 2));
```

### Example 10

```pulsar
define values = [[1, 2], [3, 4]];
show(flatten(values));
```

## 27 — Files

### Example 1

```pulsar
define filename = "puma_test.txt";
writeFile(filename, "Hello Puma");
show(readFile(filename));
deleteFile(filename);
```

### Example 2

```pulsar
define filename = "puma_test.txt";
writeFile(filename, "First");
appendFile(filename, " Second");
show(readFile(filename));
deleteFile(filename);
```

### Example 3

```pulsar
define filename = "exists_test.txt";
writeFile(filename, "test");
show(exists(filename));
deleteFile(filename);
show(exists(filename));
```

### Example 4

```pulsar
define filename = "json_test.json";
writeJSON(filename, { name: "Puma", version: 1 });
show(readJSON(filename));
deleteFile(filename);
```

### Example 5

```pulsar
define filename = "append_test.txt";
writeFile(filename, "A");
appendFile(filename, "B");
appendFile(filename, "C");
show(readFile(filename));
deleteFile(filename);
```

### Example 6

```pulsar
define filename = "empty_test.txt";
writeFile(filename, "");
show(readFile(filename));
deleteFile(filename);
```

### Example 7

```pulsar
define filename = "numbers.json";
writeJSON(filename, [1, 2, 3]);
define data = readJSON(filename);
show(data[1]);
deleteFile(filename);
```

### Example 8

```pulsar
define filename = "object.json";
writeJSON(filename, { active: true, count: 5 });
define data = readJSON(filename);
show(data.active);
show(data.count);
deleteFile(filename);
```

### Example 9

```pulsar
define filename = "lines.txt";
writeFile(filename, "one\ntwo\nthree");
define content = readFile(filename);
show(content);
deleteFile(filename);
```

### Example 10

```pulsar
define filename = "temporary.txt";
writeFile(filename, "temporary");
if exists(filename) {
    show("file created");
}
deleteFile(filename);
```

## 28 — Environment

### Example 1

```pulsar
show(env("PATH"));
```

### Example 2

```pulsar
show(env("HOME"));
```

### Example 3

```pulsar
show(env("USER"));
```

### Example 4

```pulsar
show(env("USERNAME"));
```

### Example 5

```pulsar
show(env("SHELL"));
```

### Example 6

```pulsar
show(env("TEMP"));
```

### Example 7

```pulsar
show(env("TMP"));
```

### Example 8

```pulsar
show(env("NODE_ENV"));
```

### Example 9

```pulsar
show(env("PORT"));
```

### Example 10

```pulsar
define path = env("PATH");
show(path);
```
