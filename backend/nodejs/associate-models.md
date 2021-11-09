# Relacionamento de Models

## No Model User

- Criar uma metodo

```js
...
  static associate(models) {
    // Abaixo - esse model user pertence ao model file
    this.belongsTo(models.File, { foreignKey: 'avatar_id' }); // avatar_id sera criada na tabela de Users
  }

  checkPassword(password) {
    ...
```

- No loader, `database/index.js` adicionar um novo map()

```js
...
    models
      .map(model => model.init(this.connection))
      .map(model => model.associate && model.associate(this.connection.models));
  ...
```

- esse map só roda se o Model tiver o método associate dentro. essa verificação é feita por `model.associate &&`

- Fazer a requisicao no insomnia, o id da table files deve aprecer no avatar_id da table users.
