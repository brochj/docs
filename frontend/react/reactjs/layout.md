# Layouts por página
- Quando se tem páginas muitos parecidas, como uma tela de login e de cadastro, é interessante criar layouts

## Estrutura
- Em pages criar a pasta `_layouts`

```
├── pages
│   │   ├── Dashboard
│   │   │   └── index.js
│   │   ├── _layouts
│   │   │   ├── auth
│   │   │   │   ├── index.js
│   │   │   │   └── styles.js
│   │   │   └── default
│   │   │       ├── index.js
│   │   │       └── styles.js
```

- Os arquivos de layout terão esse formato

```js
import React from 'react';
import PropTypes from 'prop-types';

import { Wrapper } from './styles';

export default function DefaultLayout({ children }) {
  return <Wrapper>{children}</Wrapper>;
}

DefaultLayout.propTypes = {
  children: PropTypes.element.isRequired,
};
```

## Routes.js

- Em `routes/Route.js` podemos definir as condições de exibição do layout. Por exemplo, se o usuário estiver logado mostra um layout, se não mostra outro.

```js
import React from 'react';
import PropTypes from 'prop-types';
import { Route, Redirect } from 'react-router-dom';

import AuthLayout from '../pages/_layouts/auth';
import DefaultLayout from '../pages/_layouts/default';

export default function RouterWrapper({
  component: Component,
  isPrivate,
  ...rest
}) {
  const signed = false;

  if (!signed && isPrivate) {
    return <Redirect to="/" />;
  }

  if (signed && !isPrivate) {
    return <Redirect to="/dashboard" />;
  }

  const Layout = signed ? DefaultLayout : AuthLayout;

  return (
    <Route
      {...rest}
      render={props => (
        <Layout>
          <Component {...props} />
        </Layout>
      )}
    />
  );
  // Forma sem o layouts
  //return <Route {...rest} component={Component} />;

}
```