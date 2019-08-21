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
import express from 'express';
import routes from './routes';

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
import app from './app';

app.listen(3333);
```

### routes.js
```js
import { Router } from 'express';

const routes = new Router();

routes.get('/', (req, res) => {
  return res.json({msg: 'hello World'});
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
```

package.json
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