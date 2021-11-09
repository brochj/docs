# Serving static files in Express

To serve static files such as `images`, `CSS files`, and `JavaScript files`, use the `express.static` built-in middleware function in Express.

The function signature is:

```js
express.static(root, [options]);
```

For example, use the following code to serve images, CSS files, and JavaScript files in a directory named **public**:

```js
app.use(express.static("public"));
```

Now, you can load the files that are in the public directory:

```sh
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

To create a virtual path prefix (where the path does not actually exist in the file system) for files that are served by the express.static function, specify a mount path for the static directory, as shown below:

```js
app.use("/static", express.static("public"));
```

```sh
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

However, the path that you provide to the express.static function is relative to the directory from where you launch your node process. If you run the express app from another directory, it’s safer to use the absolute path of the directory that you want to serve:

```js
const path = require("path");
app.use("/static", express.static(path.join(__dirname, "public")));
```
