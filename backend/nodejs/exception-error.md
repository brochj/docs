# Tratamento de excecoes

Exemplo de ferramentas

- Sentry
- Bugsnag

## Utilizando o sentry

- ir no [site](https://sentry.io/) do sentry e criar um novo projeto.

```bash
yarn add @sentry/node@5.6.2
```

- Por padrão o express não detecta erros assícronos

```bash
yarn add express-async-errors
```

## Youch

- Para formatar as msgs de erro. Ele transforma o msg de erro em Json ou Html.

```bash
yarn add youch
```

- Exemplo:

```json
{
  "error": {
    "message": "_Meetup2.default.finddAll is not a function",
    "name": "TypeError",
    "frames": [
      {
        "file": "src/app/controllers/MeetupController.js",
        "filePath": "/home/broch/projects/meetapp-backend/src/app/controllers/MeetupController.js",
        "method": "index",
        "line": 20,
        "column": 44,
        "context": {
          ...
        },
        "isModule": false,
        "isNative": false,
        "isApp": true
      },
      ...
      ...
```

## Configurando o sentry

- criar uma `config/sentry.js` e adicionar o dsn fornecido no projeto do sentry.

```js
export default {
  dsn: "https://ab849cb558af4b36a3e608e37db41cd2@sentry.io/1545899",
};
```

- No `app.js`

> OBS: `import 'express-async-errors';` TEM que ser importados antes das rotas!!.

```js
import express from "express";
import "express-async-errors";
import Youch from "youch";
import * as Sentry from "@sentry/node";

import sentryConfig from "./config/sentry";
import routes from "./routes";

import "./database";

class App {
  constructor() {
    this.server = express();

    Sentry.init(sentryConfig);

    this.middlewares();
    this.routes();
    this.exceptionhandler();
  }

  middlewares() {
    // The request handler must be the first middleware on the app
    this.server.use(Sentry.Handlers.requestHandler());
    this.server.use(express.json());
  }

  routes() {
    this.server.use(routes);
    // The error handler must be before any other error middleware and after all controllers
    this.server.use(Sentry.Handlers.errorHandler());
  }

  // Qndo o express recebe um middleware de 4 parametro ele sabe que é um midd de excecao
  exceptionhandler() {
    this.server.use(async (err, req, res, next) => {
      const errors = await new Youch(err, req).toJSON();
      return res.status(500).json(errors);
    });
  }
}

export default new App().server;
```
