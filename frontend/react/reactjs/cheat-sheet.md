- Toda vez que uma state muda, o método render() é executado
-  As funcoes que alteram estados devem ficar no mesmo arquivo dos estados, e nunca dentro de um outro componente em outro arquivo.
-  instalar o `prop-types`
```js
TechItem.defaultProps ={
  tech: 'Oculto'
}

TechItem.propTypes = {
  tech: PropTypes.number
}
```

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

### Ciclo de Vida

- O `componentDidMount()` é executado  assim que o componente aparece na tela.
- O `componentDidUpdate(prevProps, prevState)` é executado  sempre que houver alterações nas props ou estados.
- O `componentWillUnmount()` é executado quando o componente deixa de existir.


## Ícones
```bash
yarn add react-icons
```
- Utilizando
```js
import React from 'react';
import { FaGithubAlt } from 'react-icons/fa';

import { Container } from './styles';

export default function Main() {
  return (
    <Container>
      <h1>
        <FaGithubAlt />
        Repositórios
      </h1>
    </Container>
  );
}

```