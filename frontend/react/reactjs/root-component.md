# Criando o component raiz

### App.js

```js
import React from "react";

function App() {
  return <h1>Helloooo</h1>;
}

export default App;
```

### index.js

```js
import React from "react";
import { render } from "react-dom";
import App from "./App";

render(<App />, document.getElementById("app"));
```

## Importando CSS

yarn add style-loader css-loader -D

- No `webpack.config.js`

```js
const { resolve } = require("path");

module.exports = {
  entry: resolve(__dirname, "src", "index.js"),
  output: {
    path: resolve(__dirname, "public"),
    filename: "bundle.js",
  },
  devServer: {
    contentBase: resolve(__dirname, "public"),
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
      {
        test: /\.css/,
        use: [{ loader: "style-loader" }, { loader: "css-loader" }],
      },
    ],
  },
};
```

## Importando Imagens

yarn add file-loader -D

- Adicionar uma nova rule no `webpack.config`

```js
{
  test: /.*\.(gif|png|jpe?g)$/i,
  use: {
    loader: 'file-loader'
  }
}
```

## Plugins

Possibilita criar states fora do constructor da class

```js
state = {
  techs: ["Node.js", "ReactJS", "React native"],
};
```

adicionar o

```bash
yarn add @babel/plugin-proposal-class-properties -D
```

e no babel config

```js
module.exports = {
  presets: ["@babel/preset-env", "@babel/preset-react"],
  plugins: ["@babel/plugin-proposal-class-properties"],
};
```
