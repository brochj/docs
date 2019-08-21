# Models

Um model é utilizado para conseguir manipular o dados referente aquela entidade, seja para criar, alterar, deletar, etc.
## Criando um Model

### Model de usuário

- Dentro da pasta `app/models/` criar um arquivo com nome `User.js`. Adicionar o código:

```js
import Sequelize, { Model } from 'sequelize';

class User extends Model {
  static init(sequelize) { // metodo chamado pelo loader de models durante o .map()
    super.init( // chamando o metodo init() da classe Model
      {
        // Aqui não precisa das primaryKey, nem aquelas created_at e afins
        // Só é necessário aquilo que realmente o usuario vai inserir/ vir do frontend
        name: Sequelize.STRING,
        email: Sequelize.STRING,
        password_hash: Sequelize.STRING,
        provider: Sequelize.BOOLEAN,
      },
      { sequelize }
    );
  }
}

export default User;
```

- Com o model já criado ainda é necessário alguma forma de carregá-lo, para daí sim ser possível criar, alterar, deletar um usuário.

## Criando loader de Models

Um loader é um arquivo que vai fazer a conexão com o banco de dados Postgres que foi definido lá no `config/database.js`. Esse loader vai carregar todos os Models da aplicação, com isso a aplicação inteira passa a ter conhecimento desses Models.

- Dentro da pastas `src/database` criar um arquivo `index.js`

```js
  import Sequelize from 'sequelize';

  import User from '../app/models/User';
  //importando as config do banco de dados
  import databaseConfig from '../config/database';

  const models = [User];
  class Database {
    constructor() {
      this.init();
    }

    init() {// esse método que vai fazer a conexao com o DB e carregar os models
      this.connection = new Sequelize(databaseConfig); 
      // em this.connection já temos a conexão com a DB feita
      models.map(model => model.init(this.connection));
    }
  }

  export default new Database();
```

- `this.connection` será passado como parâmetro dentro de cada model da aplicação através do método `static init(sequelize)` de cada model. 
- Então para aplicar essa conexão em todos os models, cria-se um `array` de models.
```js
const models = [User];
```

- e aplica um `models.map()`
```js
models.map(model => model.init(this.connection));
```

- Na prática seria algo assim
```js
// app/models/User.js
...
class User extends Model {
  // metodo chamado pelo loader de models durante o .map() 
  // passando this.connection como parâmetro.
  static init(this.connection) { 
    super.init(
      ...
    );
  }
}  
```

- No arquivo `src/app.js` importar esse loader `import './database';` . Não precisa atribuir um nome, pois o nomde do loader é `index.js`.

### Testando Model criado
- Para verificar se o model está funcionando, no arquivo de `routes.js