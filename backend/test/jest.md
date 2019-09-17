# Testes automatizados

Adicionar o framework jest. Desenvolvido pelo Facebook, o jest funciona no nodeJS, reactJS e React-native.

```js
yarn add jest -D
```

```js
yarn jest --init
```
## Configurando

```bash
✔ Would you like to use Jest when running "test" script in "package.json"? … yes
✔ Choose the test environment that will be used for testing › node
✔ Do you want Jest to add coverage reports? … yes
✔ Automatically clear mock calls and instances between every test? … yes
```
## jest.config.js
- Antes de modificar, criar uma pasta `__tests__` na raiz do projeto.

```js
  bail: 1, //1 = Qndo ocorre um falha ele para os testes, 0 = Continua até o final
  clearMocks: true,
  collectCoverage: true,
  collectCoverageFrom: ['src/app/**/*.js'], // **= todos os subníveis
  coverageDirectory: '__tests__/coverage',
  coverageReporters: ['text', 'lcov'],
  testEnvironment: 'node',
  testMatch: ['**/__tests__/**/*.test.js'],
```

## jest e sucrase
Por padrão o jest utiliza o formato antigo do javascript, (require, module.exports, ...). Para arrumar isso vamos instalar o plugin jest para o sucrase.

```bash
yarn add --dev @sucrase/jest-plugin
```

- No `jest.config.js`  mudar o `transform: null` para

```js
transform: {
    '.(js|jsx|ts|tsx)': '@sucrase/jest-plugin',
  },
```

## Nodemon.json
- Deixar de monitorar a pasta dos testes. Ou seja, quando tiver alguma alteração dentro da pasta `__tests__` nodemon **NÃO** vai restartar o servidor.

```json
{
  "execMap": {
    "js": "sucrase-node"
  },
  "ignore": [
    "__tests__"
  ]
}
```

# Primeiro teste
- Adicionar a lib para ter o intellisense do jest.

```bash
yarn add -D @types/jest
```

- Dentro da pasta `__tests__` criar um arquivo `example.test.js`

```js
function soma(a, b) {
  return a + b;
}

test('if I call soma functio with 4 and 5 it should return 9', () => {
  const result = soma(4, 5);

  expect(result).toBe(9);
});
```

- Rodar o teste com `yarn test`.
- Resultado

```bash
❯ yarn test
yarn run v1.17.3
$ jest
 PASS  __tests__/example.test.js
  ✓ if I call soma function with 4 and 5 it should return 9 (7ms)

----------|----------|----------|----------|----------|-------------------|
| File       | % Stmts    | % Branch   | % Funcs    | % Lines    | Uncovered Line #s   |
| ---------- | ---------- | ---------- | ---------- | ---------- | ------------------- |
| All files  | 0          | 0          | 0          | 0          |                     |
| ---------- | ---------- | ---------- | ---------- | ---------- | ------------------- |
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.05s
Ran all test suites.
Done in 2.37s.
```

# Variáveis ambiente
- Por padrão quando roda-se os teste ele utilizará o banco de dados da aplicação, porém não é interessante que isso ocorra, ou seja os testes devem ocorrer em um banco de dados separado.

- Criar um arquivo na raiz `.env.test` com os dados

```bash
APP_URL=http://localhost:3333
NODE_ENV=development
# Auth
APP_SECRET=templatenoderocketseat
# Database
DB_DIALECT=sqlite
```
- Vamos utilizar o banco sqlite pois com ele não precisará adicionar nenhuma dependência, nem criar um database com o docker.

```bash
yarn add sqlite3 -D
```

## config/database.js
- No arquivo `config/database.js/` adicionar a nova variável ambiente, `storage` e mudar o `import`
- `logging: false` evita ficar mostrando as queries do banco de dados no log do jest.
```js
require('../bootstrap');

module.exports = {
  dialect: process.env.DB_DIALECT || 'postgres',
  host: process.env.DB_HOST,
  username: process.env.DB_USER,
  password: process.env.DB_PASS,
  database: process.env.DB_NAME,
  storage: './__tests__/database.sqlite',
  //logging: false,
  define: {
    timestamps: true,
    underscored: true,
    underscoredAll: true,
  },
};
```

## src/bootstrap.js
- Arquivo que fará a seleção das variáveis ambientes de acordo com a utilização.

```js
const dotenv = require('dotenv');

dotenv.config({
  path: process.env.NODE_ENV === 'test' ? '.env.test' : '.env',
});
```

## app.js
- Mudar a importação do dotenv de
```js
import 'dotenv/config';
...
```

para

```js
import './bootstrap';
...
```

## No Package.json
- Setar o `NODE_ENV` como `test` no script de test
```json
"scripts": {
    "dev": "nodemon src/server.js",
    "build": "sucrase ./src -d ./dist --transforms imports",
    "test": "NODE_ENV=test jest"
  },
```
A partir daqui os testes já devem estar funcionando novamente.

