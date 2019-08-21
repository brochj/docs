# Criando uma aplicacao no Nodejs

#### 
`yarn init -**y`

`yarn add express`

-  cria o arquivo 
`index.js`

## Retornando valores para o frontend
```js
server.get('/teste', (req,res)=>{
  return res.send('hello world')
})

```
- retornar um texto pleno
```js
 res.send('hello world')
```
- retornar um dado estruturado (JSON)
```js
 res.json({message: 'Hello World'})
```

## Recebendo valores do frontend
Tem 3 tipos de parametros

- Query params = ?teste=1




















