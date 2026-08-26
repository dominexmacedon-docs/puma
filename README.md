# Puma Language (`.pulsar`) Guide

Welcome to the **Puma Programming Language** repository!

Puma source files use the `.pulsar` extension. This guide explains how to install Puma, configure your environment, run `.pulsar` programs, and learn the core language syntax.

---

# Getting Started

## Installation

Puma is available for Windows and Linux.

---

# Windows Installation

Download the official installer:

**Download:**

https://github.com/dominexmacedon-docs/puma/releases/download/puma-v1.0.1/puma-v1.0.1.exe

The installer includes:

- Puma runtime
- Compiler components
- CLI command
- `.pulsar` file association

After installation, you can run:

```bash
puma program.pulsar
````

---

# Linux Installation

Puma Linux installation uses a Makefile installer.

## Requirements

Make sure your system has:

* Node.js 22+
* Make
* wget

Check:

```bash
node --version
make --version
```

---

## Install Puma

Create a file named:

```text
Makefile
```

Add:

```makefile
PUMA_VERSION=puma-linux-v1.0.1
PUMA_URL=https://github.com/dominexmacedon-docs/puma/releases/download/puma-linux-v1.0.1/Puma-linux-v1.0.1.tar.gz

PREFIX=/usr/local
PUMA_LIB=$(PREFIX)/lib/puma
PUMA_BIN=$(PREFIX)/bin/puma


.PHONY: install clean download extract setup launcher


install: download extract setup launcher
	@echo "Puma installed successfully"
	@echo "Run: puma your_file.pulsar"


download:
	@echo "Downloading Puma..."
	wget -O $(PUMA_VERSION).tar.gz $(PUMA_URL)


extract:
	@echo "Extracting Puma..."
	rm -rf $(PUMA_VERSION)
	tar -xzf $(PUMA_VERSION).tar.gz


setup:
	@echo "Installing Puma runtime..."

	sudo mkdir -p $(PUMA_LIB)/.runtime

	RUNTIME_DIR=$$(find . -type d -name ".runtime" | head -n 1); \
	if [ -z "$$RUNTIME_DIR" ]; then \
		echo "ERROR: .runtime folder not found"; \
		exit 1; \
	fi; \
	sudo cp -r $$RUNTIME_DIR/* $(PUMA_LIB)/.runtime/


launcher:
	@echo "Creating global Puma command..."

	sudo sh -c 'printf "#!/bin/bash\n\nexec node /usr/local/lib/puma/.runtime/puma.js \"\$$@\"\n" > $(PUMA_BIN)'

	sudo chmod +x $(PUMA_BIN)


clean:
	rm -rf $(PUMA_VERSION)
	rm -f $(PUMA_VERSION).tar.gz
```

Run:

```bash
make install
```

After installation:

```bash
puma hello.pulsar
```

Puma will be installed globally:

```text
/usr/local/bin/puma

/usr/local/lib/puma/
└── .runtime/
    ├── puma.js
    ├── lexer.js
    ├── parser.js
    ├── evaluator.js
    └── node_modules/
```

---

# Running Puma Programs

Create:

```text
hello.pulsar
```

Example:

```pulsar
show("Hello from Puma!");
```

Run:

```bash
puma hello.pulsar
```

---

# `.pulsar` File Handling

When opening a `.pulsar` file for the first time, your operating system may ask which application should open it.

> Important:
>
> Do not enable "Always open with..." unless you specifically want to permanently associate `.pulsar` files with Puma.

This allows your system to keep the file association flexible.

---

# Language Features & Code Structure

Puma uses a custom Lexer, Parser, and Evaluator architecture.

The runtime supports:

* Variables
* Functions
* Arrow functions
* Conditions
* Loops
* Async tasks
* Web servers
* APIs
* Entities and inheritance
* Database models
* Networking utilities

---

# Variables

Use `define` to create variables:

```pulsar
define greeting = "Hello, Puma!";
define count = 42;
```

---

# Output (`show`)

Print values:

```pulsar
show("Welcome to Puma!");
```

---

# Control Flow

## If / Else

```pulsar
define score = 85;

if (score >= 80) {
    show("Great job!");
} else {
    show("Keep trying!");
}
```

---

## While Loop

```pulsar
define i = 0;

while (i < 3) {
    show(i);
    i++;
}
```

---

## For-In Loop

```pulsar
define numbers = [10,20,30,40];

for item in numbers {

    show(item);

}
```

---

# Functions

Traditional functions:

```pulsar
func add(a, b) {

    return a + b;

}

show(add(5,10));
```

---

# Arrow Functions

Short function syntax:

```pulsar
define multiply = (x,y) => x * y;

show(multiply(4,5));
```

---

# Object-Oriented Programming

Puma supports:

* `entity`
* `inherits`
* `init`
* `self`

Example:

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

---

# Web Servers and APIs

Puma includes built-in server utilities.

Example:

```pulsar
define app = createServer({
    enableWebSockets: true
});


app.get("/", (req,res)=>{

    res.send("Hello from Puma Web Server!");

});


app.listen(3000,(port)=>{

    show("Server running on port " + port);

});
```

Run:

```bash
puma server.pulsar
```

---

# Complete Example

`example.pulsar`

```pulsar
#*
 Sample Puma Script

 Demonstrates:
 - Variables
 - Functions
 - Conditions
 - Loops
*#


define appName = "Puma Engine";

define version = 1.0;


func getInfo(name, ver) {

    return name + " version " + ver + " is running smoothly.";

}


define statusMessage = getInfo(appName, version);


show(statusMessage);



define numbers = [10,20,30,40];


for item in numbers {

    if (item > 20) {

        show("High value detected: " + item);

    }

}
```

Run:

```bash
puma example.pulsar
```

---

# Puma Project Structure

Typical Puma installation:

```text
Puma
│
├── puma

```

The `.runtime` directory contains Puma's execution engine.

Users interact with Puma through:

```bash
puma file.pulsar
```

---

# Version

Current version:

```text
Puma v1.0.1
```