# Tabelas e Migrations

- É interessante que cada vez que os teste forem rodados, executa-se todas as migrations, criando assim, as tabelas zeradas.
- E depois do teste, deve-se desfazer todas as migrations para que não fique resquícios de dados armazenados dos teste anteriores.


- Para isso no `package.json` adicionar os prefixos `pre` e `post`,  que serão comandos executados antes e depois do `yarn test` respectivamente.

```json
"scripts": {
    (...)
    "pretest": "NODE_ENV=test sequelize db:migrate",
    "test": "NODE_ENV=test jest",
    "posttest": "NODE_ENV=test sequelize db:migrate:undo:all"
  },
```

- Com uma migration de criar usuários configurada.
- Rodando o `yarn test` deve aparecer a seguinte mensagem e um arquivo `database.sqlite` deve ser criado dentro de `__tests__`

```bash
❯ yarn test
yarn run v1.17.3
$ NODE_ENV=test sequelize db:migrate

Sequelize CLI [Node: 10.16.2, CLI: 5.5.0, ORM: 5.9.4]

Loaded configuration file "src/config/database.js".
File: .gitkeep does not match pattern: /\.js$/
File: .gitkeep does not match pattern: /\.js$/
File: .gitkeep does not match pattern: /\.js$/
== 20190916183817-create-users: migrating =======
== 20190916183817-create-users: migrated (0.046s)

$ NODE_ENV=test jest
 PASS  __tests__/example.test.js
  ✓ if I call soma function with 4 and 5 it should return 9 (5ms)

----------|----------|----------|----------|----------|-------------------|
File      |  % Stmts | % Branch |  % Funcs |  % Lines | Uncovered Line #s |
----------|----------|----------|----------|----------|-------------------|
All files |        0 |        0 |        0 |        0 |                   |
----------|----------|----------|----------|----------|-------------------|
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.037s
Ran all test suites.
$ NODE_ENV=test sequelize db:migrate:undo:all

Sequelize CLI [Node: 10.16.2, CLI: 5.5.0, ORM: 5.9.4]

Loaded configuration file "src/config/database.js".
File: .gitkeep does not match pattern: /\.js$/
== 20190916183817-create-users: reverting =======
== 20190916183817-create-users: reverted (0.032s)

Done in 4.28s.
server on  master [!?] took 5s
```
## Teste com banco de dados e APIs

Para chamadas a API é possível utilizar o axios e fetch, porém tem uma lib que é própria para testes
```js
yarn add supertest -D
```

### Estrutura
- Teste que envolvem banco de dados, chamadas a api e etc, recebem o nome de integration
- Criar o arquivo `user.test.js`

```bash
├── __tests__
│   └── integration
│       └── controllers
│           └── user.test.js
├── tmp
```

## user.test.js
- Utilizando o conceito de TDD (test driven development), vamos primeiro criar o teste e depois vamos desenvolver o código para que este passe no teste.

```js
import request from 'supertest';
import app from '../../../src/app';

describe('User', () => {
  it('should be able to register', async () => {
    const response = await request(app)
      .post('/users')
      .send({
        name: 'Oscar Broch',
        email: 'brochj@gmail.com',
        password_hash: '34bi4h23dn93onf',
      });

    expect(response.body).toHaveProperty('id');
  });
});
```

- Com a rota `/users` criada, rodar o `yarn test` e resultado deve ser o seguinte

```bash
❯ yarn test
yarn run v1.17.3
$ NODE_ENV=test sequelize db:migrate

Sequelize CLI [Node: 10.16.2, CLI: 5.5.0, ORM: 5.9.4]

Loaded configuration file "src/config/database.js".
File: .gitkeep does not match pattern: /\.js$/
No migrations were executed, database schema was already up to date.
$ NODE_ENV=test jest
 PASS  __tests__/integration/controllers/user.test.js
  User
    ✓ should be able to register (143ms)

  console.log node_modules/sequelize/lib/sequelize.js:1176
    Executing (default): INSERT INTO `users` (`id`,`name`,`email`,`password_hash`,`created_at`,`updated_at`) VALUES
(NULL,$1,$2,$3,$4,$5);

--------------------|----------|----------|----------|----------|-------------------|
File                |  % Stmts | % Branch |  % Funcs |  % Lines | Uncovered Line #s |
--------------------|----------|----------|----------|----------|-------------------|
All files           |      100 |       75 |      100 |      100 |                   |
 controllers        |      100 |       75 |      100 |      100 |                   |
  UserController.js |      100 |       75 |      100 |      100 |                 1 |
 models             |      100 |       75 |      100 |      100 |                   |
  User.js           |      100 |       75 |      100 |      100 |                 1 |
--------------------|----------|----------|----------|----------|-------------------|
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        2.259s
Ran all test suites.
$ NODE_ENV=test sequelize db:migrate:undo:all

Sequelize CLI [Node: 10.16.2, CLI: 5.5.0, ORM: 5.9.4]

Loaded configuration file "src/config/database.js".
File: .gitkeep does not match pattern: /\.js$/
== 20190916183817-create-users: reverting =======
== 20190916183817-create-users: reverted (0.031s)

Done in 5.46s.
```

