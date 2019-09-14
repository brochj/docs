# Styled Components
```bash
yarn add styled-components
```

- instalar a extensão so styled components no vscode para ter o color highlight

### Criando um arquivo de estilização
```js
import styled from 'styled-components';

export const Title = styled.h1`
  font-size: 24px;
  color: #7159c1;
  font-family: Arial, Helvetica, sans-serif;

  small {
    font-size: 20px;
  }
`;
```

### Utilizando um arquivo de estilização
```js
import React from 'react';

import { Title } from './styles';

export default function Main() {
  return (
    <Title>
      Main
      <small>texto menor</small>
    </Title>
  );
}

```

## Passando propriedades
```js
...
export default function Main() {
  return (
    <Title error={true}>
      Main
      <small>texto menor</small>
    </Title>
  );
}

```

```js
...
export const Title = styled.h1`
  font-size: 24px;
  color: ${props => (props.error ? 'red' : '#7159c1')};
  font-family: Arial, Helvetica, sans-serif;
...
`;

```

# Criando estilização global
- Criar um arquivo em `src/styles/global.js`

```js
//global.js
import { createGlobalStyle } from 'styled-components';

export default createGlobalStyle`
  * {
    margin: 0;
    padding: 0;
    outline: 0;
    box-sizing: border-box
  }

  html, body, #root {
    min-height: 100%;
  }

  body {
    background: #7159c1;
    -webkit-font-smoothing: antialiased !important;
  }

  body, input, button {
    color: #222;
    font-size: 14px;
    font-family: Arial, Helvetica, sans-serif;
  }

  button {
    cursor: pointer;
  
`;

```

- Importar esse arquivo em `app.js`
```js
//app.js
import React from 'react';

import Routes from './routes';
import GlobalStyle from './styles/global';

function App() {
  return (
    <>
      <Routes />
      <GlobalStyle />
    </>
  );
}

export default App;
```