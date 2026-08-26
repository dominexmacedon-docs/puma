## 1. Overview

Pulsar provides builtins for:

* General values
* Strings
* Numbers and mathematics
* Arrays
* Objects
* JSON
* Functional programming
* Filesystem operations
* Environment variables
* HTTP requests
* Time and dates
* URL encoding
* Cryptographic hashing
* Utility operations
* Server functionality

The supplied `EXAMPLES.md` also organizes builtin-related examples into Math Builtins, Object Builtins, Array Builtins, Files, and Environment sections. 

---

# 2. General Builtins

## `len()`

Returns the length of a string or array, or the number of keys in an object.

```pulsar
show(len("Pulsar"));
show(len([1, 2, 3]));
show(len({
    name: "Puma",
    age: 20
}));
```

Behavior:

```text
string  → string length
array   → array length
object  → number of keys
other   → 0
```



---

## `toStr()`

Converts a value to a string.

```pulsar
show(toStr(123));
show(toStr(true));
show(toStr([1, 2, 3]));
```



---

## `str()`

Also converts a value to a string.

```pulsar
show(str(123));
show(str(true));
```

The evaluator defines `str()` as `String(arg)`. 

---

## `type()`

Returns the JavaScript-style type, with arrays reported specifically as `"array"`.

```pulsar
show(type("hello"));
show(type(10));
show(type(true));
show(type([1, 2]));
show(type({ name: "Puma" }));
```

For an array:

```text
array
```

rather than:

```text
object
```



---

## `isNaN()`

Tests whether a value is not a valid number or is `NaN`.

```pulsar
show(isNaN(10));
show(isNaN("hello"));
show(isNaN("123"));
```

The implementation returns `true` for values that are not numbers as well as for `NaN`. 

---

# 3. String Builtins

## `lower()`

Converts a value to lowercase.

```pulsar
show(lower("HELLO"));
```



---

## `upper()`

Converts a value to uppercase.

```pulsar
show(upper("hello"));
```



---

## `trim()`

Removes whitespace from both ends.

```pulsar
show(trim("   Pulsar   "));
```



---

## `trimStart()`

Removes whitespace from the beginning.

```pulsar
show(trimStart("   Pulsar"));
```



---

## `trimEnd()`

Removes whitespace from the end.

```pulsar
show(trimEnd("Pulsar   "));
```



---

## `startsWith()`

Checks whether a string starts with a specified prefix.

```pulsar
show(startsWith("Hello Pulsar", "Hello"));
```

Returns a boolean. 

---

## `endsWith()`

Checks whether a string ends with a specified suffix.

```pulsar
show(endsWith("Hello Pulsar", "Pulsar"));
```



---

## `includes()`

Checks whether a string contains another string.

```pulsar
show(includes("Hello Pulsar", "Pulsar"));
```



---

## `repeat()`

Repeats a string.

```pulsar
show(repeat("ha", 3));
```

Result:

```text
hahaha
```



---

## `repeatStr()`

Another string repetition builtin.

```pulsar
show(repeatStr("ab", 3));
```



---

## `replace()`

Replaces occurrences of a string.

```pulsar
show(replace(
    "Hello Puma",
    "Puma",
    "Pulsar"
));
```

The implementation uses string splitting and joining, so the replacement applies to all matching occurrences. 

---

## `split()`

Splits a string into an array.

```pulsar
define parts = split("a,b,c", ",");
show(parts);
```



---

## `join()`

Joins an array into a string.

```pulsar
define values = ["Pulsar", "Language"];
show(join(values, " "));
```

`join()` requires an array. 

---

## `substring()`

Extracts part of a string.

```pulsar
show(substring("Pulsar", 0, 3));
```



---

## `padStart()`

Pads the beginning of a string.

```pulsar
show(padStart("42", 5, "0"));
```



---

## `padEnd()`

Pads the end of a string.

```pulsar
show(padEnd("42", 5, "0"));
```



---

## `capitalize()`

Capitalizes the first character.

```pulsar
show(capitalize("pulsar"));
```



---

## `reverseStr()`

Reverses a string.

```pulsar
show(reverseStr("Pulsar"));
```



---

## `camelCase()`

Converts a string toward camelCase formatting.

```pulsar
show(camelCase("hello world"));
show(camelCase("hello-world"));
```



---

## `kebabCase()`

