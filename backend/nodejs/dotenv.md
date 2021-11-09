# Variáveis Ambiente

```bash
yarn add dotenv
```

- no `app.js` fazer o import do doenv na primeira linha do arquivo, fazendo isso ele vai pegar as infos de `.env` e guardar as variáveis em uma variável local q poderá ser aacessada por `process.env.NOME_DA_VARIAVEL`.

```js
// app.js
import 'dotenv/config';
...
...
```

- Como a queue roda em um processo paralelo, deve importar o `dotenv` lá tmbm.

```js
// queue.js
import 'dotenv/config';
...
...
```

- Por último, importar em `config/database.js`

```js
// database.js
require('dotenv/config');
...
...
```

- Criar um arquivo `.env` na raiz e adicioná-lo no `.gitignore`
- Dentro do arquivo `.env`

```bash
# .env
APP_URL=http://localhost:3333
NODE_ENV=development

# Auth

APP_SECRET=022e48bba4be9ef278918a86f2a5fa4e

# Database

DB_HOST=localhost
DB_USER=postgres
DB_PASS=docker
DB_NAME=meetapp
```

## Criando env example

Como o `.env` não vai para o github é interessante criar um arquivo chamado `.env.example` e copiar o `.env` para dentro, porém retirando todos os dados sensíveis. Assim, caso alguem baixe aquele projeto saberá quais variáveis tem que preencher.

```bash
# .env.example
APP_URL=http://localhost:3333
NODE_ENV=development

# Auth

APP_SECRET=022e48bbabe9ef278918a86f2a5fa4e

# Database

DB_HOST=
DB_USER=
DB_PASS=
DB_NAME=
```
