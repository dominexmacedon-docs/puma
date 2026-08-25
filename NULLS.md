## 1. Overview

`null` is a special Pulsar value representing an empty or absent value.

A basic `null` value can be created with:

```pulsar
define empty = null;

show(empty);
```

The supplied Pulsar examples explicitly include `null` as a basic value. 

---

# 2. Null Literal

`null` can be written directly as a literal.

```pulsar
show(null);
```

---

# 3. Null Variable

A variable can contain `null`.

```pulsar
define value = null;

show(value);
```

---

# 4. Null in an Array

`null` can be stored alongside other values.

```pulsar
define values = [
    1,
    "two",
    true,
    null
];

show(values);
```

The supplied examples explicitly demonstrate a mixed array containing `null`. 

---

# 5. Null in an Object

`null` can also be used as an object property value.

```pulsar
define user = {
    name: "Pulsar",
    email: null
};

show(user);
```

---

# 6. Null Property

A null-valued property can be accessed normally.

```pulsar
define user = {
    name: "Pulsar",
    email: null
};

show(user.email);
```

---

# 7. Reassigning Null

A variable containing `null` can later receive another value.

```pulsar
define value = null;

value = 100;

show(value);
```

---

# 8. Assigning Null

An existing value can be replaced with `null`.

```pulsar
define value = 100;

value = null;

show(value);
```

---

# 9. Null and Equality

`null` can participate in equality expressions.

```pulsar
define value = null;

show(value == null);
```

Use equality comparisons to explicitly test whether a value is `null`.

---

# 10. Null and Inequality

```pulsar
define value = 100;

show(value != null);
```

This checks whether the value is different from `null`.

The supplied examples establish `==` and `!=` as equality operators. 

---

# 11. Null in Conditional Logic

A value can be checked against `null`.

```pulsar
define value = null;

if value == null {
    show("No value");
}
```

---

# 12. Null Check With `else`

```pulsar
define value = null;

if value == null {
    show("Missing");
} else {
    show("Available");
}
```

---

# 13. Non-Null Check

```pulsar
define value = "Pulsar";

if value != null {
    show("Value exists");
}
```

---

# 14. Nullish Coalescing

Pulsar supports the `??` operator.

It selects the right-hand value when the left-hand value is `null`.

```pulsar
define value = null;

show(value ?? "default");
```

The supplied examples explicitly demonstrate this behavior. 

---

# 15. Non-Null Value With `??`

When the left-hand value is not `null`, it is retained.

```pulsar
define value = "Pulsar";

show(value ?? "default");
```

The supplied examples explicitly demonstrate this. 

---

# 16. Chained Nullish Coalescing

Multiple `??` expressions can be chained.

```pulsar
define a = null;
define b = null;
define c = "fallback";

show(a ?? b ?? c);
```

The supplied examples explicitly demonstrate this pattern. 

The evaluation searches from left to right until a non-null value is available.

---

# 17. Nullish Coalescing With Zero

`0` is not replaced by `??`.

```pulsar
define value = 0;

show(value ?? 100);
```

The supplied examples explicitly demonstrate that `0` is retained. 

This is an important distinction:

```text
null
```

means no value, while:

```text
0
```

is an actual numeric value.

---

# 18. Nullish Coalescing With `false`

`false` is also retained by `??`.

```pulsar
define value = false;

show(value ?? true);
```

The supplied examples explicitly demonstrate this behavior. 

Therefore:

```text
false ?? true
```

does not mean:

```text
true
```

The left side is already a valid non-null value.

---

# 19. Nullish Coalescing With Strings

```pulsar
define name = null;

define result =
    name ?? "Unknown";

show(result);
```

If `name` is a string:

```pulsar
define name = "Pulsar";

define result =
    name ?? "Unknown";

show(result);
```

the original string is retained.

---

# 20. Default Configuration Value

```pulsar
define config = {
    port: null
};

define port =
    config.port ?? 8080;

show(port);
```

This provides a default when the configuration value is `null`.

---

# 21. Default User Value

```pulsar
define username = null;

define displayName =
    username ?? "Guest";

show(displayName);
```

---

# 22. Multiple Fallback Values

```pulsar
define primary = null;
define secondary = null;
define fallback = "Pulsar";

define name =
    primary ?? secondary ?? fallback;

show(name);
```

