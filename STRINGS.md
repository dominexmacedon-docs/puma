## 1. Overview

Strings are text values in Pulsar.

A string is written inside quotation marks:

```pulsar
"Hello"
```

Strings can be stored in variables, passed to functions, combined with other values, compared, transformed with string builtins, and used inside larger expressions.

The supplied Pulsar examples include dedicated string operations for case conversion, trimming, prefix/suffix checks, searching, replacement, reversal, repetition, and splitting. 

---

# 2. Basic String

A string can be passed directly to `show()`.

```pulsar
show("Hello");
```

Another example:

```pulsar
show("Pulsar");
```

The general form is:

```pulsar
"some text"
```

---

# 3. String Variables

Strings can be assigned to variables using `define`.

```pulsar
define name = "Pulsar";

show(name);
```

The supplied examples demonstrate assigning a string to a variable and displaying it. 

---

# 4. Changing a String Variable

A variable containing a string can be reassigned.

```pulsar
define name = "Puma";

name = "Pulsar";

show(name);
```

The supplied examples explicitly demonstrate string reassignment. 

---

# 5. String Concatenation

The `+` operator combines strings.

```pulsar
show("Hello " + "World");
```

The supplied examples explicitly use `+` for string concatenation. 

---

# 6. Concatenating Variables

```pulsar
define first = "Hello";
define second = "Pulsar";

define message = first + " " + second;

show(message);
```

Result:

```text
Hello Pulsar
```

---

# 7. String Concatenation With Expressions

A string can be combined with the result of another expression.

```pulsar
define name = "Pulsar";
define version = 1;

show(name + " version " + version);
```

The exact conversion behavior depends on the evaluator's runtime value handling.

---

# 8. Strings in Function Arguments

Strings can be passed to functions.

```pulsar
func greet(name) {
    return "Hello " + name;
}

show(greet("Pulsar"));
```

The supplied function examples demonstrate string arguments and string concatenation. 

---

# 9. Strings in Return Expressions

A function can return a string expression.

```pulsar
func message(name) {
    return "Hello " + name;
}

define result = message("Pulsar");

show(result);
```

---

# 10. Strings in Conditions

Strings can participate in equality comparisons.

```pulsar
define name = "Puma";

if name == "Puma" {
    show("matched");
}
```

The supplied examples explicitly demonstrate string comparison in an `if` condition. 

---

# 11. Lowercase Conversion

The `lower()` builtin converts a string to lowercase.

```pulsar
show(lower("HELLO"));
```

The supplied string examples explicitly test `lower()`. 

---

# 12. Lowercase Variable

```pulsar
define text = "PULSAR";

define result = lower(text);

show(result);
```

---

# 13. Uppercase Conversion

The `upper()` builtin converts a string to uppercase.

```pulsar
show(upper("hello"));
```

The supplied examples explicitly test `upper()`. 

---

# 14. Uppercase Variable

```pulsar
define text = "pulsar";

show(upper(text));
```

---

# 15. Trimming Whitespace

The `trim()` builtin removes surrounding whitespace.

```pulsar
show(trim("   Puma   "));
```

The supplied examples explicitly test `trim()`. 

---

# 16. Trim a Variable

```pulsar
define name = "   Pulsar   ";

define cleanName = trim(name);

show(cleanName);
```

---

# 17. Checking a Prefix

`startsWith()` checks whether a string begins with another string.

```pulsar
show(startsWith("Hello Puma", "Hello"));
```

The supplied examples explicitly test this operation. 

---

# 18. Prefix Check With a Condition

```pulsar
define name = "Pulsar Language";

if startsWith(name, "Pulsar") {
    show("Pulsar prefix found");
}
```

---

# 19. Checking a Suffix

`endsWith()` checks whether a string ends with another string.

```pulsar
show(endsWith("Hello Puma", "Puma"));
```

The supplied examples explicitly test `endsWith()`. 

---

