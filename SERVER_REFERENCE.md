# 1. Creating a Server

The server is created with:

```pulsar
define app = createServer();
```

A minimal server:

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return "Hello from Pulsar";
});

app.listen(3000);
```

The server listens on port `3000`. 

---

# 2. Server Options

`createServer()` accepts an options object.

For static files:

```pulsar
define app = createServer({
    staticDir: "./public"
});
```

For HTML templates:

```pulsar
define app = createServer({
    viewsDir: "./views"
});
```

The two options have different purposes:

* `staticDir` serves completed files directly.
* `viewsDir` identifies the directory containing HTML templates used by `res.render()`. 

---

# 3. Starting the Server

Use:

```pulsar
app.listen(3000);
```

A callback can also be supplied:

```pulsar
app.listen(3000, () => {
    show("Server started");
});
```

The server API defines `app.listen(port, callback)`. 

---

# 4. GET Routes

Register a GET route with:

```pulsar
app.get(path, handler);
```

Example:

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return "Hello from Pulsar";
});

app.listen(3000);
```

The handler receives:

```text
req
res
```

as its parameters. 

---

# 5. POST Routes

Register a POST route with:

```pulsar
app.post(path, handler);
```

Example:

```pulsar
define app = createServer();

app.post("/submit", (req, res) => {
    return {
        received: req.body
    };
});

app.listen(3000);
```

---

# 6. PUT Routes

The server supports:

```pulsar
app.put("/users/:id", (req, res) => {
    return {
        id: req.params.id,
        data: req.body
    };
});
```

---

# 7. PATCH Routes

The server supports:

```pulsar
app.patch("/users/:id", (req, res) => {
    return {
        id: req.params.id,
        data: req.body
    };
});
```

---

# 8. DELETE Routes

The server supports:

```pulsar
app.delete("/users/:id", (req, res) => {
    return {
        deleted: req.params.id
    };
});
```

---

# 9. OPTIONS Routes

The server supports:

```pulsar
app.options("/", (req, res) => {
    return {
        allowed: true
    };
});
```

The supported route registration methods are:

```text
app.get()
app.post()
app.put()
app.patch()
app.delete()
app.options()
```



---

# 10. Returning Text

A route can return a string directly:

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return "Hello from Pulsar";
});

app.listen(3000);
```

---

# 11. Returning JSON

Returning an object produces a JSON response:

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

The response object also provides `res.json(...)`. 

---

# 12. `res.json()`

JSON can explicitly be returned with:

```pulsar
define app = createServer();

app.get("/api/user", (req, res) => {
    return res.json({
        name: "Puma",
        role: "Developer"
    });
});

app.listen(3000);
```

The response API includes:

```pulsar
res.json(data)
```



---

# 13. `res.send()`

Text or HTML can be sent explicitly:

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return res.send("<h1>Hello from Pulsar</h1>");
});

app.listen(3000);
```

The server exposes:

```pulsar
res.send(data)
```

for HTML/text responses. 

---

# 14. HTTP Status Codes

Use:

```pulsar
res.status(code)
```

Example:

```pulsar
define app = createServer();

app.post("/users", (req, res) => {
    return res.status(201).json({
        created: true
    });
});

app.listen(3000);
```

The response API provides `res.status(code)`. 

---

# 15. Route Parameters

Routes can contain named parameters.

```pulsar
define app = createServer();

app.get("/users/:id", (req, res) => {
    return {
        id: req.params.id
    };
});

app.listen(3000);
```

A request such as:

```text
/users/123
```

provides:

```pulsar
req.params.id
```

with the corresponding route value. 

---

# 16. Query Parameters

Query parameters are available through:

```pulsar
req.query
```

Example:

```pulsar
define app = createServer();

app.get("/search", (req, res) => {
    return {
        query: req.query.q,
        page: req.query.page
    };
});

app.listen(3000);
```

For:

```text
/search?q=pulsar&page=2
```

