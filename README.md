# Puma Language (`.pulsar`) Guide

Welcome to the Puma programming language repository! If you're working with Puma, you'll notice our source files use the `.pulsar` extension. This guide will help you get set up, explain how to handle file associations properly, and walk you through the core syntax and features.

---

## Getting Started

### Installation

To get Puma up and running on your system, grab the official installer executable from the releases page:

* **Download Link**: [puma-v1.0.0.exe](https://github.com/dominexmacedon-docs/puma/releases/download/puma-v1.0.0/puma-v1.0.0.exe)


### A Quick Note on Opening `.pulsar` Files

When you first double-click a `.pulsar` file on your computer, your OS will likely ask you what program you want to use to open it.

> **Important:** When this prompt pops up, **make sure you do not check or enable the box that says "Always open with..."**. This prevents your operating system from permanently locking the `.pulsar` extension to a single text editor or viewer.
> 
> 

---

## Language Features & Code Structure

Puma is built on custom compiler tokens and a solid Lexer/Parser layer. The evaluator core supports everything from asynchronous tasks and web routing to database models and object-oriented programming.

### Variables and Constants

Declare variables easily using the `define` keyword:

```pulsar
define greeting = "Hello, Puma!";
define count = 42;

```

### Printing Output (`show`)

To output data to your terminal or console, use the `show(...)` statement:

```pulsar
show("Welcome to Puma programming language.");

```

### Control Flow

Puma handles conditional logic (`if`, `else`) and loops (`while`, `for`, `for-in`) just like you'd expect:

```pulsar
define score = 85;

if (score >= 80) {
    show("Great job!");
} else {
    show("Keep trying!");
}

define i = 0;
while (i < 3) {
    show(i);
    i++;
}

```

### Functions & Arrow Syntax

Functions can be defined the traditional way using `func`, or you can use concise arrow functions (`=>`):

```pulsar
func add(a, b) {
    return a + b;
}

define multiply = (x, y) => x * y;

```

### Object-Oriented Programming

Organize your code using `entity`, inherit from other classes with `inherits`, and initialize properties using `init`:

```pulsar
entity Animal {
    init(name) {
        self.name = name;
    }
    speak() {
        show(self.name + " makes a noise.");
    }
}

entity Dog inherits Animal {
    speak() {
        show(self.name + " barks.");
    }
}

```

### Web Servers and APIs

Puma comes with built-in networking utilities like `createServer`, making it straightforward to spin up web backends, manage cookies, parse multipart file uploads, and handle WebSockets:

```pulsar
define app = createServer({ enableWebSockets: true });

app.get("/", (req, res) => {
    res.send("Hello from Puma Web Server!");
});

app.listen(3000, (port) => {
    show("Server running on port " + port);
});

```

---

## Sample `.pulsar` Script

Here is a complete, working script that puts variables, functions, conditions, and console logs together:

```pulsar
#* 
  Sample Puma Script (.pulsar)
  Demonstrating basic syntax features
*#

define appName = "Puma Engine";
define version = 1.0;

func getInfo(name, ver) {
    return name + " version " + ver + " is running smoothly.";
}

define statusMessage = getInfo(appName, version);
show(statusMessage);

define numbers = [10, 20, 30, 40];
for item in numbers {
    if (item > 20) {
        show("High value detected: " + item);
    }
}
```
