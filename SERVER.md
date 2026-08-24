## 1. Minimal Server

### `server.pulsar`

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return "Hello from Pulsar";
});

app.listen(3000);
```

---

## 2. JSON API

### `server.pulsar`

```pulsar
define app = createServer();

app.get("/api/status", (req, res) => {
    return {
        ok: true,
        status: "running"
    };
});

app.listen(3000);
```
---

## 3. HTML Static File

Use `staticDir` when HTML is already complete and does not require server-side data injection.

### Project

```text
project/
    server.pulsar
    public/
        index.html
```

### `server.pulsar`

```pulsar
define app = createServer({
    staticDir: "./public"
});

app.listen(3000);
```

### `public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Pulsar</title>
</head>
<body>
    <h1>Pulsar Server</h1>
    <p>This file is served directly.</p>
</body>
</html>
```
---

# 4. HTML Data Injection

Use `viewsDir` and `res.render(viewPath, data)` when HTML needs values supplied by Pulsar.

The renderer replaces `{{name}}` with the corresponding property from the data object. 

### Project

```text
project/
    server.pulsar
    views/
        index.html
```

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("index.html", {
        title: "Pulsar",
        message: "Hello from the server"
    });
});

app.listen(3000);
```

### `views/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{title}}</title>
</head>
<body>
    <h1>{{title}}</h1>
    <p>{{message}}</p>
</body>
</html>
```

---

# 5. Nested Data Injection

Nested object properties can be referenced with dot notation. 

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/profile", (req, res) => {
    return res.render("profile.html", {
        user: {
            name: "Puma",
            role: "Developer"
        }
    });
});

app.listen(3000);
```

### `views/profile.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Profile</title>
</head>
<body>
    <h1>{{user.name}}</h1>
    <p>{{user.role}}</p>
</body>
</html>
```

---

# 6. Data Retrieval From HTML

A normal HTML form can send data to a Pulsar route.

The server parses `application/x-www-form-urlencoded` request bodies and places the result in `req.body`.

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("form.html", {
        title: "User Form"
    });
});

app.post("/submit", (req, res) => {
    return {
        name: req.body.name,
        email: req.body.email
    };
});

app.listen(3000);
```

### `views/form.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{title}}</title>
</head>
<body>
    <h1>{{title}}</h1>

    <form method="POST" action="/submit">
        <label>
            Name
            <input type="text" name="name">
        </label>

        <label>
            Email
            <input type="email" name="email">
        </label>

        <button type="submit">Submit</button>
    </form>
</body>
</html>
```

---

# 7. HTML Form Data Returned Into Another HTML Page

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("form.html", {});
});

app.post("/submit", (req, res) => {
    return res.render("result.html", {
        name: req.body.name,
        email: req.body.email
    });
});

app.listen(3000);
```

### `views/form.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Form</title>
</head>
<body>
    <form method="POST" action="/submit">
        <input type="text" name="name">
        <input type="email" name="email">
        <button type="submit">Send</button>
    </form>
</body>
</html>
```

### `views/result.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Result</title>
</head>
<body>
    <h1>Submitted Data</h1>
    <p>Name: {{name}}</p>
    <p>Email: {{email}}</p>
</body>
</html>
```

---

# 8. JSON Data From HTML

Use JavaScript in an HTML page to send JSON to a Pulsar POST route.

### `server.pulsar`

```pulsar
define app = createServer();

app.post("/api/users", (req, res) => {
    return {
        received: req.body
    };
});

app.listen(3000);
```

### `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JSON Client</title>
</head>
<body>
    <button id="send">Send Data</button>

    <pre id="output"></pre>

    <script>
        document.getElementById("send").addEventListener("click", async () => {
            const response = await fetch("/api/users", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    name: "Puma",
                    age: 20
                })
            });

            const data = await response.json();

            document.getElementById("output").textContent =
                JSON.stringify(data, null, 2);
        });
    </script>