This follows the same chained-nullish pattern demonstrated in the supplied examples. 

---

# 23. Null as a Function Argument

A function can receive `null` as an argument.

```pulsar
func showValue(value) {
    show(value);
}

showValue(null);
```

---

# 24. Null Function Parameter Check

```pulsar
func getName(name) {
    if name == null {
        return "Unknown";
    }

    return name;
}

show(getName(null));
show(getName("Pulsar"));
```

---

# 25. Returning Null

A function can explicitly return `null`.

```pulsar
func findUser() {
    return null;
}

define user = findUser();

show(user);
```

---

# 26. Null as a Search Result

```pulsar
func findProduct(id) {
    if id == 1 {
        return {
            name: "Laptop"
        };
    }

    return null;
}

define product = findProduct(99);

if product == null {
    show("Product not found");
}
```

---

# 27. Nullish Result From a Function

```pulsar
func findName() {
    return null;
}

define name =
    findName() ?? "Unknown";

show(name);
```

---

# 28. Null and Object Properties

```pulsar
define product = {
    name: "Laptop",
    description: null
};

if product.description == null {
    show("No description");
}
```

---

# 29. Replacing a Null Property

```pulsar
define product = {
    description: null
};

product.description =
    "Portable computer";

show(product.description);
```

The evaluator permits assignment to object properties and explicitly checks for `null`/`undefined` when the object itself is unavailable. 

---

# 30. Null Object Assignment Error

An object property cannot be assigned through a `null` object.

For example:

```pulsar
define user = null;

user.name = "Pulsar";
```

The evaluator checks the target object and raises a runtime error when it is `null` or `undefined`:

```text
Cannot assign to null or undefined
```

This behavior is implemented directly in the assignment evaluator. 

---

# 31. Null Array Assignment Error

The same protection applies when assigning through an index.

```pulsar
define values = null;

values[0] = 10;
```

The evaluator checks whether the indexed object is `null` before performing the assignment. 

---

# 32. Null in Compound Assignment

The evaluator has special handling for compound assignment on member/index expressions:

```javascript
current = await this.evalMember(left, env) ?? 0;
```

and:

```javascript
current = await this.evalIndex(left, env) ?? 0;
```

Thus, the runtime treats a missing/null member or indexed value as `0` for these compound-assignment paths. 

For documentation, test this behavior against the exact interpreter version you are distributing.

---

# 33. Null From Functions Without a Return Value

The supplied evaluator explicitly normalizes JavaScript `undefined` function results to Pulsar `null`.

For native functions:

```javascript
return val === undefined ? null : val;
```

and for Pulsar functions:

```javascript
return val === undefined ? null : val;
```

The same behavior is applied to explicit `ReturnValue` results. 

Therefore, the runtime uses `null` as the normalized result when a callable produces no value.

---

# 34. Function With No Explicit Return

For example:

```pulsar
func greet() {
    show("Hello");
}

define result = greet();

show(result);
```

The evaluator's function-call machinery converts an undefined result to `null`. 

---

# 35. Arrow Function With No Result

The evaluator similarly normalizes undefined results from arrow functions to `null`.

A block arrow function with no returned value therefore follows the runtime's null-normalization behavior. 

---

# 36. Null and JSON

`JSONParse()` returns the JavaScript JSON representation of the supplied JSON string.

The evaluator requires its argument to be a string and passes valid JSON through `JSON.parse()`. 

For example:

```pulsar
define data =
    JSONParse("null");

show(data);
```

This represents JSON's `null` value.

---

# 37. JSON Object Containing Null

```pulsar
define data =
    JSONParse("{\"name\":\"Pulsar\",\"email\":null}");

show(data);
```

The parsed object can then contain a null property.

---

# 38. Reading a JSON Null Property

```pulsar
define data =
    JSONParse("{\"name\":\"Pulsar\",\"email\":null}");

if data.email == null {
    show("Email is missing");
}
```

---

# 39. JSON Stringification

`JSONStringify()` converts a Pulsar runtime value to JSON text.

```pulsar
define data = {
    name: "Pulsar",
    value: null
};

define text =
    JSONStringify(data);

show(text);
```

The supplied evaluator implements `JSONStringify()` using JSON serialization. 