the route can access:

```pulsar
req.query.q
req.query.page
```



---

# 17. Request Body

Request data is available through:

```pulsar
req.body
```

For example:

```pulsar
define app = createServer();

app.post("/users", (req, res) => {
    return {
        received: req.body
    };
});

app.listen(3000);
```

The server parses request bodies according to their `Content-Type`. JSON and URL-encoded forms become objects, while other bodies remain text. 

---

# 18. URL-Encoded HTML Forms

An ordinary HTML form can send data to Pulsar:

```html
<form method="POST" action="/submit">
    <input type="text" name="name">
    <input type="email" name="email">

    <button type="submit">Submit</button>
</form>
```

The Pulsar route receives the values through:

```pulsar
app.post("/submit", (req, res) => {
    return {
        name: req.body.name,
        email: req.body.email
    };
});
```

The built-in server parses `application/x-www-form-urlencoded` request bodies into `req.body`. 

---

# 19. JSON Request Bodies

An HTML page can send JSON:

```html
<script>
    async function sendData() {
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

        console.log(data);
    }

    sendData();
</script>
```

Pulsar receives it as:

```pulsar
app.post("/api/users", (req, res) => {
    return {
        received: req.body
    };
});
```

JSON request bodies are parsed and exposed as `req.body`. 

---

# 20. Request Headers

Request headers are available through:

```pulsar
req.headers
```

Example:

```pulsar
define app = createServer();

app.get("/headers", (req, res) => {
    return {
        headers: req.headers
    };
});

app.listen(3000);
```

The request object exposes headers as part of the request data. 

---

# 21. Static Files

Use `staticDir` to serve completed files.

Project:

```text
project/
    server.pulsar
    public/
        index.html
```

`server.pulsar`:

```pulsar
define app = createServer({
    staticDir: "./public"
});

app.listen(3000);
```

`public/index.html`:

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

The built-in server checks `staticDir` for GET requests and serves recognized file types. HTML is served as `text/html`. 

---

# 22. Static HTML and JavaScript

Static HTML can retrieve data from a Pulsar API.

`server.pulsar`:

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

`public/index.html`:

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

This creates the flow:

```text
Browser
    |
    | GET /api/message
    v
Pulsar route
    |
    | JSON
    v
Browser JavaScript
    |
    v
DOM
```



---

# 23. Server-Side HTML Rendering

Use:

```pulsar
viewsDir
```

with:

```pulsar
res.render()
```

Example:

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

`views/index.html`:

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

The renderer replaces template values such as `{{title}}` with values supplied to `res.render()`. 

---

# 24. `res.render()`

The basic syntax is:

```pulsar
res.render(
    "template.html",
    data
);
```

Example:

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("home.html", {
        title: "Home",
        message: "Welcome"
    });
});

app.listen(3000);
```

---

# 25. Simple Template Values

HTML:

```html
<h1>{{title}}</h1>

<p>{{message}}</p>
```

Pulsar:

```pulsar
return res.render("index.html", {
    title: "Pulsar",
    message: "Hello"
});
```

The template system converts template values to strings. Missing or null values render as an empty string. 

---

# 26. Nested Template Values

Data:

```pulsar
return res.render("profile.html", {
    user: {
        name: "Puma",
        role: "Developer"
    }
});
```

HTML:

```html
<h1>{{user.name}}</h1>
<p>{{user.role}}</p>
```

Nested properties use dot notation. 

---

# 27. Conditional Templates

The renderer supports:

```text
{{if value}}
{{else}}
{{/if}}
```

Example:

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

`account.html`:

```html
{{if loggedIn}}
    <h1>Welcome {{username}}</h1>
{{else}}
    <h1>Please log in</h1>
{{/if}}
```



---

# 28. Template Inheritance

A layout can contain:

```html
{{body}}
```

A child template can use:

```html
{{extends "layout.html"}}
```

`layout.html`:

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

`home.html`:

```html
{{extends "layout.html"}}