</body>
</html>
```

The Pulsar server parses `application/json` bodies with `JSON.parse` and exposes the resulting object as `req.body`. 

---

# 9. HTML Retrieves JSON From a Pulsar API

This pattern keeps HTML static while retrieving data from a Pulsar API.

### `server.pulsar`

```pulsar
define app = createServer({
    staticDir: "./public"
});

app.get("/api/message", (req, res) => {
    return {
        message: "Data from Pulsar",
        version: "1.0"
    };
});

app.listen(3000);
```

### `public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>API Client</title>
</head>
<body>
    <h1 id="message"></h1>
    <p id="version"></p>

    <script>
        async function loadData() {
            const response = await fetch("/api/message");
            const data = await response.json();

            document.getElementById("message").textContent =
                data.message;

            document.getElementById("version").textContent =
                data.version;
        }

        loadData();
    </script>
</body>
</html>
```

---

# 10. HTML Sends and Retrieves Data

### `server.pulsar`

```pulsar
define app = createServer();

app.get("/api/data", (req, res) => {
    return {
        message: "Hello from Pulsar"
    };
});

app.post("/api/data", (req, res) => {
    return {
        received: req.body
    };
});

app.listen(3000);
```

### `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Data Client</title>
</head>
<body>
    <button id="load">Load</button>
    <button id="send">Send</button>

    <pre id="output"></pre>

    <script>
        const output = document.getElementById("output");

        document.getElementById("load").onclick = async () => {
            const response = await fetch("/api/data");
            const data = await response.json();

            output.textContent =
                JSON.stringify(data, null, 2);
        };

        document.getElementById("send").onclick = async () => {
            const response = await fetch("/api/data", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    name: "Puma",
                    value: 100
                })
            });

            const data = await response.json();

            output.textContent =
                JSON.stringify(data, null, 2);
        };
    </script>
</body>
</html>
```

---

# 11. Conditional HTML Injection

The template renderer supports `{{if value}}`, `{{else}}`, and `{{/if}}`.

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("account.html", {
        loggedIn: true,
        username: "Puma"
    });
});

app.listen(3000);
```

### `views/account.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Account</title>
</head>
<body>
    {{if loggedIn}}
        <h1>Welcome {{username}}</h1>
    {{else}}
        <h1>Please log in</h1>
    {{/if}}
</body>
</html>
```

---

# 12. Template Inheritance

The renderer supports `extends` and a `body` placeholder. 

### Project

```text
project/
    server.pulsar
    views/
        layout.html
        home.html
```

### `views/layout.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{title}}</title>
</head>
<body>
    <header>
        <h1>Pulsar</h1>
    </header>

    <main>
        {{body}}
    </main>
</body>
</html>
```

### `views/home.html`

```html
{{extends "layout.html"}}

<section>
    <h2>{{heading}}</h2>
    <p>{{message}}</p>
</section>
```

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("home.html", {
        title: "Home",
        heading: "Pulsar Server",
        message: "Rendered through a layout"
    });
});

app.listen(3000);
```

---

# 13. Route Parameters Into HTML

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/users/:id", (req, res) => {
    return res.render("user.html", {
        id: req.params.id
    });
});

app.listen(3000);
```

### `views/user.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>User</title>
</head>
<body>
    <h1>User</h1>
    <p>ID: {{id}}</p>
</body>
</html>
```

Route parameters are populated from path segments such as `/users/123`. 

---

# 14. Query Parameters Into HTML

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/search", (req, res) => {
    return res.render("search.html", {
        query: req.query.q,
        page: req.query.page
    });
});

app.listen(3000);
```

### `views/search.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Search</title>
</head>
<body>
    <h1>Search</h1>
    <p>Query: {{query}}</p>
    <p>Page: {{page}}</p>
