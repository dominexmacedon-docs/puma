## Importing NPM Packages

LopoLang supports importing Node.js built-in modules and installed npm packages.

### Default Import

```lopo
import express from "express";

define app = express();

app.get("/", func(req, res) {
    res.send("Hello from LopoLang!");
});

app.listen(3000, func() {
    show("Server running on port 3000");
});
````

---

### Named Import

```lopo
import { createHash } from "crypto";

func generateHash(text) {
    define hash = createHash("sha256")
        .update(text)
        .digest("hex");

    return hash;
}

show(generateHash("LopoLang"));
```

---

### Namespace Import

```lopo
import * as path from "path";

define filePath = path.join(
    "users",
    "config.json"
);

show(filePath);
```

---

# Web Server Examples

## Basic HTTP Server

```lopo
import http from "http";

define server = createServer(func(req, res) {

    if (req.path == "/") {
        res.send("Welcome to LopoLang Server!");
    }

});

server.listen(3000);
```

---

## Express Server

```lopo
import express from "express";

define app = express();

app.use(express.json());


app.get("/", func(req, res) {

    res.send({
        message: "LopoLang Backend"
    });

});


app.post("/users", func(req, res) {

    define user = req.body;

    res.send({
        created: user
    });

});


app.listen(3000, func() {

    show("API running on port 3000");

});
```

---

# File System Example

```lopo
import * as fs from "fs";
import * as path from "path";


func readConfig(fileName) {

    do {

        define location = path.join(
            ".",
            fileName
        );

        define content = fs.readFileSync(
            location,
            "utf-8"
        );

        return jsonParse(content);


    } track(error) {

        show(error.message);

        return null;

    }

}


define config = readConfig("config.json");

show(config);
```

---

# Template Rendering Example

```lopo
createServer(func(req, res) {

    define user = {
        name: "Dominex"
    };


    render(
        res,
        "index.html",
        {
            username: user.name
        }
    );

});
```

`views/index.html`

```html
<!DOCTYPE html>
<html>

<head>
<title>LopoLang</title>
</head>


<body>

<h1>
Hello {{username}}
</h1>

</body>

</html>
```

---

# Wikipedia API Example

```lopo
import http from "http";


func wikipedia(title) {

    define url =
    "https://en.wikipedia.org/api/rest_v1/page/summary/"
    + urlencode(title);


    define response = httpFetch(url);

    return jsonParse(response);

}


createServer(func(req, res) {

    define article =
        wikipedia("Programming language");


    render(
        res,
        "article.html",
        {
            title: article.title,
            description: article.extract
        }
    );

})
.listen(3000);
```

`views/article.html`

```html
<!DOCTYPE html>
<html>

<head>
<title>{{title}}</title>
</head>


<body>

<h1>
{{title}}
</h1>


<p>
{{description}}
</p>


</body>

</html>
```

---

# Database Model Example

```lopo
define User = defineModel("users", {

    name: "string",
    age: "number",
    email: "string"

});


define account = User.create({

    name: "Alex",
    age: 20,
    email: "alex@example.com"

});


show(account);
```

---

# Async Task Example

```lopo
task downloadData() {

    define result =
        await httpFetch(
            "https://example.com"
        );

    return result;

}


define data = waitfor downloadData();

show(data);
```


This version is suitable as an `EXAMPLES.md` or documentation examples section.
```
