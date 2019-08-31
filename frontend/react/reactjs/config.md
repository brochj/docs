# Configurando projeto do zero

```bash
yarn create react-app nomedoapp
```

- Em package.json, apagar a parte do eslint
- Retirar o manifest de `public/index.html` caso não for usar PWA.

## editorconfig
```bash
root = true

[*]
end_of_line = lf
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

## Eslint 
```bash
yarn add eslint -D 
```
```bash
yarn eslint --init 
```
- remover o packge-lock.json e rodar o comando `yarn` para atulizar a dependencias

```js
//.eslintrc 
module.exports = {
  env: {
    browser: true,
    es6: true,
  },
  extends: [
    'airbnb',
    'prettier',
    'prettier/react'
  ],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parser: 'babel-eslint',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  plugins: [
    'react',
    'prettier'
  ],
  rules: {
    'prettier/prettier': 'error',
    'react/jsx-filename=extension': [
      'warn',
      { extensions: ['.jsx', '.js'] }
    ],
    'import/prefer-default-export': 'off'
  },
};

```

## Prettier
```bash
yarn add prettier eslint-config-prettier eslint-plugin-prettier babel-eslint -D 
```

```js
// .prettierrc
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```