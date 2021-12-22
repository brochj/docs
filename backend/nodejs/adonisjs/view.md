# View

## Criar Views

```sh
node ace make:view Homepage
```

Dentro da pasta `resources/views` será criado um arquivo `homepage.edge`

Dentro desse arquivo vamos escrever nosso `html`

E no nosso controller vamos passar essa view para o `render`

```js
export default class HomeController {
  async index({ view }) {
    return view.render("homepage");
  }

  async about() {
    return "About us";
  }
}
```

## Organizando as Views em pastas

Vamos criar uma pasta chamada `painel` dentro de `resources/views`, e dentro de `painel` será criado um arquivo `homepage.edge`

```sh
├── resources
│   └── views
│       ├── errors
│       │   ├── not-found.edge
│       │   ├── server-error.edge
│       │   └── unauthorized.edge
│       ├── homepage.edge
│       ├── painel  # Pasta criada
│       │   └── homepage.edge # Vamos usar essa view
│       └── welcome.edge

```

Depois é só usar `painel/homepage` para usar determinada view (ou `painel.homepage` deprecated)

```sh
export default class HomeController {

    async index({view}){
        return view.render('painel/homepage') # Referenciando o arquivo homepage.edge dentro da pasta painel
    }

    async about(){
        return 'About us'
    }
}

```

## Passando dados para a View

O segundo parâmetro do método `render` é para passar dados para dentro da view.

### Renderizando Objetos

```js
export default class HomeController {
  async index({ view }) {
    const data = {
      date: "30 jun 2021",
      user: {
        name: "Alessandro",
        age: 34,
        nickname: "kobs",
      },
    };
    return view.render("homepage", data);
  }
}
```

Depois dentro da View, usar `{{key}}` para acessar o dado passado

```html
<body>
  <h1>Homepage</h1>
  <h2>data: {{date}}</h2>
  <h2>Name: {{user.name}}</h2>
  <h2>Age: {{user.age}}</h2>
  <h2>Nickname: {{user.nickname}}</h2>
</body>
```

### Renderizando Arrays

#### Forma simples

```js
export default class HomeController {
  async index({ view }) {
    const data = {
      stack: ["ReactJS", "AdonisJS", "PostgreSQL"],
    };
    return view.render("homepage", data);
  }
}
```

Se quiser só juntar o item com vírgulas, o próprio Adonisjs já faz isso

```html
<h2>Stack: {{stack[0]}}</h2>
<h2>Stack: {{stack}}</h2>
```

Resultado

```sh
Stack: ReactJS
Stack: ReactJS,AdonisJS,PostgreSQL
```

#### Usando Loops

```js
users: [
  {  name: 'Alessandro',
     age: 34,
     nickname: 'kobs',
     stack: ['ReactJS', 'AdonisJS', 'PostgreSQL']
  },
  {  name: 'João',
     age: 24,
     nickname: 'sbok',
     stack: ['React-Native', 'MySql', 'Flutter']
  },
  {  name: 'Juliana',
     age: 27,
     nickname: 'Silverstone',
     stack: ['Express', 'Wordpress', 'Nextjs']
  },
]
```

```html
<ul>
  @each(user in users)
  <li>
    <h2>Name: {{user.name}}</h2>
    <h2>Age: {{user.age}}</h2>
    <h2>Nickname: {{user.nickname}}</h2>
    <h2>Stack: {{user.stack}}</h2>
  </li>
  @endeach
</ul>
```


### Condicionais

```js
users: [
  {  name: 'Alessandro',
     admin: true,
  },
  {  name: 'João',
     admin: false,
  },
  {  name: 'Juliana',
     admin: true,
  },
]
```

```html
<h2>Administradores</h2>
<ul>
    @each(user in users)
        @if(user.admin == true)
            <li>
                <h2>Name: {{user.name}}</h2>
            </li>
        @endif
    @endeach
</ul>
```

Resultado
```sh
Administradores
Name: Alessandro
Name: Juliana
```

Também dá para usar condição ternária do Javascript

```html
<h2>Administradores</h2>
<ul>
    @each(user in users)
      <li>
          <h2>Name: {{user.name}} {{user.admin? 'ADMIN' : 'USUÁRIO'}}</h2>
      </li>
    @endeach
</ul>
```

## Caracteres especiais 

Se quiser renderizar chaves duplas, coloque `@` na frente

```sh
@{{teste}}

# imprime -> {{teste}}
```

## injetar html

Caso passe um dado em `string`, mas que represente um `html`.

exemplo
```sh
let data = {
  myscript: "<script>alert('teste')</script>"
}
```

Caso precise "injetar" esse html na `View`, utilizo chave triplas

```sh
{{{myscript}}}
```

## Partial e Includes

Include serve para componentizar partes do sites que se repetem

Vamos criar uma pasta  `partials` dentro de `resources/views`, e dentro dela criar `header.edge` e `footer.edge`

1. `header.edge`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<header>Header</header>
```

2. `footer.edge`
```html
<footer>Footer</footer>
</body>
</html>
```

Agora podemos utilizar o `header` e `footer` dentro de outras views

```html
@include('partials/header')
<main>
Homepage
</main>
@include('partials/footer')
```