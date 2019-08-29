# Mongo DB

Banco não relacional


## Criando um container
- Criar um container no docker utilizando a imagem do mongoDB

```bash
docker run --name mongomeetapp -p 27017:27017 -d -t mongo
```
- Para verificar se está tudo certo entrar em `http://localhost:27017/` deve aparecer a msg
```
It looks like you are trying to access MongoDB over HTTP on the native driver port.
```

### Mongoose

O mongoose é um ORM para o mongoDB, ele faz o que o sequelize faz para um banco SQL.

```bash
yarn add mongoose
```

## Configurando o MongoDB

- dentro de `database/index.js` criar o metodo `mongo()` e colocá-lo no constructor

```js
...
...
constructor() {
    this.init();
    this.mongo();
  }

  init() {
    // faz a conexao com o db e carrega os models
    this.connection = new Sequelize(databaseConfig);

    models
      .map(model => model.init(this.connection))
      .map(model => model.associate && model.associate(this.connection.models));
  }

  mongo() {
    const { MONGO_HOST, MONGO_PORT, MONGO_NAME } = process.env;

    const mongoURI = `mongodb://${MONGO_HOST}:${MONGO_PORT}/${MONGO_NAME}`;

    this.mongoConnection = mongoose.connect(mongoURI, {
      useNewUrlParser: true,
      useFindAndModify: true,
    });
  }
...
...
```

- o mongo ja está conectado à aplicação

## Utilizando o MongoDB

<!-- TODO Fazer a docoumentacao de como utilizar o mongo db (Modulo 03 - aula Notificando novos agendamentos)-->