Converts a string toward kebab-case formatting.

```pulsar
show(kebabCase("Hello World"));
show(kebabCase("helloWorld"));
```



---

# 4. Number and Math Builtins

## `floor()`

```pulsar
show(floor(4.8));
```



## `ceil()`

```pulsar
show(ceil(4.2));
```



## `round()`

```pulsar
show(round(4.6));
```



## `abs()`

```pulsar
show(abs(-10));
```



## `pow()`

```pulsar
show(pow(2, 8));
```



## `sqrt()`

```pulsar
show(sqrt(25));
```



## `min()`

```pulsar
show(min(10, 5, 20));
```

## `max()`

```pulsar
show(max(10, 5, 20));
```

The evaluator converts the arguments to numbers before calculating these values. 

---

## `random()`

With one argument:

```pulsar
show(random(10));
```

produces an integer from `0` through `9`.

With two arguments:

```pulsar
show(random(5, 10));
```

produces an integer in the implementation's `[min, max)` range. 

---

## `randomInt()`

Produces an integer between the supplied minimum and maximum, inclusive.

```pulsar
show(randomInt(1, 10));
```



---

## `randomFloat()`

Produces a random floating-point value between the supplied bounds.

```pulsar
show(randomFloat(0, 1));
```



---

## `clamp()`

Restricts a value to a range.

```pulsar
show(clamp(150, 0, 100));
```

Result:

```text
100
```



---

## `sign()`

Returns the sign of a number.

```pulsar
show(sign(-10));
show(sign(10));
show(sign(0));
```



---

## `lerp()`

Performs linear interpolation.

```pulsar
show(lerp(0, 100, 0.5));
```



---

## `degToRad()`

Converts degrees to radians.

```pulsar
show(degToRad(180));
```

## `radToDeg()`

Converts radians to degrees.

```pulsar
show(radToDeg(3.141592653589793));
```



---

# 5. Array Builtins

## `push()`

Adds an item to an array and returns the new array length.

```pulsar
define values = [1, 2];

show(push(values, 3));
show(values);
```



---

## `pop()`

Removes and returns the last element.

```pulsar
define values = [1, 2, 3];

show(pop(values));
show(values);
```



---

## `shift()`

Removes and returns the first element.

```pulsar
define values = [1, 2, 3];

show(shift(values));
show(values);
```



---

## `unshift()`

Adds an element to the beginning and returns the new length.

```pulsar
define values = [2, 3];

show(unshift(values, 1));
show(values);
```



---

## `sort()`

Sorts an array.

```pulsar
define values = [3, 1, 2];

show(sort(values));
```

An optional function can be supplied according to the evaluator implementation. 

---

## `reverse()`

Reverses an array.

```pulsar
define values = [1, 2, 3];

show(reverse(values));
```



---

## `unique()`

Removes duplicate values.

```pulsar
show(unique([1, 2, 2, 3, 3]));
```



---

## `indexOf()`

Finds the index of a value.

```pulsar
show(indexOf([10, 20, 30], 20));
```



---

## `includesArr()`

Checks whether an array contains a value.

```pulsar
show(includesArr([10, 20, 30], 20));
```



---

## `flatten()`

Flattens nested arrays.

```pulsar
define values = [1, [2, [3, 4]]];

show(flatten(values));
```

The evaluator uses infinite-depth flattening. 

---

## `randomChoice()`

Selects a random array element.

```pulsar
define colors = ["red", "green", "blue"];

show(randomChoice(colors));
```



---

## `count()`

Counts occurrences of a value.

```pulsar
show(count(
    [1, 2, 2, 3, 2],
    2
));
```



---

## `uniqueBy()`

Creates an array containing unique elements according to a function or value.

```pulsar
define values = [1, 2, 2, 3, 3];

show(uniqueBy(values));
```

The evaluator tracks already-seen keys using a `Set`. 

---

# 6. Functional Builtins

## `map()`

Transforms every array element.

```pulsar
define values = [1, 2, 3];

show(map(
    values,
    x => x * 2
));
```

The callback receives:

```text
value
index
array
```



---

## `filter()`

Keeps elements for which the callback returns a truthy value.

```pulsar
define values = [1, 2, 3, 4];

show(filter(
    values,
    x => x % 2 == 0
));
```



---

## `reduce()`

Reduces an array to one value.

