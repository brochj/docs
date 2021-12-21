
## MVC

- **Model**: Manipulação de dados - Interface de comunicação com o banco de dados
  - LucidORM
- **View**: Interação do usuário - Tudo que o usuário vê em tela
  - Edge
- **Controller**: Regra de negócio - Responsável por aplicar as regras de negócio do sistema, e faz uma ponte entre a view e model 


## Installation

```sh
npx create-adonis-ts-app@4.0.5 hello-world

```

```sh
CUSTOMIZE PROJECT
❯ Select the project structure · web
❯ Enter the project name · hello-world
❯ Setup eslint? (y/N) · false
❯ Configure webpack encore for compiling frontend assets? (y/N) · false
```

```sh
node ace serve --watch  
```


## Estrutura de pastas


```sh
.
├── ace
├── ace-manifest.json
├── app  # Pasta Principal, onde fica quase tudo que vamos criar
│   └── Exceptions
├── commands  
│   └── index.ts
├── config
│   ├── app.ts
│   ├── bodyparser.ts
│   ├── cors.ts
│   ├── drive.ts
│   ├── hash.ts
│   ├── session.ts
│   ├── shield.ts
│   └── static.ts
├── contracts
│   ├── drive.ts
│   ├── env.ts
│   ├── events.ts
│   └── hash.ts
├── env.ts  # Schemas de validação das variáveis de ambiente
├── node_modules
├── package.json
├── package-lock.json
├── providers
│   └── AppProvider.ts
├── public  # tudo que o usuário pode acessar
│   └── favicon.ico
├── resources
│   └── views
├── server.ts
├── start # Nessa pasta só é utilizada no momento de build 
│   ├── kernel.ts
│   └── routes.ts
└── tsconfig.json

```

## Arquivo .env

```env
PORT=3333
HOST=0.0.0.0
NODE_ENV=development
APP_KEY=VvYlCAyZm1LyLvz-5qFgG-gXwpgb-cKA
DRIVE_DISK=local
SESSION_DRIVER=cookie
CACHE_VIEWS=false
```

### Usando as varáveis de ambiente

```js
import Env from '@ioc:Adonis/Core/Env'

Env.get('APP_KEY')
```

## ace

Ver lista de comandos

```sh
node ace
```

## Fluxo da Aplicação

Requisição -> Router -> Controller -> Model -> DB -> Model -> Controller -> View -> Controller -> Response

## Criando um Controller

```sh
node ace make:controller Home
```

Esse comando cria um arquivo chamado `HomeController.ts` em `app/Controllers/Http/`

```js
export default class HomeController {}

```
Agora Adiciona métodos à essa classe

```js
// HomeController.ts
export default class HomeController {
  async index({view}){
      return view.render('welcome')
    }
}

```

```js
// start/Routes.ts
import Route from '@ioc:Adonis/Core/Route'

Route.get('/', 'HomeController.index')
```

