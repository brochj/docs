- Toda vez que uma state muda, o método render() é executado
-  As funcoes que alteram estados devem ficar no mesmo arquivo dos estados, e nunca dentro de um outro componente em outro arquivo.

- Criar métodos utilizando arrow function para que esses tenha acesso ao `this.`

```js
handleInputChange = e => {
  this.setState({ newTech: e.target.value });
};
```

- Alterando estados em formatos de array

```js
handleSubmit = e => {
  e.preventDefault();
  this.setState({
    techs: [this.state.newTech, ...this.state.techs]
  });
};
```

- Removendo um item do estado de um array

```js
handleDelete = tech => {
  this.setState({
    techs: this.state.techs.filter(t => t !== tech)
  });
};
```