```pulsar
define values = [1, 2, 3, 4];

show(reduce(
    values,
    (a, b) => a + b,
    0
));
```

The callback receives:

```text
accumulator
current value
index
array
```



Without an initial value:

```pulsar
show(reduce(
    [1, 2, 3],
    (a, b) => a + b
));
```

The first array element becomes the initial accumulator. An empty array without an initial value produces a runtime error. 

---

# 7. Object Builtins

## `hasOwn()`

Checks whether an object directly owns a property.

```pulsar
define user = {
    name: "Puma"
};

show(hasOwn(user, "name"));
show(hasOwn(user, "age"));
```



---

## `keys()`

Returns an object's keys.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(keys(user));
```



---

## `values()`

Returns an object's values.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(values(user));
```



---

## `entries()`

Returns an object's key/value entries.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(entries(user));
```



---

## `invert()`

Creates an object whose values become keys.

```pulsar
define data = {
    a: "one",
    b: "two"
};

show(invert(data));
```



---

## `isEmpty()`

Checks whether a value is empty.

```pulsar
show(isEmpty([]));
show(isEmpty(""));
show(isEmpty({}));
```

For `null` or `undefined`, it also returns `true`. 

---

## `deepClone()`

Creates a JSON-based deep copy.

```pulsar
define original = {
    user: {
        name: "Puma"
    }
};

define copy = deepClone(original);

show(copy);
```



---

## `getProp()`

Gets a nested object property using dot notation.

```pulsar
define user = {
    profile: {
        name: "Puma"
    }
};

show(getProp(
    user,
    "profile.name"
));
```

A default value can be supplied:

```pulsar
show(getProp(
    user,
    "profile.age",
    0
));
```



---

## `setProp()`

Sets a nested property.

```pulsar
define user = {};

setProp(
    user,
    "profile.name",
    "Puma"
);

show(user);
```

Missing intermediate objects are created automatically. 

---

## `mergeDeep()`

Deep-merges two objects.

```pulsar
define a = {
    user: {
        name: "Puma"
    }
};

define b = {
    user: {
        age: 20
    }
};

show(mergeDeep(a, b));
```

Nested objects are merged recursively. 

---

# 8. JSON Builtins

## `JSONParse()`

Converts a JSON string into a Pulsar value.

```pulsar
define text = "{\"name\":\"Puma\"}";

define data = JSONParse(text);

show(data.name);
```

The argument must be a string. Invalid JSON raises a runtime error. 

---

## `JSONStringify()`

Converts a value to JSON text.

```pulsar
define data = {
    name: "Puma",
    age: 20
};

show(JSONStringify(data));
```



---

## `readJSON()`

Reads a file and parses its contents as JSON.

```pulsar
define data = readJSON("data.json");

show(data);
```

It internally uses `readFile()` followed by `JSON.parse()`. 

---

## `writeJSON()`

Writes a value to a JSON file.

```pulsar
define data = {
    name: "Puma",
    active: true
};

writeJSON(
    "data.json",
    data
);
```

The JSON is written with indentation. 

---

# 9. Filesystem Builtins

## `readFile()`

Reads UTF-8 text from a file.

```pulsar
define content = readFile("hello.txt");

show(content);
```



---

## `writeFile()`

Writes text to a file.

```pulsar
writeFile(
    "hello.txt",
    "Hello from Pulsar"
);
```

Returns `true` when successful. 

---

## `appendFile()`

Appends text to an existing file.

```pulsar
appendFile(
    "log.txt",
    "New entry\n"
);
```



---

## `exists()`

Checks whether a filesystem path exists.

```pulsar
show(exists("hello.txt"));
```



---

## `mkdir()`

Creates a directory recursively when necessary.

```pulsar
mkdir("data/users");
```

Returns `true`. 

---

## `deleteFile()`

Deletes a file.

```pulsar
show(deleteFile("hello.txt"));
```

Returns `false` when the file does not exist. 

---

## `rmdir()`

Removes a directory recursively.

```pulsar
show(rmdir("data"));
```



---

# 10. Time Builtins

## `now()`

Returns the current timestamp.

```pulsar
define timestamp = now();

show(timestamp);
```



---

## `formatDate()`

Formats a timestamp using locale and formatting options.

```pulsar
show(formatDate());
```

A timestamp can also be supplied:

```pulsar
show(formatDate(
    now(),
    "en-US"
));
```



---

## `sleep()`

Asynchronously waits for a specified number of milliseconds.

```pulsar
show("before");