# 20. Suffix Check With a Condition

```pulsar
define filename = "program.pulsar";

if endsWith(filename, ".pulsar") {
    show("Pulsar source file");
}
```

---

# 21. Searching a String

`includes()` checks whether one string contains another.

```pulsar
show(includes("Hello Puma", "Puma"));
```

The supplied examples explicitly test `includes()`. 

---

# 22. Includes With a Variable

```pulsar
define text = "Pulsar Programming Language";

if includes(text, "Programming") {
    show("Found");
}
```

---

# 23. Replacing Text

`replace()` replaces matching text.

```pulsar
show(replace("Hello Puma", "Puma", "World"));
```

The supplied examples explicitly test `replace()`. 

---

# 24. Replacement With Variables

```pulsar
define text = "Hello Puma";

define result =
    replace(text, "Puma", "Pulsar");

show(result);
```

---

# 25. Reversing a String

The supplied interpreter examples provide `reverseStr()`.

```pulsar
show(reverseStr("Puma"));
```

The string examples explicitly test this builtin. 

---

# 26. Reverse a Variable

```pulsar
define text = "Pulsar";

show(reverseStr(text));
```

---

# 27. Repeating a String

The supplied interpreter examples provide `repeatStr()`.

```pulsar
show(repeatStr("ha", 3));
```

The supplied examples explicitly test this builtin. 

---

# 28. Repeat With Variables

```pulsar
define text = "Pulsar ";

define result = repeatStr(text, 3);

show(result);
```

---

# 29. Splitting a String

The supplied interpreter examples provide `split()`.

```pulsar
show(split("a,b,c", ","));
```

The supplied examples explicitly test splitting a string using a delimiter. 

---

# 30. Split Into Values

```pulsar
define text = "red,green,blue";

define colors = split(text, ",");

show(colors);
```

The result is an array of separated values.

---

# 31. String Processing Chain

String operations can be combined.

```pulsar
define text = "   HELLO PULSAR   ";

define result =
    lower(trim(text));

show(result);
```

The processing order is:

```text
"   HELLO PULSAR   "
          |
        trim
          |
"HELLO PULSAR"
          |
        lower
          |
"hello pulsar"
```

---

# 32. Multiple String Operations

```pulsar
define text = "   Hello Puma   ";

define clean = trim(text);
define upperText = upper(clean);
define result = replace(upperText, "PUMA", "PULSAR");

show(result);
```

---

# 33. String Operations Inside Functions

```pulsar
func normalize(name) {
    return upper(trim(name));
}

show(normalize("   pulsar   "));
```

This combines:

```text
trim()
upper()
```

into one expression.

---

# 34. String Utility Function

```pulsar
func containsPulsar(text) {
    return includes(text, "Pulsar");
}

show(containsPulsar("Pulsar Language"));
```

---

# 35. String Prefix Function

```pulsar
func isPulsarFile(filename) {
    return startsWith(filename, "Pulsar");
}

show(isPulsarFile("PulsarDocs"));
```

---

# 36. String Suffix Function

```pulsar
func isSourceFile(filename) {
    return endsWith(filename, ".pulsar");
}

show(isSourceFile("main.pulsar"));
```

---

# 37. String Transformation

```pulsar
func formatName(name) {
    return upper(trim(name));
}

define name = formatName("   pulsar   ");

show(name);
```

---

# 38. Strings in Arrays

Strings can be stored in arrays.

```pulsar
define names = [
    "Pulsar",
    "Puma",
    "Dominex"
];

show(names);
```

The supplied examples also demonstrate arrays containing mixed types, including strings. 

---

# 39. Accessing Strings From Arrays

```pulsar
define names = [
    "Pulsar",
    "Puma",
    "Dominex"
];

show(names[0]);
```

The array-indexing syntax is part of the expression system.

---

# 40. String Processing With `map`

String values can be processed with the supplied `map()` builtin.