<section>
    <h2>{{heading}}</h2>
    <p>{{message}}</p>
</section>
```

The supplied renderer supports this inheritance model. 

---

# 29. Route Parameters Into Templates

`server.pulsar`:

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

`views/user.html`:

```html
<h1>User</h1>

<p>ID: {{id}}</p>
```

A request to:

```text
/users/123
```

provides the route parameter to the template. 

---

# 30. Query Parameters Into Templates

`server.pulsar`:

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

`views/search.html`:

```html
<h1>Search</h1>

<p>Query: {{query}}</p>
<p>Page: {{page}}</p>
```



---

# 31. Sessions

The request object exposes:

```pulsar
req.session
```

The supplied built-in server keeps the session store in memory. 

Example:

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

Template:

```html
<h1>Session</h1>

<p>Visits: {{visits}}</p>
```

---

# 32. Cookies

Set a cookie with:

```pulsar
res.setCookie(...)
```

Example:

```pulsar
define app = createServer();

app.get("/set-name", (req, res) => {
    res.setCookie("name", "Puma", {
        httpOnly: true,
        path: "/"
    });

    return "Cookie set";
});

app.listen(3000);
```

Read it through:

```pulsar
req.cookies.name
```



---

# 33. Rendering Cookie Data

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/profile", (req, res) => {
    return res.render("profile.html", {
        name: req.cookies.name
    });
});

app.listen(3000);
```

`profile.html`:

```html
<h1>{{name}}</h1>
```

---

# 34. Clearing Cookies

The response API provides:

```pulsar
res.clearCookie(...)
```

The server also exposes cookies through:

```pulsar
req.cookies
```



---

# 35. Middleware

Middleware is registered with:

```pulsar
app.use(fn);
```

Basic structure:

```pulsar
define app = createServer();

app.use((req, res, next) => {
    show(req.method);
    next();
});

app.get("/", (req, res) => {
    return "Hello";
});

app.listen(3000);
```

The server API exposes `app.use(fn)` as its middleware registration mechanism. 

---

# 36. API Dashboard

A static HTML dashboard can consume a Pulsar API.

`server.pulsar`:

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

`public/index.html`:

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

# 37. HTML Form With JSON API

`server.pulsar`:

```pulsar
define app = createServer();

app.post("/api/message", (req, res) => {
    return {
        message: req.body.message
    };
});

app.listen(3000);
```

`index.html`:

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

# 38. Full Server-Side Form

Project:

```text
project/
    server.pulsar
    views/
        index.html
        result.html
```

`server.pulsar`:

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

`views/index.html`:

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

`views/result.html`:

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

# 39. Complete API and HTML Application

Project:

```text
project/
    server.pulsar
    public/
        index.html
```

`server.pulsar`:

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

`public/index.html`:

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
        const output =
            document.getElementById("output");

        document.getElementById("load").onclick =
            async () => {
                const response =
                    await fetch("/api/profile");

                const data =
                    await response.json();

                output.textContent =
                    JSON.stringify(data, null, 2);
            };

        document.getElementById("save").onclick =
            async () => {
                const response =
                    await fetch("/api/profile", {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json"
                        },
                        body: JSON.stringify({
                            name:
                                document.getElementById("name").value,
                            role:
                                document.getElementById("role").value
                        })
                    });

                const data =
                    await response.json();

                output.textContent =
                    JSON.stringify(data, null, 2);
            };
    </script>
</body>
</html>
```

This demonstrates both directions of application data flow:

```text
Pulsar server
    |
    | JSON
    v
HTML browser

HTML browser
    |
    | JSON POST
    v