await sleep(1000);

show("after");
```

The evaluator defines `sleep()` using a Promise and `setTimeout`. 

---

# 11. HTTP Builtins

## `fetch()`

Performs an HTTP request and returns an object containing:

```text
status
ok
text()
json()
```

Example:

```pulsar
define response = await fetch(
    "https://example.com"
);

show(response.status);
```

The evaluator wraps the native fetch response. 

---

## `get()`

Performs a GET request and parses the response as JSON.

```pulsar
define data = await get(
    "https://example.com/api/data"
);

show(data);
```



---

## `post()`

Sends a JSON POST request.

```pulsar
define result = await post(
    "https://example.com/api/users",
    {
        name: "Puma"
    }
);

show(result);
```

The implementation sends JSON with:

```text
Content-Type: application/json
```



---

## `httpFetch()`

The evaluator also exposes a lower-level HTTP client.

```pulsar
define response = await httpFetch(
    "https://example.com"
);

show(response.status);
show(response.body);
```

It supports HTTP/HTTPS requests and accepts options such as method, headers, and body. JSON responses are parsed when the response content type indicates JSON. 

---

# 12. URL Builtins

## `encodeURLComponent()`

Encodes a value for use as a URL component.

```pulsar
show(encodeURLComponent(
    "hello world"
));
```



---

## URL Encoding Expression

The evaluator also directly handles the `UrlencodeExpression` AST node.

This is separate from the `encodeURLComponent()` builtin. 

---

# 13. Environment Builtins

## `getEnv()`

Reads an environment variable.

```pulsar
define value = getEnv("PORT");

show(value);
```

A fallback can be supplied:

```pulsar
define port = getEnv(
    "PORT",
    "3000"
);

show(port);
```

The evaluator returns the fallback when the environment variable is not defined. 

---

## `process`

The evaluator also exposes the Node.js `process` object globally.

```pulsar
show(process);
```

This is a host-runtime object rather than a normal Pulsar function. 

---

# 14. Cryptographic Builtins

## `sha256()`

Calculates the SHA-256 hash of text.

```pulsar
define hash = sha256("hello");

show(hash);
```

The implementation converts the input to a string and returns the hexadecimal digest. 

---

# 15. Built-in Global Objects

The evaluator also exposes several JavaScript globals directly.

## `Date`

```pulsar
show(Date);
```

## `Math`

```pulsar
show(Math);
```

## `String`

```pulsar
show(String);
```

These are explicitly registered in the evaluator. 

---

# 16. Array Range

## `range()`

Creates an array of numbers.

### One argument

```pulsar
show(range(5));
```

Conceptually:

```text
[0, 1, 2, 3, 4]
```

### Two arguments

```pulsar
show(range(2, 6));
```

### Three arguments

```pulsar
show(range(0, 10, 2));
```

The implementation supports one, two, or three arguments:

```text
range(end)
range(start, end)
range(start, end, step)
```

A zero step produces a runtime error. 

---

# 17. Object Inspection

These builtins are particularly useful for dynamic programs.

```pulsar
define user = {
    name: "Puma",
    age: 20
};

