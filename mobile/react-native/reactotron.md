# Configurando o reactotron

- Baixar o app do github e instalar [infinitered/reactotron](https://github.com/infinitered/reactotron/releases)
- Na pasta do projeto adicionar

```bash
yarn add reactotron-react-native
```

- Em `src/config/ReactotronConfig.js`

```js
import Reactotron from "reactotron-react-native";

if (__DEV__) {
  const tron = Reactotron.configure({ host: "192.168.16.101" })
    .useReactNative()
    .connect();

  console.tron = tron;

  tron.clear();
}
```

- se tiver no simulador, pode usar apenas `configure(})`

- Adicionar a variavel `__DEV__` no globals do do `.eslintrc`

```js
 globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
    __DEV__: 'readonly'
  },
```

### Utilizando

- Fazer o import do Reactotron no arquivo de entrada do app `src/index.js`

```js
import "./config/ReactotronConfig";
```

- Para utilizar é apenas um

````js
console.tron.log("Mensagem");
````
