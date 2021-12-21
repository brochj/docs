# Passando Parametros

## Criando rotas dinâmicas

Em `api.routes.ts` criar uma rota e criar um parametro `:id`

```sh
Route.get('/usuarios/:id', 'PainelController.usuario')
```

Em `PainelController` criar um método `usuario` que será responsável por buscar os dados de acordo com o `id` fornecido na Requisição

```js
//...
protected users = [
        {id: 1, name: "joao", apelido: "ja1"},
        {id: 2, name: "luciana", apelido: "lu"},
    ]

async usuario({params}){
        let userId = params['id']
        let myUser = this.users.find(user => user.id == userId)
        return myUser
    }
```

## Validando rotas dinâmicas

Perceba que `id` e `slug` estão no mesmo nível, mesma rota. O Adonis vai utilizar a primeira que ele encontrar

```js
Route.get('/usuarios/:id', 'PainelController.usuarioById')
Route.get('/usuarios/:slug', 'PainelController.usuarioBySlug')
```

Para funcionar as duas corretamente, temos que fazer uma verificação do tipo de dado passado no parâmetro.  

Para isso adicionamos um `where` na rota `:id` e validamos se essa rota for um número o adonis utilizará essa rota, caso o parâmetro não seja número o adonis redireciona para rota `:slug` 

```js
Route.get('/usuarios/:id', 'PainelController.usuarioById').where('id', /^[0-9]+$/)
Route.get('/usuarios/:slug', 'PainelController.usuarioBySlug')
```

Se não quiser usar expressão regular

```js
Route.get('/usuarios/:id', 'PainelController.usuarioById').where('id', Route.matchers.number())
Route.get('/usuarios/:slug', 'PainelController.usuarioBySlug').where('id', Route.matchers.slug())
```

## Parâmetros Opcionais e Coringas

### Parâmetros Opcionais 

Basta adicionar o `?` no final do parâmetro `:id` ficando `:id?`

```js
// api.routes
Route.get('/usuarios/:id?', 'PainelController.usuarioById').where('id', Route.matchers.number())
```

E no controller verificar se foi enviado um parâmetro

```js
async usuarioById({params}){
    if (!params['id']){
        return {user: this.users}
    }
    
    let userId = params['id']
    let myUser = this.users.find(user => user.id == userId)
    return myUser
}

```
### Parâmetros Coringas (wildcard) 

São parâmetros necessários, porém podem ser de diversos tipos

```js
// api.routes
Route.get('/docs/*', 'PainelController.docs')
```
e No controller
```js
async docs({params}){

    return params
}
```


Acessando essa Rota `/api/painel/docs/QualquerParametroAqui` temos como retorno

```json
{
  "*": [
    "QualquerParametroAqui"
  ]
}
```
Acessando essa Rota `/api/painel/docs/QualquerParametroAqui/SegundoParametro/Terceiro/Quarto` temos como retorno

```json
{
  "*": [
    "QualquerParametroAqui",
    "SegundoParametro",
    "Terceiro",
    "Quarto"
  ]
}
```

Acessando o primeiro parâmetro
```js
async docs({params}){

  return params['*'][0]
}
```