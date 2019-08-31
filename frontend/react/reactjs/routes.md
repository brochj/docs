# Configurando rotas

```bash
yarn add react-router-dom
```

## app.js
```js
import React from 'react';
import Routes from './routes';

function App() {
  return <Routes />;
}

export default App;
```

## routes.js
```js
import React from 'react';
import { BrowserRouter, Switch, Route } from 'react-router-dom';

import Main from './pages/Main';
import Repository from './pages/Repository';

// Switch garante que uma unica rota seja exibida por vez
export default function Routes() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" exact component={Main} />
        <Route path="/repository" component={Repository} />
      </Switch>
    </BrowserRouter>
  );
}


```