Pulsar server
```

The complete API + HTML pattern is part of the existing server examples.  

---

# 40. Server API Reference

| Feature            | Syntax                       |
| ------------------ | ---------------------------- |
| Create server      | `createServer(options)`      |
| Middleware         | `app.use(fn)`                |
| GET                | `app.get(path, handler)`     |
| POST               | `app.post(path, handler)`    |
| PUT                | `app.put(path, handler)`     |
| PATCH              | `app.patch(path, handler)`   |
| DELETE             | `app.delete(path, handler)`  |
| OPTIONS            | `app.options(path, handler)` |
| Start              | `app.listen(port, callback)` |
| Static files       | `staticDir`                  |
| Template directory | `viewsDir`                   |
| Render HTML        | `res.render(path, data)`     |
| JSON response      | `res.json(data)`             |
| HTML/text response | `res.send(data)`             |
| Status             | `res.status(code)`           |
| Route parameters   | `req.params`                 |
| Query parameters   | `req.query`                  |
| Request body       | `req.body`                   |
| Uploaded files     | `req.files`                  |
| Cookies            | `req.cookies`                |
| Session            | `req.session`                |
| Request headers    | `req.headers`                |
| Set cookie         | `res.setCookie(...)`         |
| Clear cookie       | `res.clearCookie(...)`       |



---

# 41. Request Object

The request object contains:

```text
req.path
req.method
req.params
req.query
req.body
req.files
req.cookies
req.session
req.headers
```

The supplied server assembles these values into the request object. 

---

# 42. Response Object

The response object provides:

```text
res.status()
res.json()
res.send()
res.render()
res.setCookie()
res.clearCookie()
```

These operations cover status codes, JSON, text/HTML, templates, and cookies. 

---

# 43. Template Syntax Reference

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

# 44. Server-Side Data Injection

The basic data injection flow is:

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

For example:

```pulsar
define user = {
    name: "Puma",
    role: "Developer"
};

app.get("/", (req, res) => {
    return res.render("index.html", {
        user: user
    });
});
```

HTML:

```html
<h1>{{user.name}}</h1>
<p>{{user.role}}</p>
```



---

# 45. Browser-to-Server Data Flow

HTML forms and browser JavaScript can send HTTP requests:

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



---

# 46. Server-to-Browser API Flow

A Pulsar API can return JSON:

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



---

# 47. Static HTML Flow

For static files:

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

# 48. Static Files vs Templates

Use static files when the HTML is already complete:

```pulsar
define app = createServer({
    staticDir: "./public"
});
```

Use templates when Pulsar must inject server-side data:

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("index.html", {
        title: "Pulsar"
    });
});
```

`staticDir` and `viewsDir` therefore represent two different server-side HTML workflows. 

---

# 49. HTTP Client Helper

The evaluator also contains an `httpFetch` builtin.

Its basic form is:

```pulsar
define response = await httpFetch(
    "https://example.com"
);

show(response);
```

The builtin accepts a URL and optional options object. The implementation supports HTTP methods, headers, request bodies, and returns an object containing:

```text
status
headers
body
```



---

# 50. HTTP POST Client Example

```pulsar
define response = await httpFetch(
    "https://example.com/api/data",
    {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: {
            name: "Puma",
            value: 100
        }
    }
);

show(response.status);
show(response.body);
```

When the body is an object, the implementation serializes it as JSON and supplies an appropriate content type when one is not already specified. 

---

# 51. Server Architecture

The built-in server can be viewed as several layers:

```text
                    Pulsar Server
                         |
          +--------------+--------------+
          |              |              |
       Routing       Middleware      Static Files
          |
          v
       Request
          |
    +-----+-----+
    |     |     |
 params query  body
    |
    v
  Handler
    |
    +-------------------+
    |         |         |
  JSON      HTML      Template
 response  response   rendering
```

The supplied implementation provides route registration, request parsing, response handling, static serving, templates, cookies, and sessions. 

---

# 52. AI Rules for Pulsar Server Code

When generating Pulsar server programs:

