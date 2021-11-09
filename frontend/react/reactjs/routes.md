# Configurando rotas

```bash
yarn add react-router-dom
```

## app.js

```js
import React from "react";
import Routes from "./routes";

function App() {
  return <Routes />;
}

export default App;
```

## routes.js

```js
import React from "react";
import { BrowserRouter, Switch, Route } from "react-router-dom";

import Main from "./pages/Main";
import Repository from "./pages/Repository";

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

# Configurando rotas com history

## Estrutura

```
├── src
│   ├── App.js
│   ├── index.js
│   ├── pages
│   │   ├── Dashboard
│   │   │   └── index.js
│   │   ├── Profile
│   │   │   └── index.js
│   │   ├── SignIn
│   │   │   └── index.js
│   │   └── SignUp
│   │       └── index.js
│   ├── routes
│   │   └── index.js
│   └── services
│       └── history.js
```

## Dependências

```bash
yarn add history react-router-dom
```

## history.js

```js
// history.js
import { createBrowserHistory } from "history";

const history = createBrowserHistory();

export default history;
```

## routes/index.js

```js
// routes/index.js
import React from "react";
import { Router } from "react-router-dom";

import Routes from "./routes";
import history from "./services/history";

export default function src() {
  return (
    <Router history={history}>
      <Routes />
    </Router>
  );
}
```

## app.js

```js
// app.js
import React from "react";
import { Router } from "react-router-dom";

import Routes from "./routes";
import history from "./services/history";

export default function src() {
  return (
    <Router history={history}>
      <Routes />
    </Router>
  );
}
```