</body>
</html>
```

---

# 15. Session Data Into HTML

The request object exposes `req.session`. The built-in server keeps the session store in memory. 

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    if req.session.visits == null {
        req.session.visits = 0;
    }

    req.session.visits++;

    return res.render("session.html", {
        visits: req.session.visits
    });
});

app.listen(3000);
```

### `views/session.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Session</title>
</head>
<body>
    <h1>Session</h1>
    <p>Visits: {{visits}}</p>
</body>
</html>
```

---

# 16. Cookie Data Into HTML

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/set-name", (req, res) => {
    res.setCookie("name", "Puma", {
        httpOnly: true,
        path: "/"
    });

    return "Cookie set";
});

app.get("/profile", (req, res) => {
    return res.render("profile.html", {
        name: req.cookies.name
    });
});

app.listen(3000);
```

### `views/profile.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Profile</title>
</head>
<body>
    <h1>{{name}}</h1>
</body>
</html>
```

The response object supports `setCookie` and `clearCookie`, while cookies are exposed through `req.cookies`.

---

# 17. API + HTML Dashboard

### `server.pulsar`

```pulsar
define app = createServer({
    staticDir: "./public"
});

app.get("/api/stats", (req, res) => {
    return {
        users: 120,
        posts: 450,
        online: 18
    };
});

app.listen(3000);
```

### `public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dashboard</title>
</head>
<body>
    <h1>Dashboard</h1>

    <p>Users: <span id="users"></span></p>
    <p>Posts: <span id="posts"></span></p>
    <p>Online: <span id="online"></span></p>

    <script>
        async function loadStats() {
            const response = await fetch("/api/stats");
            const data = await response.json();

            document.getElementById("users").textContent = data.users;
            document.getElementById("posts").textContent = data.posts;
            document.getElementById("online").textContent = data.online;
        }

        loadStats();
    </script>
</body>
</html>
```

---

# 18. HTML Form With JSON API

### `server.pulsar`

```pulsar
define app = createServer();

app.post("/api/message", (req, res) => {
    return {
        message: req.body.message
    };
});

app.listen(3000);
```

### `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Message</title>
</head>
<body>
    <input id="message" type="text">
    <button id="send">Send</button>

    <p id="result"></p>

    <script>
        document.getElementById("send").onclick = async () => {
            const message =
                document.getElementById("message").value;

            const response = await fetch("/api/message", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    message: message
                })
            });

            const data = await response.json();

            document.getElementById("result").textContent =
                data.message;
        };
    </script>
</body>
</html>
```

---

# 19. Full Server-Side HTML Example

### Project

```text
project/
    server.pulsar
    views/
        index.html
        result.html
```

### `server.pulsar`

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("index.html", {
        title: "Pulsar Form",
        heading: "Enter your information"
    });
});

app.post("/submit", (req, res) => {
    return res.render("result.html", {
        name: req.body.name,
        email: req.body.email
    });
});

app.listen(3000);
```

### `views/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{title}}</title>
</head>
<body>
    <h1>{{heading}}</h1>

    <form method="POST" action="/submit">
        <input
            type="text"
            name="name"
            placeholder="Name"
            required
        >

        <input
            type="email"
            name="email"
            placeholder="Email"
            required
        >

        <button type="submit">Submit</button>
    </form>
</body>
</html>
```

### `views/result.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Result</title>
</head>
<body>
    <h1>Submitted</h1>

    <p>Name: {{name}}</p>
    <p>Email: {{email}}</p>

    <a href="/">Back</a>
</body>
</html>
```

---

# 20. Complete API + HTML Application

### Project

```text
project/
    server.pulsar
    public/
        index.html
```

### `server.pulsar`

```pulsar
define app = createServer({
    staticDir: "./public"
});

app.get("/api/profile", (req, res) => {
    return {
        user: {
            name: "Puma",
            role: "Developer"
        }
    };
});

app.post("/api/profile", (req, res) => {
    return res.status(201).json({
        saved: true,
        profile: req.body
    });
});

