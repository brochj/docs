# Query Strings

As queries Strings ficam dentro do objeto `request`

```js
async index ({ request }){ 
  return {
    response: "index do Painel",
    qs: request.qs()
  }
}
```

Acessando `http://127.0.0.1:3333/api/painel/?idade=18`

```json
{
  "response": {
    "idade": "18"
  }
}
```

Acessando `http://127.0.0.1:3333/api/painel/?idade=18&sexo=masculino&filtro=2`

```json
{
  "response": "index do Painel",
  "qs": {
    "idade": "18",
    "sexo": "masculino",
    "filtro": "2"
  }
}
```