```pulsar
define names = [
    "pulsar",
    "puma",
    "dominex"
];

show(map(names, x => upper(x)));
```

The supplied examples explicitly demonstrate mapping `upper()` over an array of strings. 

---

# 41. Filtering Strings

Strings can be filtered using a predicate.

```pulsar
define names = [
    "Pulsar",
    "Puma",
    "Dominex"
];

define result =
    filter(names, x => startsWith(x, "P"));

show(result);
```

---

# 42. String Reduction

Strings can also be combined through `reduce()`.

```pulsar
define values = [
    "Pulsar",
    "Language"
];

define result =
    reduce(values, (a, b) => a + " " + b, "");

show(result);
```

The supplied examples establish `reduce()` as a built-in operation for arrays. 

---

# 43. Strings and Objects

Strings can be stored as object properties.

```pulsar
define user = {
    name: "Pulsar",
    role: "Developer"
};

show(user.name);
```

The supplied object examples demonstrate string-valued object properties and property access. 

---

# 44. Nested String Properties

```pulsar
define user = {
    profile: {
        name: "Pulsar"
    }
};

show(user.profile.name);
```

The supplied examples demonstrate nested object access. 

---

# 45. Changing String Object Properties

```pulsar
define user = {
    name: "Puma"
};

user.name = "Pulsar";

show(user.name);
```

The supplied examples explicitly demonstrate modifying a string-valued object property. 

---

# 46. Strings and JSON

Strings can represent serialized JSON data.

For example:

```pulsar
define text = "{\"name\":\"Pulsar\"}";
```

The supplied JSON examples use JSON strings with `JSONParse()` and `JSONStringify()`. 

---

# 47. Parsing JSON From a String

```pulsar
define text = "{\"name\":\"Pulsar\"}";

define data = JSONParse(text);

show(data.name);
```

The supplied examples demonstrate parsing JSON text and accessing the resulting object's property. 

---

# 48. Converting an Object to a String

`JSONStringify()` converts structured data into JSON text.

```pulsar
define data = {
    name: "Pulsar"
};

define text = JSONStringify(data);

show(text);
```

The supplied examples explicitly demonstrate this conversion. 

---

# 49. String Round Trip

A value can be converted to JSON text and parsed back.

```pulsar
define data = {
    name: "Pulsar",
    scores: [90, 95]
};

define encoded = JSONStringify(data);
define decoded = JSONParse(encoded);

show(decoded.name);
show(decoded.scores);
```

The supplied examples demonstrate this complete encode/decode cycle. 

---

# 50. Strings and Closures

Strings can be captured by functions.

```pulsar
define prefix = "Hello ";

func greet(name) {
    return prefix + name;
}

show(greet("Pulsar"));
```

The supplied closure examples explicitly demonstrate a string variable being captured and used by a function. 

---

# 51. Strings in Arrow Functions

```pulsar
define greet = name => "Hello " + name;

show(greet("Pulsar"));
```

The supplied arrow-function examples explicitly demonstrate this pattern. 

---

# 52. Arrow Function With String Processing

```pulsar
define normalize = text => upper(trim(text));

show(normalize("   pulsar   "));
```

This combines arrow functions with string builtins.

---

# 53. String Comparison

```pulsar
define language = "Pulsar";

if language == "Pulsar" {
    show("Correct");
}
```

Strings can therefore participate in the normal equality-expression system.

---

# 54. String Search

```pulsar
define message = "Pulsar is a programming language";

if includes(message, "programming") {
    show("Found");
}
```

---

# 55. Filename Validation

```pulsar
func validSourceFile(filename) {
    return endsWith(filename, ".pulsar");
}

show(validSourceFile("main.pulsar"));
show(validSourceFile("main.txt"));
```

---

# 56. Username Normalization

```pulsar
func normalizeUsername(username) {
    return lower(trim(username));
}

define username =
    normalizeUsername("   PULSAR   ");

show(username);
```