app.listen(3000);
```

### `public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Pulsar Application</title>
</head>
<body>
    <h1>Profile</h1>

    <button id="load">Load Profile</button>

    <input id="name" type="text" placeholder="Name">
    <input id="role" type="text" placeholder="Role">

    <button id="save">Save Profile</button>

    <pre id="output"></pre>

    <script>
        const output = document.getElementById("output");

        document.getElementById("load").onclick = async () => {
            const response = await fetch("/api/profile");
            const data = await response.json();

            output.textContent =
                JSON.stringify(data, null, 2);
        };

        document.getElementById("save").onclick = async () => {
            const response = await fetch("/api/profile", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    name: document.getElementById("name").value,
                    role: document.getElementById("role").value
                })
            });

            const data = await response.json();

            output.textContent =
                JSON.stringify(data, null, 2);
        };
    </script>
</body>
</html>
```

---

# Server API Reference

| Feature | Syntax |
|---|---|
| Create server | `createServer(options)` |
| Middleware | `app.use(fn)` |
| GET | `app.get(path, handler)` |
| POST | `app.post(path, handler)` |
| PUT | `app.put(path, handler)` |
| PATCH | `app.patch(path, handler)` |
| DELETE | `app.delete(path, handler)` |
| OPTIONS | `app.options(path, handler)` |
| Start | `app.listen(port, callback)` |
| Static files | `staticDir` |
| Template directory | `viewsDir` |
| Render HTML | `res.render(path, data)` |
| JSON response | `res.json(data)` |
| HTML/text response | `res.send(data)` |
| Status | `res.status(code)` |
| Route parameters | `req.params` |
| Query parameters | `req.query` |
| Request body | `req.body` |
| Uploaded files | `req.files` |
| Cookies | `req.cookies` |
| Session | `req.session` |
| Request headers | `req.headers` |
| Set cookie | `res.setCookie(...)` |
| Clear cookie | `res.clearCookie(...)` |

The request object is assembled with `path`, `method`, `params`, `query`, `body`, `files`, `cookies`, and `session`.

The response object provides status, JSON, text/HTML, cookie, and template-rendering operations. 

---

# Template Syntax Reference

## Simple value

```html
<h1>{{title}}</h1>
```

## Nested value

```html
<p>{{user.name}}</p>
```

## Conditional

```html
{{if loggedIn}}
    <p>Logged in</p>
{{else}}
    <p>Logged out</p>
{{/if}}
```

## Layout inheritance

```html
{{extends "layout.html"}}

<h1>{{title}}</h1>
```

## Layout body

```html
<main>
    {{body}}
</main>
```

These forms are implemented by the supplied template renderer. 

---

# Data Flow Patterns

## Server-side injection

```text
Pulsar data
    |
    v
res.render("page.html", data)
    |
    v
HTML template
    |
    v
Browser
```

## Browser to server

```text
HTML form / fetch()
    |
    v
HTTP request
    |
    v
Pulsar route
    |
    v
req.body / req.query / req.params
```

## Server API to browser

```text
Pulsar route
    |
    v
JSON response
    |
    v
HTML fetch()
    |
    v
DOM update
```

## Static HTML

```text
Browser
    |
    v
GET /
    |
    v
staticDir
    |
    v
index.html
```

---

# Notes

1. `staticDir` is for files that are served as files; `viewsDir` with `res.render(...)` is for server-side template rendering. 

2. `req.body` is populated according to the request `Content-Type`. JSON requests become objects, URL-encoded forms become objects, and other bodies remain text. 

3. Template values are converted to strings. Missing or null values render as an empty string.

4. The template system shown here is not a general JavaScript template engine. Use the syntax implemented by the interpreter: values, nested properties, conditionals, and inheritance. 

5. The examples intentionally contain no decorative symbols, emojis, stickers, or non-code UI elements. They are written as clean language/server documentation examples.
