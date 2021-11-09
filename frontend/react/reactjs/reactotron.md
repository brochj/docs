# Reactotron no ReactJS

```bash
yarn add reactotron-react-js
```

## Estrutura

```
├── src
│   ├── App.js
│   ├── config
│   │   └── ReactotronConfig.js
│   ├── index.js
```

## ReacotoronConfig.js

```js
import Reactotron from "reactotron-react-js";

if (process.env.NODE_ENV === "development") {
  const tron = Reactotron.configure().connect();

  tron.clear();
  console.tron = tron;
}
```

## Utilizando

- Fazer o import do Reactotron no arquivo de entrada do app `src/index.js`

```js
import "./config/ReactotronConfig";
```

- Para utilizar é apenas um

```js
console.tron.log("Mensagem");
```