1. Use `createServer()` for the server.
2. Register routes through `app.get()`, `app.post()`, `app.put()`, `app.patch()`, `app.delete()`, or `app.options()`.
3. Use `req.params` for route parameters.
4. Use `req.query` for query parameters.
5. Use `req.body` for request data.
6. Use `req.headers` for headers.
7. Use `req.cookies` for cookies.
8. Use `req.session` for session data.
9. Use `staticDir` for static files.
10. Use `viewsDir` with `res.render()` for server-side HTML templates.
11. Use the implemented template syntax rather than assuming a general-purpose template language.
12. Use `res.json()`, `res.send()`, `res.status()`, and `res.render()` according to the response needed.
13. Use the actual server API rather than inventing unsupported methods.

The API surface above is the one established by the supplied server implementation and existing server documentation. 

---

# 53. Important Runtime Rules

`req.body` depends on the request content type:

```text
application/json
        |
        v
object

application/x-www-form-urlencoded
        |
        v
object

other body
        |
        v
text
```



Template values are converted to strings. Missing or null values render as an empty string. 

The template system is not a general JavaScript template engine. Its documented syntax is based on values, nested properties, conditionals, and template inheritance. 

---

# 54. Minimal Complete API

```pulsar
define app = createServer();

app.get("/", (req, res) => {
    return {
        name: "Pulsar",
        status: "running"
    };
});

app.listen(3000);
```

---

# 55. Minimal Complete Static Website

Project:

```text
project/
    server.pulsar
    public/
        index.html
```

`server.pulsar`:

```pulsar
define app = createServer({
    staticDir: "./public"
});

app.listen(3000);
```

`public/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Pulsar</title>
</head>
<body>
    <h1>Pulsar</h1>
</body>
</html>
```

---

# 56. Minimal Complete Dynamic Website

Project:

```text
project/
    server.pulsar
    views/
        index.html
```

`server.pulsar`:

```pulsar
define app = createServer({
    viewsDir: "./views"
});

app.get("/", (req, res) => {
    return res.render("index.html", {
        title: "Pulsar",
        message: "Dynamic server-side data"
    });
});

app.listen(3000);
```

`views/index.html`:

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

# 57. Minimal Complete HTML API Application

`server.pulsar`:

```pulsar
define app = createServer({
    staticDir: "./public"
});

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

`public/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Pulsar API</title>
</head>
<body>
    <button id="load">Load</button>
    <button id="send">Send</button>

    <pre id="output"></pre>

    <script>
        const output =
            document.getElementById("output");

        document.getElementById("load").onclick =
            async () => {
                const response =
                    await fetch("/api/data");

                const data =
                    await response.json();

                output.textContent =
                    JSON.stringify(data, null, 2);
            };

        document.getElementById("send").onclick =
            async () => {
                const response =
                    await fetch("/api/data", {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json"
                        },
                        body: JSON.stringify({
                            name: "Puma",
                            value: 100
                        })
                    });

                const data =
                    await response.json();

                output.textContent =
                    JSON.stringify(data, null, 2);
            };
    </script>
</body>
</html>
```

This represents the core browser-to-Pulsar and Pulsar-to-browser data cycle documented by the existing server implementation. 

---

# 58. Reference Summary

The built-in Pulsar server is centered around:

```text
createServer()
    |
    +-- app.use()
    |
    +-- app.get()
    +-- app.post()
    +-- app.put()
    +-- app.patch()
    +-- app.delete()
    +-- app.options()
    |
    +-- app.listen()
```

Requests provide:

```text
req.path
req.method
req.params
req.query
req.body
req.files
req.cookies
req.session
req.headers
```

Responses provide:

```text
res.status()
res.json()
res.send()
res.render()
res.setCookie()
res.clearCookie()
```

HTML can be delivered through:

```text
staticDir
```

or rendered dynamically through:

```text
viewsDir
res.render()
```

The main application data flows are:

```text
Pulsar -> HTML
HTML -> Pulsar
Pulsar -> JSON -> HTML
HTML -> JSON -> Pulsar
```