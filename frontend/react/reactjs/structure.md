

yarn init -y

yarn add @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli -D

yarn add react react-dom

yarn add babel-loader -D

## Configurando Babel
- criar na raiz um `babel.config.js`

```js
module.exports = {
  presets: [
    "@babel/preset-env",
    "@babel/preset-react"
  ],
}
```

## Configurando WebPack
- criar na raiz um `webpack.config.js`

```js
const { resolve } = require('path');

module.exports = {
  entry: resolve(__dirname, 'src', 'index.js'),
  output: {
    path: resolve(__dirname, 'public'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader'
        }
      }
    ]
  }
}
```

### Package.json

```json
"scripts": {
    "build": "webpack --mode production"
  },

```

## Estrutura

```
├── babel.config.js
├── package.json
├── public
│   └── index.html
├── src
│   └── index.js
├── webpack.config.js
└── yarn.lock
```

### index.html
- importar o bundle dentro do html
- Colocar um div com id app, dentro dessa div que será renderizado toda a aplicação

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>ReactJS</title>
</head>
<body>
  <div id="app"></div>

  <script src="./bundle.js"></script>
</body>
</html>
```


## Monitorar alterações

yarn add webpack-dev-server -D

- abaixo de output em `webpack.config.js` adicionar
```js
output: {
  ...
}
devServer: {
    contentBase: resolve(__dirname, 'public')
  },
```

- Package.json

```json
"scripts": {
    "build": "webpack --mode production",
    "dev": "webpack-dev-server --mode development"
  },
```

- Modo `production` gera um bundle mais otimizado e de uma unica linha.