---

# 40. Null and `isEmpty()`

The supplied interpreter contains an `isEmpty()` builtin.

Its implementation explicitly returns `true` when the argument is `null`:

```javascript
if (arg == null) return true;
```

It also handles empty arrays, strings, and objects separately. 

Therefore:

```pulsar
define value = null;

show(isEmpty(value));
```

returns the empty-state result defined by the runtime.

---

# 41. Empty Versus Null

An empty array and `null` are different values.

```pulsar
define a = null;
define b = [];

show(a);
show(b);
```

The supplied examples separately demonstrate `null` and an empty array.  

---

# 42. Null Versus Empty String

Likewise, `null` and an empty string are different values.

```pulsar
define a = null;
define b = "";

show(a);
show(b);
```

They represent different kinds of state.

---

# 43. Nullish Default Pattern

A common Pulsar pattern is:

```pulsar
define value = null;

define result =
    value ?? "default";

show(result);
```

This is the simplest nullish-default pattern demonstrated by the supplied examples. 

---

# 44. Nullish Configuration Pattern

```pulsar
define settings = {
    host: null,
    port: null
};

define host =
    settings.host ?? "localhost";

define port =
    settings.port ?? 8080;

show(host);
show(port);
```

---

# 45. Nullish User Profile Pattern

```pulsar
define profile = {
    username: null,
    nickname: "Pulsar"
};

define name =
    profile.username ??
    profile.nickname ??
    "Guest";

show(name);
```

---

# 46. Nullish Database Result Pattern

```pulsar
func findRecord(id) {
    return null;
}

define record =
    findRecord(10);

define result =
    record ?? "Not found";

show(result);
```

---

# 47. Null in Conditional Return

```pulsar
func getValue(condition) {
    if condition {
        return "Pulsar";
    }

    return null;
}

define value =
    getValue(false);

if value == null {
    show("No result");
}
```

---

# 48. Nullish Fallback Function

```pulsar
func getName(value) {
    return value ?? "Unknown";
}

show(getName(null));
show(getName("Pulsar"));
```

---

# 49. Null in Mixed Data

```pulsar
define records = [
    {
        name: "Pulsar",
        email: "hello@example.com"
    },
    {
        name: "Dominex",
        email: null
    }
];

for record in records {
    if record.email == null {
        show(record.name + " has no email");
    }
}
```

---

# 50. Null Feature Summary

Pulsar's supplied materials demonstrate `null` in the following contexts:

```text
Null literal
Null variables
Null reassignment
Null object properties
Null array values
Null equality
Null inequality
Null conditional checks
Nullish coalescing
Chained nullish coalescing
Nullish defaults
Null function arguments
Null function results
Null return values
Null JSON values
Null object assignment protection
Null indexed assignment protection
Null compound-assignment handling
Null normalization for undefined callable results
isEmpty(null)
```

The core examples explicitly establish `null` as a basic value and demonstrate `??`, including fallback values, chained fallbacks, and the fact that `0` and `false` are retained rather than treated as null.  

---

# 51. Null Operator Reference

| Syntax              | Purpose                         |
| ------------------- | ------------------------------- |
| `null`              | Null literal                    |
| `value == null`     | Check for null                  |
| `value != null`     | Check for non-null              |
| `value ?? fallback` | Use fallback when value is null |
| `a ?? b ?? c`       | Try multiple fallback values    |

The supplied examples directly demonstrate these null-related forms. 

---

# 52. Recommended Null Tests

For testing the Pulsar interpreter:

```text
1. null literal
2. null variable
3. null reassignment
4. null in an array
5. null in an object
6. null property access
7. null equality
8. null inequality
9. null in if
10. null in if/else
11. null function argument
12. null function return
13. nullish coalescing
14. non-null value with ??
15. zero with ??
16. false with ??
17. chained ??
18. string fallback
19. numeric fallback
20. object fallback
21. JSON null
22. null JSON property
23. JSONStringify with null
24. isEmpty(null)
25. assignment through null
26. indexed assignment through null
27. function with no explicit return
28. arrow function with no result
29. null configuration value
30. null search result
```

These tests are based on the supplied Pulsar examples and evaluator behavior rather than introducing additional null semantics not supported by the source material.