---

# 57. String Replacement Pipeline

```pulsar
define message = "Hello Puma";

define result =
    replace(
        upper(message),
        "PUMA",
        "PULSAR"
    );

show(result);
```

---

# 58. Splitting and Processing

```pulsar
define text = "pulsar,puma,dominex";

define names = split(text, ",");

define upperNames =
    map(names, x => upper(x));

show(upperNames);
```

---

# 59. String Repetition

```pulsar
define separator = repeatStr("-", 20);

show(separator);
```

This is useful for generating simple text output.

---

# 60. Reversing Text

```pulsar
define text = "Pulsar";

define reversed = reverseStr(text);

show(reversed);
```

The supplied interpreter examples explicitly provide `reverseStr()`. 

---

# 61. Combining Multiple Builtins

```pulsar
define input = "   hello pulsar   ";

define result =
    upper(
        reverseStr(
            trim(input)
        )
    );

show(result);
```

The expression is evaluated from the innermost operation outward:

```text
input
  ↓
trim
  ↓
reverseStr
  ↓
upper
  ↓
result
```

---

# 62. String Utility Example

```pulsar
func describe(text) {
    define clean = trim(text);

    show("Original: " + text);
    show("Clean: " + clean);
    show("Upper: " + upper(clean));
    show("Lower: " + lower(clean));
}

describe("   Pulsar Language   ");
```

---

# 63. Complete String Example

```pulsar
define name = "   Pulsar   ";

define cleanName = trim(name);
define upperName = upper(cleanName);
define lowerName = lower(cleanName);

if includes(lowerName, "pulsar") {
    show("Language name found");
}

show(cleanName);
show(upperName);
show(lowerName);
```

---

# 64. String Builtin Reference

The supplied interpreter examples establish the following string-related builtins:

| Builtin        | Purpose                       | Example                     |
| -------------- | ----------------------------- | --------------------------- |
| `lower()`      | Convert to lowercase          | `lower("HELLO")`            |
| `upper()`      | Convert to uppercase          | `upper("hello")`            |
| `trim()`       | Remove surrounding whitespace | `trim("  text  ")`          |
| `startsWith()` | Test beginning of string      | `startsWith(text, "Hi")`    |
| `endsWith()`   | Test end of string            | `endsWith(text, ".pulsar")` |
| `includes()`   | Search for text               | `includes(text, "Pulsar")`  |
| `replace()`    | Replace text                  | `replace(text, "A", "B")`   |
| `reverseStr()` | Reverse text                  | `reverseStr("Puma")`        |
| `repeatStr()`  | Repeat text                   | `repeatStr("ha", 3)`        |
| `split()`      | Split text into values        | `split("a,b", ",")`         |

These operations are directly represented in the supplied `EXAMPLES.md` string section. 

---

# 65. String Feature Summary

Pulsar strings can be used for:

```text
Literal text
Variable values
Concatenation
Equality comparisons
Function arguments
Function return values
Object properties
Array elements
JSON text
Prefix checking
Suffix checking
Substring searching
Text replacement
Case conversion
Whitespace trimming
String reversal
String repetition
String splitting
Map/filter/reduce processing
Arrow-function expressions
Conditional expressions
```

The supplied examples demonstrate these string operations through standalone examples, functions, closures, arrow functions, arrays, objects, and JSON.  

---

# 66. Recommended String Tests

For testing the Pulsar interpreter, use this order:

```text
1. Basic string literal
2. String variable
3. String reassignment
4. String concatenation
5. String comparison
6. lower()
7. upper()
8. trim()
9. startsWith()
10. endsWith()
11. includes()
12. replace()
13. reverseStr()
14. repeatStr()
15. split()
16. Strings in arrays
17. Strings in objects
18. Strings in functions
19. Strings in arrow functions
20. Strings with JSON
21. Chained string operations
22. String processing with map/filter/reduce
```