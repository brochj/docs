# Controllers


## Criando um Model

### Controller de usuário

#### Criação de usuário

- Para implementar a feature de criação de usuário. Dentro da pasta `app/controllers/` criar um arquivo com nome `UserController.js`. Adicionar o código:

```js
  import User from '../models/User';

  class UserController {
    async store(req, res) {
      // Verificando se ja existe usuário com email cadastrado
      const userExists = await User.findOne({ where: { email: req.body.email } });

      if (userExists) {
        return res.status(400).json({ error: 'User already exists.' });
      }

      // Salvando usuario no banco de dados
      const { id, name, email, provider } = await User.create(req.body);

      return res.json({ id, name, email, provider });
    }
  }
  export default new UserController();
```

- Dentro do arquivo `routes.js` importar o `UserController` e criar uma rota POST

```js
  import { Router } from 'express';

  import UserController from './app/controllers/UserController';

  const routes = new Router();

  routes.post('/users', UserController.store);

  export default routes;
```