# Estrutura inicial

## Pasta raiz

- Dentro da pasta raiz iniciar o `yarn`.

```bash
yarn init -y
```

## Pastas e arquivos iniciais

- Dentro da pasta raiz

```
projeto
      ├── package.json
      ├── src
      │   ├── app.js
      │   ├── routes.js
      │   └── server.js
      └── yarn.lock
```

### app.js

```js
import express from "express";
import routes from "./routes";

class App {
  constructor() {
    this.server = express();
    this.middlewares();
    this.routes();
  }

  middlewares() {
    this.server.use(express.json());
  }

  routes() {
    this.server.use(routes);
  }
}

export default new App().server;
```

### server.js

```js
import app from "./app";

app.listen(3333);
```

### routes.js

```js
import { Router } from "express";

const routes = new Router();

routes.get("/", (req, res) => {
  return res.json({ msg: "hello World" });
});

export default routes;
```

## Iniciar o GIT

- Iniciar o GIT com `git init` e criar o arquivo `.gitignore` com `node_modules/`
  dentro.

## Adicionar o Express

```bash
yarn add express
```

## Nodemon & Sucrase

```bash
yarn add sucrase nodemon -D
# OR
yarn add sucrase nodemon --dev
```

- package.json

```json
"scripts": {
    "dev": "nodemon src/server.js"
  },
```

- Na raiz do projeto criar um arquivo `nodemon.json` e adicionar:

```json
{
  "execMap": {
    "js": "sucrase-node"
  }
}
```

## Rodar `yarn dev`

- Em `http://localhost:3333` deve aparecer o **Hello world**.

## ESLint & Prettier

### ESLint

- Instalar o ESLint com dependência de desenvolvimento.

```bash
yarn add eslint -D
yarn add eslint --dev
```

- Iniciar o ESLint no projeto

```bash
yarn eslint --init
```

- Configurar dessa maneira

```bash
  ? How would you like to use ESLint?
  To check syntax, find problems, and enforce code style

  ? What type of modules does your project use?
  JavaScript modules (import/export)

  ? Which framework does your project use?
  None of these

  ? Where does your code run?
  Node

  ? How would you like to define a style for your project?
  Use a popular style guide

  ? Which style guide do you want to follow?
  Airbnb (https://github.com/airbnb/javascript)

  ? What format do you want your config file to be in?
  JavaScript

  ? Would you like to install them now with npm?
  Yes
```

- Como a instalação é feita pelo `npm`, apagar o arquivo package-lock.json e rodar
  os comando `yarn` para refazer a instalação utilizando o Yarn.

- Instalar a extensão `ESLint` no VSCode

- Nas settings do VSCode (JSON) adicionar:

```json
  "eslint.autoFixOnSave": true,
  "eslint.validate": [
      {
          "language": "javascript",
          "autoFix": true
      },
      {
          "language": "javascriptreact",
          "autoFix": true
      },
      {
          "language": "typescript",
          "autoFix": true
      },
      {
          "language": "typescriptreact",
          "autoFix": true
      }

  ],
```

- Dentro do arquivo `.eslintrc.js` deixar da seguinte forma:

```js
module.exports = {
  env: {
    es6: true,
    node: true,
  },
  extends: ["airbnb-base", "prettier"],
  plugins: ["prettier"],
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly",
  },
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: "module",
  },
  rules: {
    "prettier/prettier": "error",
    "class-methods-use-this": "off",
    "no-param-reassign": "off",
    camelcase: "off",
    "no-unused-vars": ["error", { argsIgnorePattern: "next" }],
  },
};
```

### Prettier

- Instalar o Prettier como dependência de desenvolvimento

```bash
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

- Criar um arquivo `.prettierrc` na raiz e adicionar

```json
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

- Após isso, o ESLint e Prettier já devem estar funcionando, caso não esteja, dar
  um `reload window` no `VSCode`.

### EditorConfig

- Instalar a extensão do VSCode `EditorConfig for VS Code`
- No VSCodr, ir na raiz do projeto clicar com o botão direito em selecionar
  `Generate .editorconfig`
- Dentro de `.editorconfig` deixar da seguinte maneira

```
  root = true

  [*]
  indent_style = space
  indent_size = 2
  charset = utf-8
  trim_trailing_whitespace = true
  insert_final_newline = true
```

### Dica ESLint

- Para arrumar todos os arquivos de uma vez, rodar o comando:

```bash
yarn eslint --fix src --ext .js
```
