# Basic routing

Basic routing
Routing refers to determining how an application responds to a client request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, and so on).

Each route can have one or more handler functions, which are executed when the route is matched.

Route definition takes the following structure:

```js
app.METHOD(PATH, HANDLER);
```

```js
app.get("/", function (req, res) {
  res.send("Hello World!");
});
```

```js
app.post("/", function (req, res) {
  res.send("Got a POST request");
});
```

```js
app.put("/user", function (req, res) {
  res.send("Got a PUT request at /user");
});
```

```js
app.delete("/user", function (req, res) {
  res.send("Got a DELETE request at /user");
});
```
