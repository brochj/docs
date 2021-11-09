# Root Import

- Com o comando `npx create-react-app` não temos acesso as configurações do babel e webpack. Para ter acesso vamos instalar

```bash
yarn add customize-cra react-app-rewired -D
```

- Instalar o plugin do babel

```bash
yarn add babel-plugin-root-import -D
```

- Na raiz do Projeto criar um arquivo chamado `config-overrides.js`. Esse arquivo de configuração será carregado pelo `react-app-rewired` quando utilizarmos os scripts de `start`, `build` e `test`.

```js
// /config-overrides.js
const { addBabelPlugin, override } = require("customize-cra");

module.exports = override(
  addBabelPlugin([
    "babel-plugin-root-import",
    {
      rootPathSuffix: "src",
    },
  ])
);
```

- No `package.json` trocar os scripts de `start`, `build` e `test` por

```json
"scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-scripts eject"
  },
```

## Utilizando

- Neste momento já será possível fazer o import da seqguinte maneira

```js
// Modo antigo
import AuthLayout from "../pages/_layouts/auth";
// Modo com babel-plugin-root-import
import AuthLayout from "~/pages/_layouts/auth";
```

- o `~` representa a pasta `src`, que foi definido em `rootPathSuffix: 'src'`

## Configurando o ESLint

- Adicionar

```bash
yarn add eslint-import-resolver-babel-plugin-root-import -D
```

- No arquivo `.eslintrc` lá no final, adicionar as `settings`.

```js
rules: {
    ( ... )
  },
  settings: {
    "import/resolver": {
      "babel-plugin-root-import": {
        rootPathSuffix: "src"
      },
    },
  },
```

## Configurando acesso ao arquivos

- Com passo realizado acima, provavelmente no VSCode não estará funcionando a questão de segurar o `Ctrl` e clicar em cima do caminho do arquivo para abrí-lo

```js
import AuthLayout from "~/pages/_layouts/auth";
```

- Para arrumar, criar um arquivo na pasta raiz `jsconfig.json`

```json
// /jsconfig.json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "~/*": ["*"]
    }
  }
}
```