show(keys(user));
show(values(user));
show(entries(user));
show(hasOwn(user, "name"));
```

The evaluator directly exposes these operations. 

---

# 18. Builtin Error Behavior

Many builtins validate their input.

For example:

```pulsar
push("hello", 10);
```

is invalid because `push()` expects an array.

The evaluator raises:

```text
push() expects an array
```

Similarly:

```pulsar
join("hello", ",");
```

raises:

```text
join() expects an array
```

The builtin implementations explicitly perform these checks and throw `RuntimeError` when the type is invalid. 

---

# 19. Builtin Categories

The evaluator's builtin system can therefore be summarized as:

| Category     | Builtins                                                                                                                                                                                                                           |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| General      | `len`, `toStr`, `str`, `type`, `isNaN`                                                                                                                                                                                             |
| Strings      | `lower`, `upper`, `trim`, `trimStart`, `trimEnd`, `startsWith`, `endsWith`, `includes`, `repeat`, `repeatStr`, `replace`, `split`, `join`, `substring`, `padStart`, `padEnd`, `capitalize`, `reverseStr`, `camelCase`, `kebabCase` |
| Math         | `random`, `randomInt`, `randomFloat`, `floor`, `ceil`, `round`, `abs`, `pow`, `sqrt`, `min`, `max`, `clamp`, `sign`, `lerp`, `degToRad`, `radToDeg`                                                                                |
| Arrays       | `push`, `pop`, `shift`, `unshift`, `sort`, `reverse`, `unique`, `indexOf`, `includesArr`, `flatten`, `randomChoice`, `count`, `uniqueBy`, `range`                                                                                  |
| Functional   | `map`, `filter`, `reduce`                                                                                                                                                                                                          |
| Objects      | `hasOwn`, `keys`, `values`, `entries`, `invert`, `isEmpty`, `deepClone`, `getProp`, `setProp`, `mergeDeep`                                                                                                                         |
| JSON         | `JSONParse`, `JSONStringify`, `readJSON`, `writeJSON`                                                                                                                                                                              |
| Files        | `readFile`, `writeFile`, `appendFile`, `exists`, `mkdir`, `deleteFile`, `rmdir`                                                                                                                                                    |
| Time         | `now`, `formatDate`, `sleep`                                                                                                                                                                                                       |
| HTTP         | `fetch`, `get`, `post`, `httpFetch`                                                                                                                                                                                                |
| URL          | `encodeURLComponent`                                                                                                                                                                                                               |
| Environment  | `getEnv`, `process`                                                                                                                                                                                                                |
| Cryptography | `sha256`                                                                                                                                                                                                                           |
| Host globals | `Date`, `Math`, `String`                                                                                                                                                                                                           |

This list is derived from the supplied `evaluator.js` rather than inferred from the language documentation.    

---

# 20. Example: Combining Builtins

```pulsar
define users = [
    {
        name: "Puma",
        active: true
    },
    {
        name: "Alex",
        active: false
    },
    {
        name: "Maya",
        active: true
    }
];

define activeUsers = filter(
    users,
    user => user.active
);

define names = map(
    activeUsers,
    user => upper(user.name)
);

show(names);
```

This combines `filter()` and `map()` with object properties and `upper()`. The supplied examples also demonstrate this style of functional composition. 

---

# 21. Example: File and JSON Builtins

```pulsar
define user = {
    name: "Puma",
    active: true
};

writeJSON(
    "user.json",
    user
);

define loaded = readJSON(
    "user.json"
);

show(loaded.name);
show(loaded.active);
```

`writeJSON()` serializes the value and delegates to `writeFile()`, while `readJSON()` reads the file and parses the JSON. 

---

# 22. Example: Range and Map

```pulsar
define numbers = range(1, 6);

define squares = map(
    numbers,
    x => x * x
);

show(squares);
```

The combination is useful for generating and transforming sequences. `range()` produces the sequence and `map()` calls the supplied function for each element.  

---

# 23. Example: String Processing

```pulsar
define text = "   hello pulsar   ";

define cleaned = trim(text);
define title = capitalize(cleaned);
define result = upper(title);

show(result);
```

The evaluator supplies each of these string operations directly.  

---

# 24. Example: Object Manipulation

```pulsar
define user = {};

setProp(
    user,
    "profile.name",
    "Puma"
);

setProp(
    user,
    "profile.role",
    "Developer"
);

show(getProp(
    user,
    "profile.name"
));

show(keys(user.profile));
```

`setProp()` creates missing intermediate objects, while `getProp()` traverses nested keys using dot notation. 

---

# 25. Example: HTTP and JSON

```pulsar
define response = await fetch(
    "https://example.com/api/data"
);

if (response.ok) {
    define data = await response.json();
    show(data);
}
```

The supplied evaluator's `fetch()` wrapper exposes `status`, `ok`, `text()`, and `json()`. 

---

# 26. Example: Environment Configuration

```pulsar
define port = getEnv(
    "PORT",
    "3000"
);

show(port);
```

This allows a Pulsar program to use an environment variable while providing a fallback. 

---

# 27. Example: Hashing

```pulsar
define text = "Pulsar";

define hash = sha256(text);

show(hash);
```

`sha256()` returns a hexadecimal SHA-256 digest. 

---

# 28. Example: Utility Pipeline

```pulsar
define values = [1, 2, 3, 4, 5];

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

This uses three of Pulsar's functional builtins together: `map()`, `filter()`, and `reduce()`. 
