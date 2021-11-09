# Sequelize

É responsável por fazer a conexão com o banco de dados.

## Instalando o Sequelize

> Necessita da estrutura MVC implementada.

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
const { resolve } = require("path");

module.exports = {
  config: resolve(__dirname, "src", "config", "database.js"),
  "models-path": resolve(__dirname, "src", "app", "models"),
  "migrations-path": resolve(__dirname, "src", "database", "migrations"),
  "seeders-path": resolve(__dirname, "src", "database", "seeds"),
};
```

- Para configurar o Dialects do sequelize é necessário as lib `pg` e `pg-hstore` como indica no tutorial oficial [Dialect- PostgresSQL](https://sequelize.org/master/manual/dialects.html).

```bash
yarn add pg pg-hstore
```

- No arquivo `config/database.js`

```js
module.exports = {
  dialect: "postgres",
  host: "localhost",
  username: "postgres",
  password: "docker",
  database: "gobarber",
  define: {
    timestamps: true,
    underscored: true,
    underscoredAll: true,
  },
};
```

## Criando uma migration

A migration serve para criar a tabela dentro do banco de dados.

- **Exemplo** de uma migration que cria uma tabela de usuários.

```bash
yarn sequelize migration:create --name=create-users
```

- Depois de rodar o comando acima, deve ter criado automaticamente um arquivo de migration dentro da pasta `database/migrations`

- Dentro do arquivo criado deve ter algo assim.

```js
"use strict";

module.exports = {
  up: (queryInterface, Sequelize) => {
    /*
          Add altering commands here.
          Return a promise to correctly handle asynchronicity.

          Example:
          return queryInterface.createTable('users', { id: Sequelize.INTEGER });
        */
  },

  down: (queryInterface, Sequelize) => {
    /*
          Add reverting commands here.
          Return a promise to correctly handle asynchronicity.

          Example:
          return queryInterface.dropTable('users');
        */
  },
};
```

- O método `up:` é usado quando a migration for executada.
- O método `down:` é usado pra dar rollback dessa migration.

## Definindo campos da tabela

Ainda dentro do arquivo de migration, definir os campos da seguinte maneira

- **Exemplo** tabela de usuários

```js
module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.createTable("users", {
      id: {
        type: Sequelize.INTEGER,
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
      },
      name: {
        type: Sequelize.STRING,
        allowNull: false,
      },
      email: {
        type: Sequelize.STRING,
        allowNull: false,
        unique: true,
      },
      password_hash: {
        type: Sequelize.STRING,
        allowNull: false,
      },
      provider: {
        type: Sequelize.BOOLEAN,
        defaultValue: false,
        allowNull: false,
      },
      created_at: {
        type: Sequelize.DATE,
        allowNull: false,
      },
      updated_at: {
        type: Sequelize.DATE,
        allowNull: false,
      },
    });
  },

  down: (queryInterface) => {
    return queryInterface.dropTable("users");
  },
};
```

## Executando uma migration

- Para executar uma migration

```bash
yarn sequelize db:migrate
```

- Com esse comando, o sequelize cria a tabela dentro do banco de dados de acordo com o que foi definido no arquivo de migration.

> IMPORTANTE: O nome da database que está no arquivo `config/database` deve ser o mesmo nome de quando for criar o database dentro do Postbird, se não vai dar o erro abaixo.

```bash
Loaded configuration file "src/config/database.js".
ERROR: database "meetapps" does not exist
error Command failed with exit code 1.
```

## Desfazendo uma migration

- Para desfazer a última migration

```bash
yarn sequelize db:migrate:undo
```

- Para desfazer todas as migrations

```bash
yarn sequelize db:migrate:undo:all
```
