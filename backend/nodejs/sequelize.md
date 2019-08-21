# Sequelize

## Instalando o Sequelize
>Necessita da estrutura MVC implementada.

- Para instalar 
```bash
yarn add sequelize
```

- Para executar as migrations e outros comandos úteis.
```bash
yarn add sequelize-cli -D
```

## Configurando o Sequelize

- Cria na Raiz do projeto um arquivo `.sequelizerc` e adicionar:
> Para ficar melhor de visualizar, mudar de PlainText para javascript no VSCode 

```js
  const { resolve } = require('path');

  module.exports = {
    'config': resolve(__dirname, 'src', 'config', 'database.js'),
    'models-path': resolve(__dirname, 'src', 'app', 'models'),
    'migrations-path': resolve(__dirname, 'src', 'database', 'migrations'),
    'seeders-path': resolve(__dirname, 'src', 'database', 'seeds'),
  }
```
- Para configurar o Dialects do sequelize é necessário as lib `pg` e `pg-hstore` como indica no tutorial oficial [Dialect- PostgresSQL](https://sequelize.org/master/manual/dialects.html).
```bash
yarn add pg pg-hstore
```
- No arquivo `config/database.js`
```js
  module.exports = {
    dialect: 'postgres',
    host: 'localhost',
    username: 'postgres',
    password: 'docker',
    database: 'gobarber',
    define: {
      timestamps: true,
      underscored: true,
      underscoredAll: true,
    },
  };
```