# Visualizando melhor

Na pasta `__tests__/coverage/lcov-report` abrir o arquivo `index.html` para ter uma melhor visualização dos arquivos e linhas que foram testados.

# Limpar Tabelas
- É possível executar comandos antes de cada `it()` ou `test()`. É interessante pois criamos ambiente isolado e controlado.
- Nesse caso vamos criar uma função que limpa os dados do database antes de rodar cada test.

## Exemplo de Teste de email duplicado
- Em `__tests__` vamos criar uma pasta e arquivo chamados `util/truncate.js`

### truncate.js
- Essa funçãoserá responsável por percorrer todos os models do banco de dados e removê-los utilizando o `.destroy()`
- `trucate: true` é um modo mais bruto para deletar tabelas do sqlite.
- `force: true` é para forçar o delete de tabelas que possuem relacionamentos.

```js
import database from '../../src/database';

export default function truncate() {
  return Promise.all(
    Object.keys(database.connection.models).map(key => {
      return database.connection.models[key].destroy({
        truncate: true,
        force: true,
      });
    })
  );
}
```

### user.test.js
- Vamos utilizar o método `beforeEach()` e passar a função `truncate()` dentro dele. Como o nome já diz, o que estiver dentro de `beforeEach()` será executado antes de iniciar o `it()` ou `test()`

```js
import request from 'supertest';
import app from '../../../src/app';

import truncate from '../../util/truncate';

describe('User', () => {
  beforeEach(async () => {
    await truncate();
  });

  it('should be able to register', async () => {
    //(...)
  });

  it('should not be able to register with duplicated email', async () => {
    await request(app)
      .post('/users')
      .send({
        name: 'Oscar Broch',
        email: 'brochj@gmail.com',
        password_hash: '34bi4h23dn93onf',
      });

    const response = await request(app)
      .post('/users')
      .send({
        name: 'Oscar Broch',
        email: 'brochj@gmail.com',
        password_hash: '34bi4h23dn93onf',
      });

    expect(response.status).toBe(400);
  });
});
```

# Teste de criptografia de senha

```js
import request from 'supertest';
import bcrypt from 'bcryptjs';
import app from '../../../src/app';

import User from '../../../src/app/models/User';
import truncate from '../../util/truncate';

describe('User', () => {
  beforeEach(async () => {
    await truncate();
  });

  it('should encrypt user password when new user created', async () => {
    const user = await User.create({
      name: 'Oscar Broch',
      email: 'brochj@gmail.com',
      password: '123456',
    });

    const compareHash = await bcrypt.compare('123456', user.password_hash);
    expect(compareHash).toBe(true);
  });

});

```

# Gerando dados aleatórios
- Instalar as libs

```bash
yarn add factory-girl faker -D
```

> Visitar o repositório do [faker.js](https://github.com/marak/Faker.js/)
> **faker.js** - generate massive amounts of fake data in the browser and node.js

- Criar na pasta `__tests__/factories.js`
- Esse arquivo será responsável por gerar os dados aleatórios.
- **É interessante criar sempre um factory para cada Model da aplicação**
- `factory.define('NomeDaFactory', Model, {camposModel})`

```js
import faker from 'faker';
import { factory } from 'factory-girl';

import User from '../src/app/models/User';

factory.define('User', User, {
  name: faker.name.findName(),
  email: faker.internet.email(),
  password: faker.internet.password(),
});

export default factory;
```


## Utilizando as factories
- `factory.create('NomeDaFactory',{override ramdom data})` : utilizando o `create`, além de gerar os dados aleatório, será criado o usuário na tabela de dados.
- `factory.attrs('NomeDaFactory');` : apenas gera e retorna os dados aleatórios.

- No exemplo de `user.test.js`
```js
import request from 'supertest';
import bcrypt from 'bcryptjs';
import app from '../../../src/app';

import factory from '../../factories';
import truncate from '../../util/truncate';

describe('User', () => {
  beforeEach(async () => {
    await truncate();
  });

  it('should encrypt user password when new user created', async () => {
    const user = await factory.create('User', {
      password: '123456',
    });

    const compareHash = await bcrypt.compare('123456', user.password_hash);
    expect(compareHash).toBe(true);
  });

  it('should be able to register', async () => {
    const user = await factory.attrs('User');
    // user = objeto com dados aletorio
    const response = await request(app)
      .post('/users')
      .send(user);

    expect(response.body).toHaveProperty('id');
  });

});
```
