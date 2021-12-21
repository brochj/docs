# Rotas

## Criando as Rotas Simples

1. Vá em `start/routes.ts` e adicione uma rota 

```js
Route.get('/about', 'HomeController.about')
```

2. Em `HomeController.ts` adicione o método

```js
async about(){
  return 'About us'
}
```

## Criando Nested Routes

1. Vá em `start/routes.ts` e adicione uma rota 

```js
Route.get('/painel/', 'PainelController.index') // não esquecer do  / no final 
Route.get('/painel/usuarios', 'PainelController.usuarios')
```

2. `node ace make:controller Painel`

3. Em `PainelController.ts` adicione o método

```js
export default class PainelController {

    async index(){
        return {response: 'index do painel'}
    }

    async usuarios(){
        return {response: 'usuarios do painel'}
    }
}

```

## Separando rotas em arquivos

Não é legal deixar rotas que retornam View junto com rotas de API.

Dentro de `start/` criar um arquivo `api.routes.ts`

```js
import Route from '@ioc:Adonis/Core/Route'

Route.get('/painel/', 'PainelController.index')
Route.get('/painel/usuarios', 'PainelController.usuarios')

```
Tem duas maneiras de carregar esse arquivo

### forma 1: Alterando `adonisrc`
Ainda não vai funcionar pois `api.routes.ts` não está visível na aplicação. temos que carregá-lo, para isso vamos no arquivo `.adonisrc.json` e adiciona uma linha

```json
// .adonisrc.json
{
  ...
  "preloads": [
      "./start/api.routes", # Adiciona essa linha referenciando o arquivo criado
      "./start/routes",
      "./start/kernel" # OBS: kernel deve ser a última linha, não adiciona nada abaixo
    ],
  ...
}
```

### forma 2: Importando `api.routes`

No arquivo `routes.ts` adicionar a linha

```js
import Route from '@ioc:Adonis/Core/Route'
import './api.routes'  // add this line

Route.get('/', 'HomeController.index')
Route.get('/about', 'HomeController.about')
```

## Agrupando e definindo prefixos de rotas

Vamos agrupar as rotas de `api` dentro de uma rota `/api/`

```js
// api.routes.ts  ANTES
import Route from '@ioc:Adonis/Core/Route'

Route.get('/painel/', 'PainelController.index')
Route.get('/painel/usuarios', 'PainelController.usuarios')
```

```js
// api.routes.ts  DEPOIS
import Route from '@ioc:Adonis/Core/Route'


Route.group(()=> {
  
  Route.get('/painel/', 'PainelController.index')
  Route.get('/painel/usuarios', 'PainelController.usuarios')

}).prefix('/api')

```

Podemos criar grupos dentro grupos

```js
// api.routes.ts 

Route.group(()=> {
  Route.get('/admin/', 'PainelController.admin')
  
  Route.group(()=>{
    
    Route.get('/', 'PainelController.index')
    Route.get('/usuarios', 'PainelController.usuarios')

  }).prefix('/painel')

}).prefix('/api')
