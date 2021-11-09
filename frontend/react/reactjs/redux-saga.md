# Redux Saga

```bash
yarn add redux-saga
```

- O Saga vai funcionar como um middleware. O fluxo será o seguinte:

1. O usuário dispara uma action que está sendo ouvida pelo saga em `store/modules/cart/sagas.js` (exemplo)
2. A action do saga faz o que precisa fazer, tipo um requisição.
3. Quando termina a action do saga, o próprio saga dispara uma action
4. E essa action está sendo ouvida pelo reducer.
5. Reducer faz as alterações de estados necessárias.

```js
// Sem Redux-saga
dispara a action 1 -> Reducer

// Com Redux-saga
dispara a action -> (action-saga executada) -> dispara action 1 -> Reducer
```

### Exemplo

#### Actions

- Como agora tem uma action a mais, mudar no arquivo `store/modules/cart/actions.js`

```js
// Sem redux saga
export function addToCartRequest(product) {
  return {
    type: '@cart/ADD',
    id,
  };
}
...
```

Para

```js
// Com redux saga
export function addToCartRequest(id) {
  return {
    type: '@cart/ADD_REQUEST',
    id,
  };
}
export function addToCartSuccess(product) {
  return {
    type: '@cart/ADD_SUCCESS',
    product,
  };
}
...
```

- `addToCartRequest()` é a action disparada pelo usuário lá no front-end e ouvida pelo redux-saga
- `addToCartSuccess()` é a action disparada pelo redux-saga e ouvida pelo reducer

#### Reducer

- No reducer mudar o tipo de action que está sendo ouvida, no caso de `@cart/ADD` para `@cart/ADD_SUCCESS`

```js
...
switch (action.type) {
    case '@cart/ADD_SUCCESS':
      return produce(state, draft =>
...
```

#### Sagas

- Em `store/modules/cart/sagas.js`

```js
import { call, put, all, takeLatest } from "redux-saga/effects";
import api from "../../../services/api";

import { addToCartSuccess } from "./actions";

function* addToCart({ id }) {
  const response = yield call(api.get, `/products/${id}`);

  // put é para disparar actions
  yield put(addToCartSuccess(response.data));
}

// all é pra ficar ouvindo as actions
export default all([takeLatest("@cart/ADD_REQUEST", addToCart)]);
```

#### rootSaga

- Fazer o load de todos os sagas `store/modules/rootSaga.js`

```js
import { all } from "redux-saga/effects";

import cart from "./cart/sagas";

export default function* rootSaga() {
  return yield all([cart]);
}
```

#### Carregando o redux-saga

- Em `store/index.js` fazer a configuração do redux-saga

```js
import { createStore, applyMiddleware, compose } from "redux";
import createSagaMiddleware from "redux-saga";

import rootReducer from "./modules/rootReducer";
import rootSaga from "./modules/rootSaga";

const sagaMiddleware = createSagaMiddleware();

const enhancer =
  process.env.NODE_ENV === "development"
    ? compose(console.tron.createEnhancer(), applyMiddleware(sagaMiddleware))
    : applyMiddleware(sagaMiddleware);

const store = createStore(rootReducer, enhancer);

sagaMiddleware.run(rootSaga);

export default store;
```

## Reactotron + Saga

```bash
yarn add reactotron-redux-saga
```

### Configurando o Reactotron

```js
import Reactotron from "reactotron-react-js";
import { reactotronRedux } from "reactotron-redux";
import reactotronSaga from "reactotron-redux-saga";

if (process.env.NODE_ENV === "development") {
  const tron = Reactotron.configure()
    .use(reactotronRedux())
    .use(reactotronSaga())
    .connect();

  tron.clear();

  console.tron = tron;
}
```

### Criando o saga monitor

- Em `store/index.js` fazer as alterações

```js
...
const sagaMonitor =
  process.env.NODE_ENV === 'development'
    ? console.tron.createSagaMonitor()
    : null;

const sagaMiddleware = createSagaMiddleware({
  sagaMonitor,
});
...
```

## Navegação com Redux-saga

```bash
yarn add history
```

- Em `services/history.js`

```js
import { createBrowserHistory } from "history";

const history = createBrowserHistory();

export default history;
```

- Em `app.js` mudar de `BrowserRouter` para `Router` e adicionar o history como propriedade

```js
import React from 'react';
import { Router } from 'react-router-dom';
import { Provider } from 'react-redux';
...
import history from './services/history';
..
function App() {
  return (
    <Provider store={store}>
      <Router history={history} >
        <Header />
        <Routes />
        <GlobalStyles />
        <ToastContainer autoClose={3000} />
      </Router >
    </Provider>
  );
}
export default App;
```

## Utilizando o history

- A navegação só será feita depois que terminar a chamada a api.
- Em algum arquivo `sagas.js`

```js
import { call, select, put, all, takeLatest } from 'redux-saga/effects';
...
import history from '../../../services/history';
...
function* addToCart() {
 // alguma chama na api
    history.push('/cart');
  }
}
```
